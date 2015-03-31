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

### User Motivation
_"I don't know *anyone* who would *actually* do this."_ –Hopefully not you

"Crowdsourcing" is an immensely broad field of practice, but it generally boils down to bringing an interested, distributed group of people to solve an organization's directed problems.

To create a successful crowdsourcing project, you not only need a well-organized set of tasks or challenges, you also need to find your "crowd".

To create the tasks, there are Crowdsourced Innovation platforms designed to run distributed challenges, there are crowdsourced microtask frameworks like [PyBossa](http://pybossa.com/), and Scribe (oh hey, hi!). But what these don't solve are the "who" of crowdsourcing. They're tools that can help you design, build, and run a project, but they aren't designed to recruit the real people - friends, family, experts, amateurs, enthusiasts, passersby - who will be working _with_ you to make your project real.

Often, this is solved in the commercial world with a very simple solution: money. Most crowdsourcing platforms marry a tool for creating crowdsourced tasks with a marketplace to pay people for performing individual tasks or large payouts for solving major challenges. As I write this, Amazon Mechanical Turk, one of the largest crowdsourcing marketplaces on the internet, is offering 276,274 "Human Intelligence Tasks" at a price between $0.00 (yes, nothing - this is a new feature), and $74.79 (for an urgent audio transcription). Most tasks are only a few cents ($0.01-$0.10) per activity. Studies have shown that the average hourly pay for someone performing these tasks is about [GAH FIND THAT STUDY].

At Zooniverse and The New York Public Library, we take a very different approach to finding motivated users: we build projects that we think will actively excite people. We want them to be excited by the broad concept.

Zooniverse puts its promise front and center:
> We make citizen science websites so that everyone can be part of real research online
No matter who you are, when you're participating in a Zooniverse project, you're actively doing real research. When you join one of its citizen science projects, you're acutely aware of how your participation is actively helping the underlying research project.

From the moment you land on the homepage of a Zoonvierse project, you're presented with:
* the core idea of the project
* what material you'll be working with
* a general sense of what you'll be doing

And it's all delivered in a way that excites participants. Galaxy Zoo promises, "Few have witnessed what you're about to see. Experience a privileged glimpse of the distant universe as observed by the SDSS, the Hubble Space Telescope, and UKIRT... To understand how galaxies formed we need your help to classify them according to their shapes. If you're quick, you may even be the first person to see the galaxies you're asked to classify." It connects with astronomy and space enthusiasts. It's designed to speak to _someone_, in this case science enthusiasts, and space enthusiasts in particular.

In business strategy speak, this is called the [value proposition](http://en.wikipedia.org/wiki/Value_proposition). What are you delivering for your users? What are they contributing to?

This approach goes deeper than just the homepage.

There are elements which will intersect with your the [design of the tasks](#task-design), [user acquisition and promotion](#promotion), and [long-term participant engagement](#engagement), but at the heart of your project you've got to ground it to the bigger goal you're trying to accomplish. What will transforming these documents into a dataset do, what will they enable, why should folks outside your organization get really excited about it? Providing a broader context for this to plug into is critical. 

As you're conceptualizing your project, consider:
* Who will actually do this?
* Is there a community that this actively speaks to?
 * How can I let them know that this effort exists, and gain their trust and interest to participate

In terms of context-setting this means giving your project some character and flavor in the design, but also what you say. Who's behind it? How are they using the data? Whats the basis behind the science? Making these things clear from the start on the homepage, and then going into significant depth in informational sections of the site is critical. On the informational sections, don't be afraid to get geeky. Take the time to really explain the rationale behind the project, the significance of the work being processed (in many cases being seen by the public for the first time). Use it as an opportunity to turn enthusiasts into evangelists.


#### Takeaways:
* Know who your community is who will be participating in the site. Make it with an intended audience in mind.
* Design the site so your value proposition is front and center. Your participants should immediately know why they're there, what they're doing, and what value will come from their efforts.


### <a name="task-design"></a>The right task for the right audience



Put yourself in the shoes of your participants 

### Testing Your Project

### Launching a crowdsourcing project

### <a name="promotion"></a> Promoting your project


### <a name ="engagement"></a>Engaging your audience

### Consistently Testing and Improving Your Project

### Sharing your data and results

### Going Further