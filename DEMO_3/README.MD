# ASP.NET Core with GAE - Standard Environment #

Create a new *GCP Project* and launch *Google Cloud Shell*

## ASP.NET Core 1.0.0 CLI ##

Display SDK version:

    dotnet --version

Display runtime version:

    dotnet

List Templates:

    dotnet new -t --help

## Create .NET Core 1.0 HelloWorld ##

### Step 1 ###

    mkdir app
    cd app

    dotnet new -t console
    dotnet restore
    dotnet run
### Step 2 ###

    vi Program.cs

編輯Hi, I am Blackie

    dotnet run
## GAE - Standard Env - Web ##
### Step 1 ###
    mkdir web
    cd web

    dotnet new -t web
    dotnet restore
    dotnet run

### Step 2 ###

    vi wwwroot/js/site.js

```js    
console.log("Inject Hi here");
```
    gulp clean;gulp min
    dotnet run

### Step 3 (enable Google Cloud Container Builder API)###
    
    dotnet publish --configuration Release
    cd bin/Release/netcoreapp1.0/publish/

    gcloud beta app gen-config --custom

Content:

    runtime: aspnetcore
    env: flex

Deploy:

    gcloud beta app deploy
    gcloud app browse