---
title: Creating Your Own Models
type: guide
order: 5
---

In this section we will create an example To-Do list application with BootGen. The first thing in our domain model will be the To-Do item itself:

```csharp
[HasTimestamps]
public class ToDoItem
{
    public string Title { get; set; }
    public string Description { get; set; }
    public bool IsDone { get; set; }
}
```

The `HasTimestamps` attribute on the `ToDoItem` class adds two properties to the model: a `Created` and an `Updated` timestamp.
If this attribute is set, then the default implementation of the `ToDoItemsService` will set these timestamps properties as needed.

In the `Configuration.cs` file we add this class to the API as a resource:

```csharp
internal static void AddResources(BootGenApi api)
{
    UserResource = api.AddResource<User>(isReadonly: true, authenticate: true);
    ToDoItemResource = api.AddResource<ToDoItem>(authenticate: true, parent: UserResource, parentName: "Owner");
}
```

We have set `UserResource` as parent of `ToDoItemResource`, and so we have created a One-To-Many relationship between `User` and `ToDoItem`.
The REST API we will access the To-Do items on the following path: `/users/{userId}/to-to-items`.
Naming the parent "Owner" means that the `ToDoItem` entity class will refer to the user it belongs to as "Owner".
