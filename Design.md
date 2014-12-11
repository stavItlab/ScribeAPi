# Design Specifications
## High Level Overview
Scribe is designed to be a point-and-click configurable tool enabling scientists, librarians, and others to create text-based structured data projects from digitized documents.

## Experience Walkthrough
### Example 1
Ken the Curator has an idea for a crowdsourcing project. He wants "The Crowd" to transcribe the full text of Shakespeare's sonnets.

Ken the Curator looks at Scribe, realizes it's probably not for him.

Scribe isn't about getting to the full text of a thing, it's about collecting selected elements that are relevant in a structured form. This can be ultimately for the improvement of metadata, or to create new standalone data sets [UGH].


# Features

# Components
Scribe's architecture is deeply inspired by Zooniverse's [Panoptes](https://github.com/zooniverse/Panoptes/) / [Panoptes Frontend](https://github.com/zooniverse/Panoptes-Front-End/), their platform for self-service citizen science projects. Panoptes will ultimately provide 


## Project Setup & Workflow Creation Tool
_NOTE: This is the most TBD part of the application_

Each Project is broken down into "Tasks", the individual stages an "asset" (the image) goes through to be structured with Scribe. Tasks are "[Composable](http://en.wikipedia.org/wiki/Composability)" – the output from one task can be used to drive the input of the next task (or series of tasks). That said, many Scribe projects are likely to only have one kind of Task (e.g. back to our Menus example, transcribing the name and price of a dish on a menu).





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


