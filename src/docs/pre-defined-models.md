---
title: Pre-defined Models
type: guide
order: 3
---

## Entity classes

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

You also might notice that the generated entity classes have an integer identifier. This identifier is added automatically, because the user entity is persisted into the database. We will talk later about how BootGen knows that this class needs to be persisted.

## Controller methods

The authentication method is also defines in the Generator/Models.cs file, with the following:

```csharp
class AuthenticationData
{
    public string Email { get; set; }
    public string Password { get; set; }
}

class LoginResponse
{
    public string Jwt { get; set; }
    public User User { get; set; }
}

interface Authentication
{
   LoginResponse Login(AuthenticationData data);
}
```

Because `AuthenticationData` and `LoginResponse` are simple data transfer objects (DTOs) that are not persisted in the database, their generated server side counterparts are identical to them. There is no big surprise on the client side either:

```typescript
export interface AuthenticationData {
    email: string;
    password: string;
}

export interface LoginResponse {
    jwt: string;
    user: User;
}
```

