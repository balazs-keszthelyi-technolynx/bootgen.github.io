---
title: Customization Options
type: guide
order: 6
---

## Irregular Plural Nouns

Sometimes we need to use [irregular plural nouns](https://www.grammarly.com/blog/irregular-plural-nouns/) as class name. You might for example have a class named `LogEntry`. You can specify the plural form of the name the following way:

```csharp
[PluralName("LogEntries")]
public class LogEntry {
  public DateTime Timestamp { get; set; }
  public string Message { get; set; }
}
```
You may also specify the name (and plural name) of the resource to be different than the class name:

```csharp
var logResource = api.AddResource<Log>(authenticate: true);
var logEntryResource = api.AddResource<LogEntry>(name: "Entry", pluralName: "Entries", parent: LogResource, authenticate: true);
```

In this case setting the resource name will result in the following:
 * The http path will be `logs/{id}/entries` instead of `logs/{id}/log-entries`
 * The controller will be called `LogsEntriesController` instead of `LogsLogEntriesController`
 * The service will be called `LogsEntriesService` instead of `LogsLogEntriesService`
 
 ## Custom namesfor controllers and services

If you do not like the naming convention that BootGen uses for controllers and services, or if they are against the naming policy of your company, you can set the names explicitly:

```csharp
logEntryResource.GenerationSettings.ServiceName = "LogEntriesDataService";
logEntryResource.GenerationSettings.ControllerName = "LogEntriesController";
```

## Opting out from generating certain files

The generation of the controller, service and service interface is optional. You can opt-out form generating some of these file by setting any of the following properties false:

```csharp
logEntryResource.GenerationSettings.GenerateController = false;
logEntryResource.GenerationSettings.GenerateService = false;
logEntryResource.GenerationSettings.GenerateServiceInterface = false;
```
