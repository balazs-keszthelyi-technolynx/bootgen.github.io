---
title: Configuration
type: guide
order: 4
---

## Creating Resources

Besides creating a model, an other important job is, to create a configuration. This will instruct the code generator how to use the created models.

If we look into the `Generator/Configuration.cs` file, we will see that the `User` class is added to the API as a REST resource:

```csharp
private static Resource UserResource { get; set; }

internal static void AddResources(BootGenApi api)
{
    UserResource = api.AddResource<User>(isReadonly: true, authenticate: true);
}
```

Because resources are stored in the database, the `User` class will get an integer identifier. The resource is set to readonly, as the registration and the profile data modification are not handled by the user resource controller.
The authentication parameter means, that the user have to be logged in to query the list of users.

For this resource the following files are generated:
 * [UsersController.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Controllers/UsersController.cs)
 * [IUsersService.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Services/IUsersService.cs)
 * [UsersService.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Services/UsersService.cs)

The business logic is implemented in the `UsersService`. A default implementation is provided by BootGen, which is adequate for simple use cases. However, if you wish to implement your own `UsersService` you can opt-out from the generation of this file with the following:

```csharp
UserResource.GenerationSettings.GenerateService = false;
```

## Creating Controllers

A little bellow the controllers are registered:

```csharp
internal static void AddControllers(BootGenApi api)
{
    api.AddController<Authentication>();
    api.AddController<Registration>();
    api.AddController<Profile>(authenticate: true);
}
```
Classes that we have defined in the `Model.cs` file and are only referred to (directly or indirectly) by the controller interfaces, but not the resources are handled as simple DTO classes. This means that they will not be persisted in the database, and will not get a generated identifier.

For the controllers the following files are generated:
 * [AuthenticationController.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Controllers/AuthenticationController.cs)
 * [IAuthenticationService.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Services/IAuthenticationService.cs)
 * [RegistrationController.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Controllers/AuthenticationController.cs)
 * [IRegistrationService.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Services/IAuthenticationService.cs)
 * [ProfileController.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Controllers/AuthenticationController.cs)
 * [IProfileService.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Services/IAuthenticationService.cs)

## Database Seeds

We can also supply sample initial data for our application. The following code adds three test users:

```csharp
internal static void AddSeeds(SeedDataStore seedStore)
{
    seedStore.Add(UserResource, new List<User>{
        new User {
            UserName = "Sample User",
            Email = "example@email.com",
            PasswordHash = "AQAAAAEAACcQAAAAEL//UdrNeiFjd0hYeQEBOtAN+OXME8tu8kNMTg4wZUrBSt1/t0Okfs389I82ZaIU2Q==" //password123
        },
        new User {
            UserName = "Sample User 2",
            Email = "example2@email.com",
            PasswordHash = "AQAAAAEAACcQAAAAENZt+JlnUq5Ukt83M//z8Y/GlXWwYj6d260pmjQEz3Usac29eNfhmZTXHCGVOz70Hg==" //password123
        },
        new User {
            UserName = "Sample User",
            Email = "example3@email.com",
            PasswordHash = "AQAAAAEAACcQAAAAENffyhoiBzkUXycLNzvQOYJJGCXsXw+7U2ZL1ED+kCFCnDmL4yGGQT7Xkr4ZaNV8/A==" //password123
        }
    });
}
```
