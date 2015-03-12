# Getting Started With Scribe, A Guide

So you have decided to start a Scribe project. After reading this guide, you will know:

* [The anatomy of a Scribe project](#anatomy)
* [How to create a new Scribe project](#create)
* [The best practices for starting, promoting, and maintaining a crowdsourcing project](#best-practices)

*[TODO: break up large sections into individual/wiki pages]*

## Am I in the right place?

Before we get started, make sure you say *"yes"* to all of the following:

1. You have a collection of digital images that you'd like to extract information from, but you don't have the resources to do so yourself.
2. You are *not* looking for full text transcription of your images; rather, you would like to collect specfic partial text or metadata from your images.
3. You or a member of your team has basic web development experience, specifically with creating a [Rails](http://rubyonrails.org/) web application.

## <a name="anatomy"></a>The Anatomy of a Scribe project

In this guide, we will reference a number of crowdsourcing concepts and use a lot of Scribe lingo. Here's a brief primer on crowdsourcing concepts and how they are implemented in a Scribe project.

*[TODO: Add supporting visuals for each example]*

### Subjects

A **subject** is a uniquely identifiable image that you will ask users to perform a task on. Here are some examples:

* A **single page** in a diary
* A **single photograph** in a scrapbook
* A **single record** in an account book

### Groups

A **group** organizes subjects into related sets. Typically groups are created based on similarity of subject content or format. This is mostly to help the project creator organize, maintain, and present the project's subjects. Users perform tasks on individual subjects, not on groups. Here are some examples:

* A collection of diaries may be grouped into **Ann's 2012 Diary**, **Bob's 2013 Diary**, and **Cathy's 2014 Diary**
* An account book may be grouped into **Index pages**, **Main section**, and **Appendix**

### Classifications

A **classification** is a record of a user's response to a given task performed on a subject. Here are some examples:

* A user marks **where the date is written** in a page of a diary.
* A user indicates **whether or not a person is present** in a photograph.
* A user transcribes **the name of a person** listed on a single record in an account book.

### Workflows

A **workflow** represents a series of ordered or unordered tasks to be performed on a set of subjects. Here are some examples:

* A workflow for extracting dates from a diary:
  1. A user **marks** where the date is written in a page of a diary.
  2. A user **transcribes** the date that was marked
  3. Another user **verifies** that the date is accurate
* A workflow for classifying photographs
  1. A user **indicates** whether or not a person is present in a photograph.
  2. For a photograph with a person present, a user **inputs** how many people are present

### Tasks

A **task** is an action your ask a user to perform on a subject. Here are some examples:

* A user **marks** where the date is written in a page of a diary.
* A user **indicates** whether or not a person is present in a photograph.
* A user **transcribes** the name of a person listed on a single record in an account book.
* A user **verifies** that another user's transcription is correct.

## <a name="create"></a> Creating a new Scribe project

### I. Start with an idea

Typically, you start with a collection of images and you would like to get some data out of the content they contain, but there's too many to go through on your own. Imagine what you would ask a stranger, who has no familiarity with your collection, to do to get that data. Keep it simple as possible. Scribe works best when users are asked to perform clear and simple tasks. A very complex task can usually be broken into multiple simple sub-tasks.

Let's say that you wanted to transcribe all the names of people, places, and dates in a collection of diaries. Instead of asking a user to perform all those tasks at once, you may approach the problem as follows:

1. A user is shown a page of the diary and asked to mark any mentions of people, places, or dates.
2. The same or another user is asked to transcribe the names of the people, places, or dates that are marked.
3. Another user is shown those transcriptions and asked if they are correct or need to be fixed.

By breaking up the bigger task into smaller ones, you can have multiple users working concurrently on different parts of your collection. One user can focus on marking, another on transcription, and another on verification. Additionally, you can have multiple people transcribing the same mark, which can increase your confidence in the accuracy of the transcriptions.

### II. Choose and prepare your images

#### The right type of image collection

The ideal image collection candidate has the following traits:

1. **Unambiguous** - If you generally know what the images contain and what you're looking for, you can craft clear and concise tasks for your users.
2. **Consistently formatted** - Consistent image sizes, dimensions, and layouts will enable simpler and more intuitive interfaces for your users.
3. **Composite, nonsequential** - The images are related, but users can perform tasks on a single image independently from any others. This allows users to focus on a single subject and task at a time and freely switch between subjects and tasks.
4. **Single Subjects** - Each image should contain one subject. This will greatly simplify the interface for your users.
5. **High resolution** - This is especially important if legibility of text or details may be in issue.

#### Image processing resources

Sometimes you will need to preprocess your images to make their format or layout simpler or more consistent. Here are some resources that may help:

*[TODO: Link to tools]*

* De-skewer - for removing skew from images
* Auto-cropper - for removing unnecessary borders or margins from images
* Image splitter - for extracting multiple subjects from images

#### Image hosting

Scribe currently does not provide image hosting, so you will have to host the images yourself. Here are some resources:

*[TODO: Link to image hosting]*

### III. Set up your project

Too big, created separate page [here](Set-up-your-project).

## <a name="best-practices"></a> Crowdsourcing Best Practices

In terms of a web platform, crowdsourcing is a relatively new and evolving concept. Scribe is an even newer tool and is constantly evolving. As the creators of this tool, [Zooniverse](https://www.zooniverse.org/) and [NYPL Labs](http://www.nypl.org/collections/labs), we have been experimenting with crowdsourcing data from science to humanities projects alike. We'd like to share with you what we've learned so far.

### The right task for the right audience

### Launching a crowdsourcing project

### Promoting your project

### Engaging your audience

### Sharing your data and results


