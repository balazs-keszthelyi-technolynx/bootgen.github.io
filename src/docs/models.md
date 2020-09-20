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

You also might notice that the generated entity classes have an integer identifier. This identifier is added automatically, because the user entity is persisted into the database. We will talk later about how BootGen knows that this class needs to be persisted.

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

We can understand how BootGen knows that the `User` class is supposed to be stored in the database, but `AuthenticationData` and `LoginResponse` not, if we look into the Generator/Configuration.cs file:

```csharp
private static Resource UserResource { get; set; }

internal static void AddResources(BootGenApi api)
{
    UserResource = api.AddResource<User>("User", isReadonly: true, authenticate: true);
}

internal static void AddControllers(BootGenApi api)
{
    api.AddController<Authentication>();
}
```

We can see that `User` is added to the API as a REST resource. Because resources are stored in the database, the `User` class will get an integer identifier. The resource is set to readonly, as the registration and the profile data modification is not handled buy te user resource controller. For this resource the following files are generated:
 * [UsersController.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Controllers/UsersController.cs)
 * [IUsersService.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Services/IUsersService.cs)
 * [UsersService.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Services/UsersService.cs)

The `Authentication` interface is added as a controller. As `AuthenticationData` and `LoginResponse` classes are not referred to elsewhere BootGen will handle them as simple DTOs. For this controller the following files are generated:
 * [AuthenticationController.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Controllers/AuthenticationController.cs)
 * [IAuthenticationService.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Services/IAuthenticationService.cs)
