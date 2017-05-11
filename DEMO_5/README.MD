# ASP.NET Core with GAE - Flex Environment #

## GAE - Flex Env - Web  ##

    touch Dockerfile

Content:

    FROM microsoft/dotnet:1.1.1-runtime
    COPY . /app
    WORKDIR /app

    EXPOSE 8080/tcp
    ENV ASPNETCORE_URLS http://*:8080

    ENTRYPOINT ["dotnet", "GAENetCoreApp.dll"]

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

Setup gcloud SDK account:

    gcloud config configurations list
    gcloud config configurations activate <YOUR_CONFIG>

    gcloud config set account blackie1019@gmail.com
    gcloud config set project gcpug-tw-meetup

Deploy:

    gcloud app deploy