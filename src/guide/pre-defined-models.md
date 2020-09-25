---
title: Pre-defined Models
type: guide
order: 3
---

## User Entity

Entity classes are an important part of our model. As most software system has users, BootGen ships with a pre-defined `User` model. In the Generator/Models.cs file you will find the pre-defined models, the first being the User model:

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

## Controllers

The other important part of the model are the controllers. Controllers are defined with C# interfaces. There are some pre-defined controllers that are beneficary for most applications.

### Authentication

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
   [Post]
   LoginResponse Login(AuthenticationData data);
}
```
The `Post` attribute on the login method sets the HTTP verb for the controller methods. Other useable attributes are `Get`, `Put`, `Patch` and `Delete`.

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

### Registration

```csharp
class RegistrationData
{
    public string UserName { get; set; }
    public string Email { get; set; }
    public string Password { get; set; }
}

class ProfileResponse
{
    public bool Success { get; set; }
    public bool IsUserNameInUse { get; set; }
    public bool IsEmailInUse { get; set; }
}

interface Registration
{
    [Get]
    ProfileResponse CheckRegistration(RegistrationData data);
    
    [Post]
    ProfileResponse Register(RegistrationData data);
}
```
Because we are working on a single page application, users expects us to show form validation errors (like "email address is already in use") before they are actually submitting a form. We define the `CheckRegistration` method for this reason. It can check the validity of the registration form without making any changes on the server.


### Profile

```csharp
public class ChangePasswordData
{
    public string OldPassword { get; set; }
    public string NewPassword { get; set; }
}

interface Profile
{
    [Get]
    User Profile();
    
    [Get]
    ProfileResponse CheckProfile(User user);
    
    [Post]
    ProfileResponse UpdateProfile(User user);

    [Post]
    bool ChangePassword(ChangePasswordData data);
}
```

The `CheckProfile` is similar to the previously defined `CheckRegistration` method. It is used to check the validity of the profile update form before the form is actually submitted.
