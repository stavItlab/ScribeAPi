# Design Specifications
## High Level Overview
Scribe is designed to be a point-and-click configurable tool enabling scientists, librarians, and others to create text-based structured data projects from digitized documents.

## Experience Walkthrough
### Example 1
Ken the Curator has an idea for a crowdsourcing project. He wants "The Crowd" to transcribe the full text of Shakespeare's sonnets.

Ken the Curator looks at Scribe, realizes it's probably not for him.

Scribe isn't about getting to the full text of a thing, it's about collecting selected elements that are relevant in a structured form. This can be ultimately for the improvement of metadata, or to create new standalone data sets [UGH].


# Features
* Framework for image-based crowdsourcing of text extraction tasks
* Workflow for designing transcription tasks
* Multi-stage workflows so users don't have to do all work in a single pass
* A library of combinable widgets for structuring transcription workflows
* User accounts [Based on third party account authentication]


## Doesn't provide
* Image hosting
* User authentication (to be provided by a third party such as Zooniverse Login or [OmniAuth](http://intridea.github.io/omniauth/))
* User Discussion Service (to be provided by a third party such as [Zooniverse Talk](https://github.com/zooniverse/Talk) or [Discourse](http://www.discourse.org/))

# Components

Scribe's architecture is deeply inspired by Zooniverse's [Panoptes](https://github.com/zooniverse/Panoptes/) / [Panoptes Frontend](https://github.com/zooniverse/Panoptes-Front-End/), their platform for self-service citizen science projects.


## Project Setup & Workflow Creation Tool
_NOTE: This is the most TBD part of the application_

A Scribe project starts with an idea: "I have a stack of images, and I'd like to get some data out of the text they contain, but there's too many of for me to go through on my own."

A scribe project starts as a stack of organized images, called **subjects**. Each *subject* is part of a *grouping*, which can be part of a *collection*.

Think of it in terms of Zooniverse's data model for [Old Weather](https://oldweather.org), which is about transcribing historical ships logs for climate data:
<table>
<tr>
<th>Classification</th> <th>Example</th>
</tr>
<tr>
<td>Collection</td> <td>WWI</td>
</tr>
<tr>
<td>Grouping</td> <td>Ship (e.g. Jamestown (1876))</td>
</tr>
<tr>
<td>Subject</td> <td>Pages of ship logs (ordered by date)</td>
</tr>
</table>

When a user comes to your Scribe project and starts working, they'll 





## Datastore & API
Once the workflow 

## Client Transcription Site
* 100% Database-driven
* Made up of reusable and style-able UI components for classification, structuring, and transcription
* Components designed for "[Composability](http://en.wikipedia.org/wiki/Composability)", the outputs from one UI element easily feed the API or other UI components

### Homepage
Projects get a homepage

### Other Client Site Features
* Login agnostic - use Zooniverse ID's, use Facebook ID's, use nothing at all. If it talks oAuth (or a dead-simple login like Zooniverse), you can use it here.
* Discussion agnostic - Very simple to jump from a task to talking about that task and that subject, using something like [Zooniverse Talk](https://github.com/zooniverse/Talk) or [Discourse](http://www.discourse.org/).

## Project Admin Tool


