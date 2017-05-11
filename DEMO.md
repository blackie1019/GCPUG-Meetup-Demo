# General #

## Google Cloud SDK ##
./google-cloud-sdk/bin/gcloud init

## ASP.NET Core 1.0.0 ##

    dotnet --version
    dotnet new -t --help

## ASP.NET Core 1.1.0 ##

## GAE - Standard Env - Console ##
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
    
    ls
    
    vi wwwroot/js/site.js
    
編輯console.log("Inject Hi here");

### Step 3 (enable Google Cloud Container Builder API)###
    dotnet publish --configuration Release
    cd bin/Release/netcoreapp1.0/publish/
    touch Dockerfile

FROM microsoft/dotnet:1.0.3-runtime

COPY . /web
WORKDIR /app

EXPOSE 8080/tcp
ENV ASPNETCORE_URLS http://*:8080

ENTRYPOINT ["dotnet", "web.dll"]

    gcloud beta app gen-config --custom

runtime: aspnetcore
env: flex

    gcloud beta app deploy
    
    gcloud app browse

## GAE - Flex Env - Web ##

    gcloud config configurations list

    gcloud config configurations activate <YOUR_CONFIG>

    gcloud config set account blackie1019@gmail.com
    gcloud config set project gcpug-tw-meetup

service: netcore-latest-version
runtime: custom
env: flex
automatic_scaling:
min_num_instances: 1
max_num_instances: 3
cool_down_period_sec: 60 # default value
cpu_utilization:
target_utilization: 0.5

    gcloud app deploy