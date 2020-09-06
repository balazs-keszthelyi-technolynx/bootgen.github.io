---
title: Installation
type: guide
order: 2
---

The suggested way to start developing with BootGen is to clone or fork the [template project](https://github.com/BootGen/BootGenVue) on GitHub.

In the repository you will see two folders: WebProject and Generator. In the WebProject folder there is an ASP.Net Core application. In WebProject/ClientApp there is a Vue.js application.

To run the project, first build the Vue.js application, then run the server:
```sh
cd ClientApp
npm install
npm run build
cd ..
dotnet restore
dotnet run
```

Now if you navigate to https://localhost:5001 you will see the default Vue.js application.

While working with this template you might also run the server and the client separately, by running the `dotnet run` command in the WebProject and the `npm run serve` in the WebProject/ClientApp folder.
