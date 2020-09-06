---
title: Introduction
type: guide
order: 1
---

## What is BootGen?

BootGen is a model based, template driven application code generator for ASP.Net Core and Vue.js.

**Model based** means that to tell the generator what to do you have to create an initial model of your application. Unlike other code generators, BootGen does not introduce a separate modelling language. BootGen models are created in the form of C# classes and interfaces, making it really easy to learn.

With the model you create BootGen can generate bot server side and client side code. When you change your model, BootGen will change every affected part of your project consistently.

**Template driven** means that a template belongs to each piece of code you generate (for example entity classes and controllers). These templates are created with [Scriban](https://github.com/lunet-io/scriban). This approach makes it easy to customize the generated code, so that the code you generate can look as if you have written it yourself.

## Why Use A Code Generator?

We are programers because we love to write code, yet we all know that in every project there are boring parts and exciting parts. We usually have to start with the boring parts, and make those work before we got to write the exciting parts. The boring parts are repetitive, tedious. The boring parts are where many mistakes are made, and to fix those mistakes is where most of the time goes. Would not it be nice to start you next project with the boring parts already done?
