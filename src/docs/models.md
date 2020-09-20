---
title: Creating Models
type: guide
order: 3
---

## Pre-defined Models

As most software system has users, BootGen ships with a pre-defined `User` model and a simple JWT authentication. In the Generator/Models.cs file you will find the pre-defined models, the first being the User model:

```csharp
class User
{
    public string UserName { get; set; }
    public string Email { get; set; }
    [ServerOnly]
    public string PasswordHash { get; set; }
}
```

Based on this model entity classes are generated on both server and client side.
On the server side the generated class is found in WebProject/User.cs:

```csharp
public class User
{
    public int Id { get; set; }
    public string UserName { get; set; }
    public string Email { get; set; }
    [JsonIgnore]
    public string PasswordHash { get; set; }
}
```
On the client side the generated TypeStript interface is found in WebProject/ClientApp/src/models/User.ts:

```typescript
export interface User {
    id: number;
    userName: string;
    email: string;
}
```

You must have noticed the `ServerOnly` attribute on the `PasswordHash` property. The effect of this property is that the password hash is missing on the
client side entity. There is also a `JsonIgnore` attribute on this property on the server side, preventing this attribute to be serialized into JSON.
