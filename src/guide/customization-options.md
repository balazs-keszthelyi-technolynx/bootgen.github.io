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
api.AddResource<LogEntry>(name: "Entry", pluralName: "Entries", parent: LogResource, authenticate: true);
```
