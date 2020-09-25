---
title: Introduction
type: guide
order: 1
---

## What is BootGen?

BootGen is a model based, template driven application code generator for ASP.Net Core and Vue.js.

**Model based** means that to start working on your project, first you have to create a model of your entities, resources and operations. Unlike other code generators, it is not necessary to learn separate modelling language, because BootGen models are plain C# classes and interfaces.

**Template driven** means that each piece of generated code (for example entity classes and controllers), is described by a [Scriban](https://github.com/lunet-io/scriban) template. Templates are customizable, this way you can make the generated code look consistent with the code you write by hand.

## Why Use A Code Generator?

In every software project there are interesting parts that need programmer creativity, and there are boring parts that do not. We usually have to develop the boring parts, before we can work on the interesting parts. The boring parts are repetitive, tedious and error prone. A significant amount of development time is spent on creating these parts, and also a significant amount of time is spent on finding bugs in these parts. Would not it be nice to start your next project with the boring parts already done?
