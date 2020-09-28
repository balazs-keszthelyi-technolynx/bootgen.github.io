---
title: API Documentation
type: guide
order: 100
---

<a name='assembly'></a>
# BootGen

## Contents

- [ClassModel](#T-BootGen-ClassModel 'BootGen.ClassModel')
  - [ClientProperties](#P-BootGen-ClassModel-ClientProperties 'BootGen.ClassModel.ClientProperties')
  - [CommonProperties](#P-BootGen-ClassModel-CommonProperties 'BootGen.ClassModel.CommonProperties')
  - [HasRequiredProperties](#P-BootGen-ClassModel-HasRequiredProperties 'BootGen.ClassModel.HasRequiredProperties')
  - [HasTimestamps](#P-BootGen-ClassModel-HasTimestamps 'BootGen.ClassModel.HasTimestamps')
  - [IdProperty](#P-BootGen-ClassModel-IdProperty 'BootGen.ClassModel.IdProperty')
  - [IsResource](#P-BootGen-ClassModel-IsResource 'BootGen.ClassModel.IsResource')
  - [Location](#P-BootGen-ClassModel-Location 'BootGen.ClassModel.Location')
  - [Name](#P-BootGen-ClassModel-Name 'BootGen.ClassModel.Name')
  - [Persisted](#P-BootGen-ClassModel-Persisted 'BootGen.ClassModel.Persisted')
  - [PluralName](#P-BootGen-ClassModel-PluralName 'BootGen.ClassModel.PluralName')
  - [Properties](#P-BootGen-ClassModel-Properties 'BootGen.ClassModel.Properties')
  - [ServerProperties](#P-BootGen-ClassModel-ServerProperties 'BootGen.ClassModel.ServerProperties')
  - [PropertyWithName()](#M-BootGen-ClassModel-PropertyWithName-System-String- 'BootGen.ClassModel.PropertyWithName(System.String)')

<a name='T-BootGen-ClassModel'></a>
## ClassModel `type`

##### Namespace

BootGen

##### Summary

Model of a class used in the REST API

<a name='P-BootGen-ClassModel-ClientProperties'></a>
### ClientProperties `property`

##### Summary

Properties that are visible on the client side.

<a name='P-BootGen-ClassModel-CommonProperties'></a>
### CommonProperties `property`

##### Summary

Properties that are visible on both server and client side.

<a name='P-BootGen-ClassModel-HasRequiredProperties'></a>
### HasRequiredProperties `property`

##### Summary

True if any property is required

<a name='P-BootGen-ClassModel-HasTimestamps'></a>
### HasTimestamps `property`

##### Summary

Indicates that class usescreated nd updated timestamps

<a name='P-BootGen-ClassModel-IdProperty'></a>
### IdProperty `property`

##### Summary

The property used as identifier

<a name='P-BootGen-ClassModel-IsResource'></a>
### IsResource `property`

##### Summary

True if class is used as resorce

<a name='P-BootGen-ClassModel-Location'></a>
### Location `property`

##### Summary

Determines if class is used on server, client or both

<a name='P-BootGen-ClassModel-Name'></a>
### Name `property`

##### Summary

Singular name of the class

<a name='P-BootGen-ClassModel-Persisted'></a>
### Persisted `property`

##### Summary

True if class is persisted to the database

<a name='P-BootGen-ClassModel-PluralName'></a>
### PluralName `property`

##### Summary

Plural name of the class. Use PluralNameAttribute to speciy explicitly

<a name='P-BootGen-ClassModel-Properties'></a>
### Properties `property`

##### Summary

All properties defined in class.

<a name='P-BootGen-ClassModel-ServerProperties'></a>
### ServerProperties `property`

##### Summary

Properties that are visible on the server side.

<a name='M-BootGen-ClassModel-PropertyWithName-System-String-'></a>
### PropertyWithName() `method`

##### Summary

Returns property with the given name

##### Parameters

This method has no parameters.
