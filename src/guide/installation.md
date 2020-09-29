---
title: Installation
type: guide
order: 2
---
## Prerequisites

To use this toolkit make sure that you have the following installed:
 * .Net Core 3.1 https://dotnet.microsoft.com/download
 * An up-to-date version of Node.js https://nodejs.org/
 * Entity Framework Core command line interface. You can install this with the following command: <br>
   `dotnet tool install --global dotnet-ef`
 * It is also recommended to install Vue.js devtools for [Chrome](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=en) or [Firefox](https://addons.mozilla.org/en-US/firefox/addon/vue-js-devtools/)

## Get BootGen From GitHub

The recommended way to start developing with BootGen is to clone or fork the [template project](https://github.com/BootGen/BootGenVue) on GitHub.

In the repository you will see two folders: `WebProject` and `Generator`. In the WebProject folder there is an ASP.Net Core application. In `WebProject/ClientApp` there is a Vue.js application. The `Generator` folder contains the models and templates for code generation. 

## Start the Application

To bring the application alive, we first have to initialize the database. By default we use an SQLite database, but of course you can change this later. To initialize the database run the following two commands:

```sh
dotnet ef migrations add InitialCreate
dotnet ef database update
```

To run the project, first build the Vue.js application, then run the server:
```sh
cd ClientApp
npm install
npm run build
cd ..
dotnet restore
dotnet run
```

Now if you navigate to https://localhost:5001 you will see a login screen.

While working with this template you might also run the server and the client separately, by running the `dotnet run` command in the WebProject and the `npm run serve` in the WebProject/ClientApp folder.
