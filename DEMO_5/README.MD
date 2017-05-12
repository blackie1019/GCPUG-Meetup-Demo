# ASP.NET Core with GAE - Flexible Environment and Custom Runtime #

    touch Dockerfile

- [gcloud shell] ASP.NET Core Runtime 1.0.1 Content:

        FROM microsoft/dotnet:1.0.1-runtime
        COPY . /app
        WORKDIR /app

        EXPOSE 8080/tcp
        ENV ASPNETCORE_URLS http://*:8080

        ENTRYPOINT ["dotnet", "web.dll"]

- [Local] ASP.NET Core Runtime 1.1.1 Content:

        FROM microsoft/dotnet:1.1.1-runtime
        COPY . /app
        WORKDIR /app

        EXPOSE 8080/tcp
        ENV ASPNETCORE_URLS http://*:8080

        ENTRYPOINT ["dotnet", "app.dll"]

Modify:

    vi app.yaml

Content:

    service: default
    runtime: custom
    env: flex
    automatic_scaling:
    min_num_instances: 1
    max_num_instances: 3
    cool_down_period_sec: 60 # default value
    cpu_utilization:
    target_utilization: 0.5

## Google Cloud SDK ##

- Download [CLOUD SDK](https://cloud.google.com/sdk/) 
- Init CMD:

    ./google-cloud-sdk/bin/gcloud init

- Version Check:

    gcloud -v

- Config Info:

### Setup gcloud SDK account ###

    gcloud config configurations list
    gcloud config configurations create gcpug-tw-meetup
    gcloud config configurations list
    gcloud config configurations activate gcpug-tw-meetup

    gcloud config set account blackie1019@gmail.com
    gcloud config set project gcpug-tw-meetup

### Deploy ###

    gcloud app deploy