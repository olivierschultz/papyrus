---
title: "Software Documentation"
tags:
  - Software Development Life Cycle
  - Documentation
---

# Software Documentation

Three types of documentation:
1. __Written documentation__: READMEs, tutorials, reference guides, white papers
2. __Code documentation__: API docs, comments, example code, the type system
3. __Community documentation__: blog posts, Q&A sites, talks, meetup groups

## Written documentation

### README

Every project should have a README. The README is typically your first contact with a new user, so your goal is to introduce them to the project as quickly as possible, convince them why it's worth learning more, and give them pointers on how to get started and where to get more info

A typical README should have the following information:

1. __Description__: short "sales pitch". Tell the reader why they should keep reading.
2. __Quick examples__: short code snippets or screenshots to support the description.
3. __Quick start__: how to get going, install instructions, and more examples.
4. __Further documentation__: links to the full docs and more info
5. __Project organization__: who are the authors, how to contribute, how to file bugs.
6. __Legal notices__: licence, copyright, and any other legal details.

Examples of great README's:

- twitter bootstrap
- guard
- ace
- jekyll
- hogan
- ember

I usually practice Readme Driven Development, writing the README before writing any code. This forces me to be clear on exactly what I'm trying to build, helps me prioritize the work, and provide a great sanity check in what the basic user experience looks like (quick example and quick start sections are essential).

### Tutorials, walkthroughs, and guides

The README gets the user in the door; the tutorial shows them how to walk around.

For small project, simple projects, you may be able to squeeze a tutorial into the README itself, but most projects will want to use a wiki, a blog post, a standalone webpage, slide deck, or even a recorded video.

The gold standard, however, is the interactive tutorial. Most developers learn best by doing, so a step-by-step guide that lets the developer participate is the ultimate learning tool.

Example of interactive tool: codepen, codecademy

### Reference documentation

The goal of the reference documentation is to give users a way to find the specific information they need. In this part of the documentation, you can cover all the major topics in depth, but make sure to organize, but make sure to organize the information in a way that is easy to search and navigate.

### Project websites

Standalone project websites are a great exampe of documentation as marketing.

### White papers and books

If you want to make a project look legit, a white paper, and espacially a book, is the way to go. White papers are a great way to explain the background for the project: why it was built, the requirements, the approach, and the results.

## Code documentation

We now understand the role of written documentation: the README gets your goot in the door; the tutorial shows you how to walk around; the reference guide is a map. But to truly understand how a piece of software works, you have to learn to read the source. 

However the code cannot be the only documentation for a project.

### Naming, design patterns, and the type system

One of the first aspects of code readability is naming: every piece of software defines its own mini language or DSL that consists of class names, package names, method names, and variable names.

Design patterns are another tool for communicating the intent of your code.

Type system in statically typed languages can be another powerful source of information. A type system can reduce not only the number of tests you write (by catching a certain class of errors automatically), but also the documentation you have to write.

### API docs and literate programming

APIs docs are documentation for each class, function, and variable in your code. They are a fine grained form of documentation that lets you learn about the inputs and ouputs of each function, the preconditions and postconditions, and, perhaps most importantly, why a certain piece of code exists and behaves the way it does.

Example scala API docs

Literate programming goes even further: the idea is that program logic should be described first in natural language, the code comes second, interspersed amongst the English description where convenient. Instead of organizing programs in a way that's easy for compilers to process (ie, rigid file, folder, and package structure), literate programs should be organized in a way that makes it easier for humans to understand, such as an essay format.

### Comments

When used correctly, comments are another important source of information: whereas the code tells you how, comments tell your why. Always use commments in moderation and always to explain why.

### Example code and test code

Getting the example code right is critical to the success of a project, as many developers will blindly copy and paste it. Your goal is to make as many clean, idiomatic examples available as possible. 

## Community documentation

### Project management tools

Most teams use bug tracking software (github Issues, JIRA) and/or project management software (Trello). These systams contain a lot of information about the project: what you worked on before, what you're working on now, what you'll work in the future, bugs found, bugs fixed, and so on.

### Mailing lists and Q&A boards

Discussion from Q&A sites like StackOverflow or gitter and mailing lists like google groups also come up frequently in search results.

**Resources**:

- [You are what you document](https://www.ybrikman.com/writing/2014/05/05/you-are-what-you-document/)
