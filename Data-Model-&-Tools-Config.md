# Data Model
A first pass distillation of the Scribe data model as shared by ruby and js.

## Project
The project is the top-level element defining project properties, site pages, and defining workflows. There SHOULD be only one project. It contains the following fields:
* `description`: Text
* `producer`: String
* `title`: String
* `workflows`: Array of WORKFLOWs

## Workflow
Because tools are namespaced by workflow key ('mark','transcribe'), there will be only two workflows possible without hacking. **[Verify]** Workflow properties include:
* `key`: String - Unique id for this workflow. (e.g. 'mark', 'transcribe')
* `label`: String - Friendly name for workflow (e.g. "Mark Stuff!")
* `first_task`: TASK id
* `tasks`: Hash mapping task ids to TASKs **[Or is it an array, as in project/example_project/workflows/mark.rb ?]**
* `enables_workflows`: Hash mapping WORKFLOW ids to sub-hashes that include the following keys: 
    * `denormalized_fields`: Array of fields to copy into generated subjects. By default, the id of the SUBJECT acted upon (and task `type`?) is also copied. **[Verify]**
    * **[Anything else? What other config required for subject generation?]**

The enables_workflows object specifies for each workflow key a simple specification for transitioning submitted annotations from the current workflow to the workflow identified by the key.

## Task
* `key`: String - Workflow-unique alphanumeric (e.g. '0','1','mark_one')
* `type`: Enum "text","integer","date" - Seems to include these basic data types but also things like "drawing", "textBlock". Seems like `type` could refer to data type desired (e.g. string, date, int, float, bounding box, point, polygon) but may in current practice be used to hint at tool (e.g. pick_page_type, textBlock).
* `directions`: Text - Friendly prompt given to user, which contextualizes task (e.g. "How many penguins are there?", "What color is this penguin?", "Choose the type of document") **[This is sometimes given as 'instruction']**
* `field_name`: String - Another alphanumeric workflow-unique id like 'key' above? **[Verify]**
* `tool`: String - Identifies tool to show. Note that there are distinct tools for mark and transcribe workflows. **[This is sometimes given as `tools`]***
* `options`: Hash - Specify arbitrary tool options. See "Tools" 

## Classification
* `location`: String - **[Not sure what this is]**
* `annotations`: Object - **[Not sure why this is an Object, what its composition is]**
* `started_at`: Date - Submitted by JS when created
* `finished_at`: Date - Submitted by JS when created
* `user_agent`: String - Submitted by JS when created
* `subject`: SUBJECT
* `workflow`: WORKFLOW

## Subject
A "primary" subject represents a single image. A "secondary" subject represents an annotation made on a primary subject. A "tertiary" subject annotates a secondary subject. Fields include:
* `name`: String
* `location`: Hash mapping identifiers to URLs. (e.g. 'standard' => 'http://...')
* `type`: Enum "root", ... **[What other values?]**
* `meta_data`: Hash - Includes width, height and other arbitrary known data imported from subject CSVs that might be useful when transcribing like subject type, date
* `thumbnail`: String - Thumbnail URL
* `file_path`: String - Path/URL to original asset **[Verify]**
* `classification_count`: Int - Denormalized count of subjects that are annotations on this subject.
* `retire_count`: Int - Number of annotations required before this subject is retired. Inherited from Group.
* `state`: Enum "active", "done" - Subjects marked done are not served to any workflow.
* `random_no`: Float (0...1) - Generated on-save.
* `order`: Int - Order within Group? **[Verify]**

# SubjectSet
A Subject always belongs to a single SubjectSet. Multi-page documents are represented by multiple subjects associated by a single subject-set. Fields include:
* `name`: String
* `subjects`: Many SUBJECTs

## Group
Groups organize subject-sets into related collections.

Note that although group membership and metadata may be helpful to the project maintainer and transcriber (if group metadata is displayed with member subjects) annotations are applied to subjects exclusively. It's not currently possible to annotate a group. 

Athough groups principally serve the purpose of collecting several intellectually distinct items under a single familiar topic or entity (e.g. grouping by ship in Old Weather), Groups may be exploited in the future to enable multi-image document annotation. Many items - like theater playbills - span multiple pages and it's sometimes necessary to see a page in the context of it's neighbors to adequately transcribe it. Theater playbill cast lists sometimes span multiple pages, for example; Page two of such a list may be confusing without being able to see the list heading on the preceding page. **[Verify]**

Group fields include:
* `name`: String - As given by groups CSV
* `description`: Text - As given by groups CSV
* `cover_image_url`: String - URL of group representative image
* `external_url`: String - URL of another representation of this object (e.g. wikipedia) if avail
* `meta_data`: Hash - Includes arbitrary known data imported from group CSVs that might be useful to display in transcription interface
* `selection_method`: Enum "linear", "random" - Indicates method for selecting subject-sets from this group for marking, whether linearly or randomly.
* `subject_sets`: Many SUBJECTSETs

# Tools
Tools are pluggable, configurable widgets that perform a single, simple task related to identifying an area of the subject ("marking"), adding data to a subject ("transcribing"), or moving the user from one tool to the next ("core"). 

**[Note that this gets pretty speculative. This is an attempt to formalize the conventions I see arising in the code.]**

## Core Tools **[proposed designation]**
Certain tools (e.g. 'pick_one') are "core tools", meaning they may appear in either the Transcribe or Mark workflows. Core tools are defined internally. **[Maybe better placed in components/core-tools or something?]** (If a tool isn't a core tool, it can be found in either components/mark or components/transcribe depending on the workflow in which it appears.)

### Pick One
Pick One is a simple tool that presents two or more optional tasks. This is currently defined as a hash mapping keys (e.g. "history_sheet", "attestation") to sub-hashes with a single next_task key that indicates the task. It's unclear what label is used for the option. **[Proposed revision below]*** 
 * `options`: Array of hashes with following properties
   * `label`: String - Friendly label of option (e.g. "This looks like a Casualty Form...", "This looks like an attestation..")
   * `next_task`: String - Key of TASK to jump to if user clicks this option. (Alt names we've used include `leads_to`, `task`)
   * `number_of_rounds`: Enum "many", "one" - Default "one". Indicates how many iterations of choices user may make. If "many" user can return to the picker after completing an option so that other options can be pursued. "Many" should be used anytime there are multiple potentially relevant tools to apply, for example multiple entities to identify.


## Marking Tools
Marking tools include various methods for identifying specific points and areas of images. They're defined in components/mark.

All marking tools generate the following common metadata fields (in addition to tool-specific metadata noted below):
 * `x`: Integer - Pixel coordinate within parent subject
 * `y`: Integer - Pixel coordinate within parent subject

**[Proposed]** All marking tools accept the following options (in addition to tool specific options noted below):

 * `fill_color`: String - CSS color. (Default "rgba(0,0,0,0.30)")
 * `stroke_color`: String - CSS color. (Default "#fff")
 * `stroke_width`: Integer Pixel stroke width (Default 3)  

### Point Tool
Special Options:
 * `radius`: Integer - Pixel radius (Default 40)

### Text Row Tool
Document-wide rectangular selector suited to identifying rows of horizontal text that span the width of the document.

Extra metadata generated: 
 * `yUpper`: Integer
 * `yLower`: Integer

Options:
 * `min_height`: Integer (or float percentage of subject)
 * `max_height`: ditto

### Vertical Mark Tool
**[I'm not sure what this is.]**

Extra metadata generated: 
 * `yUpper`: Integer
 * `yLower`: Integer

Options:
 * `min_height`: Integer (or float percentage of subject)
 * `max_height`: ditto

## Transcribe Tools
Transcribe tools are widgets suitable for gathering specific types of data with configurable constraints.

### Transcribe Row Tool
At writing, this tool presents multiple forms - one for each transcribe task. Each form contains a single field styled based on the task type property. 

### Text Tool  **[proposed]**
Probably the simplest tool, the text tool presents a single text input. The tool can be augmented with options below.

Options:
 * `limit`: Integer - Character limit.
 * `suggest`: Either an array of strings (e.g. ["cat","dog","other"]) or a URL returning auto-complete suggestions for current entry (e.g. "http://example.com/terms/suggest?term=%%TERM%%" )
 * `multiline`: Boolean - Indicates whether or not value is expected to have line-breaks. Note that sufficiently large values of `limit` imply use of a textarea regardless.
 * `match`: String - Regex defining valid strings (e.g. "^[a-z]+$")

For example, 
```
transcribe_workflow = {
    "key":             "transcribe",
    "label":             "Transcribe Content",
    "first_task":        "journal_entry",
    "tasks": {
      "journal_entry": {
        "key":          "0",
        "tool":         "text-tool",
        "tool_options": {
          "limit": null,
          "multiline": true
        },
        "instruction":  "Drag a mark around a block of text.",
      }
    }
    "enables_workflows": {}, 
    "project":           ...
}
```
### Number Tool  **[proposed]**
An extension of the Text Tool (perhaps using `match` option to restrict characters like "^-?\d+([,.]\d+)?$")
 * `minimum`: Integer/Float
 * `maximum`: Integer/Float

### Select Tool  **[proposed]**
Useful when expected values are few, presents valid options as a list, optionally with a manual entry. Options include:
 * `options`: Array of string values
 * `allow_other`: Boolean - If true, final option will be "Other..." and will allow manual entry
 * `multiselect`: Boolean - If true, multiple values can be selected.

### Boolean Tool  **[proposed]**
Really just a shorthand for the Select Tool with `options` = ["Yes", "No"]

### Date Tool  **[proposed]**
A date (and date range) picker that supports approximates dates and pre-1970 dates.
* `minimum`: String - ISO 8601 date string establishing oldest allowed date (e.g. "-30000101" for 3000 BCE)
* `maximum`: String - ISO 8601 date string establishing maximum allowed date (e.g. "20150227")
* `range`: Boolean - If true, a date range may be selected
* `allow_approximate`: Boolean - If true, user may check a box to indicate date is approximate.

### Composite Tool  **[proposed]**
A composite tool is a tool composed of two or more basic tools. A composite tool presents multiple tools side by side for cases where the mark being considered contains multiple distinct data that are confusing to consider in isolation. Options include:
 * `tools`: Array of tool configurations from those listed above.

 




