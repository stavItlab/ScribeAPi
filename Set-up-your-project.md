# III. Set up your project

If you follow along in this section step-by-step, there's a very good chance you'll create your first Scribe project. Since each project has its own combination features and requirements, there may be sections that you can skip. Rest assured, we will tell you when you can do so.

## Set up your environment

With the exception of the Mongo database, the setup of a Scribe project is more or less like a typical Rails project.

*[TODO: more specific tech instructions with code snippets, etc]*

1. Install Rails
2. Install MongoDB
3. Clone repository
4. Install gems
5. Install node modules 
6. Create, migrate, and seed your database
7. Start server, open browser

## Configure your project

Typically, the only thing you'll need to do after preparing your images and setting up your environment is to define update the configuration file to suit your project's needs.

### Enter Project Details

First, create a new project by entering your details in the project object. For example:

```var project = Project.create({
  producer: 'Zooniverse/NYPL',
  title: 'Whale Tales',
  description: 'The world\'s largest whaling library has been digitized.',
  home_page_content: '&lt;h1&gt;Whale Tales&lt;/h1&gt;&lt;p&gt;Lorem ipsum dolor sit amet, consectetur adipiscing elit.&lt;/p&gt;',
  summary: 'Transcribe ship logs from the New Bedford Whaling Museum',
  organizations: [
    {
      name: 'Zooniverse',
      location: 'Chicago IL',
      description: 'World leaders in Citizen Science',
      url: 'https://www.zooniverse.org'
    }
  ],
  team: [
    {
      name: 'John Doe',
      location: 'New Bedford, MA',
      description: '',
      url: 'http://www.whalingmuseum.org'
    }
  ],
  background: ''
})```

### Define tasks

You can create a new task by creating an object with the following parameters:

| PARAMETER | TYPE | DEFAULT VALUE | REQUIRED? | DESCRIPTION |
| :-------- | :--- | :------------ | :-------- | :---------- |
| `tool` | String, tool [pick_one, point, row, rectangle, text, select, number, date] | pick_one | yes | The tool used to perform this task, see [tools reference](#tools) for details |
| `field_name` | String, key | none | yes | The name of the data-model field, e.g. "date" |
| `label` | String | none | yes | The human-readable name of this task, e.g. "Date" |
| `instruction` | String | none | no | Descriptive text for this task, e.g "Please type-in the date" |
| `next_task` | String, key | nil | no | The key of the task that follows this one |

#### Example task objects

```var transcribe_tasks = {
  journal_date: {
    key: 0,
    tool: 'singleDate',
    field_name: 'date',
    label: 'Date',
    instruction: 'Please type-in the log date.',
    next_task: 'journal_entry'
  },
  journal_entry: {
    key: 1,
    tool: 'textBlock',
    field_name: 'journal_entry',
    label: 'Journal Entry',
    instruction: 'Please type-in the journal entry for this day.',
    next_task: 'additional_comment'
  },
    additional_comment: {
    key: 2,
    type: 'textBlock',
    field_name: 'other_entry',
    label: 'Other Entry',
    instruction: 'Type something, anything.',
    next_task: nil
  }
};```

### Define workflows

You can create a new workflow by creating an object with the following parameters:

| PARAMETER | TYPE | DEFAULT VALUE | REQUIRED? | DESCRIPTION |
| :-------- | :--- | :------------ | :-------- | :---------- |
| `name` | String | none | yes | The name of this workflow, e.g. "transcribe" |
| `label` | String | none | yes | The human-readable name of this workflow, e.g. "Transcribe Workflow" |
| `first_task` | String, key | none | yes | The key of the first task, e.g. "journal_entry" |
| `tasks` | Hash of Objects, tasks | none | yes | A hash of task objects |
| `enables_workflows` | Hash of Objects, workflows | none | no | A hash of workflow objects that this workflow enables |
| `project` | Object, project | none | yes | The project to which this workflow belongs |

#### Example workflow object

```var transcribe_workflow = Workflow.create(
  {
    name: 'transcribe',
    label: 'Transcribe Workflow',
    first_task: 'journal_entry',
    tasks: transcribe_tasks,
    enables_workflows: {},
    project: project
  }
);```

### Define assets path

You can configure where your assets are being pulled from by...

### <a name="tools"></a>Tools reference

Here is a list of interface tools available for users to perform tasks with. You can refer to this table when defining your tasks.

#### Core Tools

Core tools can appear in either the Transcribe and Mark workflows

##### Pick One

A simple tool that presents two or more optional tasks. Contains parameter `options`, an array of hashes with following properties:

| PARAMETER | TYPE | DESCRIPTION |
| :-------- | :--- | :------------ |
| `label` | String, pixels | Friendly label of option |
| `task` | String, key | Key of TASK to jump to if user clicks this option |

#### Marking Tools

##### Point Tool

A single point [x, y] in an image. Options:

| PARAMETER | TYPE | DEFAULT VALUE |
| :-------- | :--- | :------------ |
| `radius` | Integer, pixels | 40 |
| `fill_color` | String, CSS color | rgba(0,0,0,0.30) |

##### Text Row Tool

Document-wide rectangular selector suited to identifying rows of horizontal text that span the width of the document. Options:

| PARAMETER | TYPE | DEFAULT VALUE |
| :-------- | :--- | :------------ |
| `fill_color` | String, CSS color | rgba(0,0,0,0.30) |
| `stroke_color` | String, CSS color | #fff |
| `stroke_width` | Integer, pixels | 3 |
| `min_height` | Integer, pixels | 0 |
| `max_height` | Integer, pixels | none |

##### Rectangle Tool

A single rectangular region [x, y, w, h] in an image. Same options as Text Row Tool, plus:

| PARAMETER | TYPE | DEFAULT VALUE |
| :-------- | :--- | :------------ |
| `min_width` | Integer, pixels | 0 |
| `max_width` | Integer, pixels | none |

#### Transcribing Tools

##### Text Tool

A single text input. Options:

| PARAMETER | TYPE | DEFAULT VALUE | DESCRIPTION |
| :-------- | :--- | :------------ | :---------- |
| `limit` | Integer | none | Character limit |
| `suggest` | Array of Strings or URL String | [] | auto-complete suggestions for current entry |
| `multiline` | Boolean | false | Indicates whether or not value is expected to have line-breaks. |
| `match` | String | none | Regex defining valid strings (e.g. "^[a-z]+$") |

##### Number Tool

An extension of the Text Tool. Options:

| PARAMETER | TYPE | DEFAULT VALUE |
| :-------- | :--- | :------------ |
| `minimum` | Integer or Float | none |
| `maximum` | Integer or Float | none |

##### Select Tool

Useful when expected values are few, presents valid options as a list, optionally with a manual entry. Options:

| PARAMETER | TYPE | DEFAULT VALUE | DESCRIPTION |
| :-------- | :--- | :------------ | :---------- |
| `options` | Array of Strings | [] | The options to select from |
| `allow_other` | Boolean | false | If true, final option will be "Other..." and will allow manual entry |
| `multiselect` | Boolean | false | If true, multiple values can be selected |

##### Date Tool

A date (and date range) picker that supports approximates dates and pre-1970 dates. Options:

| PARAMETER | TYPE | DEFAULT VALUE | DESCRIPTION |
| :-------- | :--- | :------------ | :---------- |
| `minimum` | String, date | none | ISO 8601 date string establishing oldest allowed date (e.g. "-30000101" for 3000 BCE) |
| `maximum` | String, date | none | ISO 8601 date string establishing maximum allowed date (e.g. "20150227") |
| `range` | Boolean | false | If true, a date range may be selected |
| `allow_approximate` | Boolean | false | If true, user may check a box to indicate date is approximate. |

## Customize your project

### Add custom pages

You can add custom pages directly in your configuration file. Simply create an array of page objects with the following parameters:

| PARAMETER | TYPE | DESCRIPTION |
| :-------- | :--- | :---------- |
| `name` | String | The name of the page as it appears in the URL, e.g. "about" |
| `title` | String | The human-readable title of the page, e.g. "About Us" |
| `content` | String, html | The content of the page in HTML |

#### Example page objects

```var pages = [
  {
    name: 'science',
    title: 'Science Page',
    content: '&lt;h1&gt;Science Page&lt;/h1&gt;&lt;p&gt;I am a science!&lt;/p&gt;'
  },{
    name: 'about',
    title: 'About Us',
    content: '&lt;h1&gt;About Us&lt;/h1&gt;&lt;p&gt;This is the about page.&lt;/p&gt;'
  }
]```

### Change the look and feel

You can override the default look-and-feel by...

