---
title: Configuration
type: guide
order: 4
---

## Creating Resources

Besides creating a model, an other important job is, to create a configuration. This will instruct the code generator how to use the created models.

If we look into the Generator/Configuration.cs file, we will see that the `User` class is added to the API as a REST resource:

```csharp
private static Resource UserResource { get; set; }

internal static void AddResources(BootGenApi api)
{
    UserResource = api.AddResource<User>("User", isReadonly: true, authenticate: true);
}
```

Because resources are stored in the database, the `User` class will get an integer identifier. The resource is set to readonly, as the registration and the profile data modification is not handled buy te user resource controller. For this resource the following files are generated:
 * [UsersController.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Controllers/UsersController.cs)
 * [IUsersService.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Services/IUsersService.cs)
 * [UsersService.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Services/UsersService.cs)

## Creating Controllers

A little bellow the `Authentication` interface is added as a controller:

```csharp
internal static void AddControllers(BootGenApi api)
{
    api.AddController<Authentication>();
}
```

As `AuthenticationData` and `LoginResponse` classes are not referred to elsewhere BootGen will handle them as simple DTOs. For this controller the following files are generated:
 * [AuthenticationController.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Controllers/AuthenticationController.cs)
 * [IAuthenticationService.cs](https://github.com/BootGen/BootGenVue/blob/master/WebProject/Services/IAuthenticationService.cs)

## Database Seeds

We can also supply sample initial data for our application. The following code adds three test users:

```csharp
internal static void AddSeeds(SeedDataStore seedStore)
{
    seedStore.Add(UserResource, new List<User>{
        new User{
            UserName = "Sample User",
            Email = "example@email.com",
            PasswordHash = "AQAAAAEAACcQAAAAEL//UdrNeiFjd0hYeQEBOtAN+OXME8tu8kNMTg4wZUrBSt1/t0Okfs389I82ZaIU2Q==" //password123
        },
        new User{
            UserName = "Sample User 2",
            Email = "example2@email.com",
            PasswordHash = "AQAAAAEAACcQAAAAENZt+JlnUq5Ukt83M//z8Y/GlXWwYj6d260pmjQEz3Usac29eNfhmZTXHCGVOz70Hg==" //password123
        },
        new User{
            UserName = "Sample User",
            Email = "example3@email.com",
            PasswordHash = "AQAAAAEAACcQAAAAENffyhoiBzkUXycLNzvQOYJJGCXsXw+7U2ZL1ED+kCFCnDmL4yGGQT7Xkr4ZaNV8/A==" //password123
        }
    });
}
```
