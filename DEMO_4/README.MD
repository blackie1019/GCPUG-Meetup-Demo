# ASP.NET Core with Container #

## Create New MVC Project ##

    mkdir app;
    cd app;
    dotnet new mvc;
    dotnet restore;
    dotnet run;

    dotnet publish -c Release;

    cd bin/Release/netcoreapp1.1/publish;
    touch Dockerfile;
    vi Dockerfile

Content:

    FROM microsoft/dotnet:1.1.1-runtime
    COPY . /app
    WORKDIR /app

    EXPOSE 8080/tcp
    ENV ASPNETCORE_URLS http://*:8080

    ENTRYPOINT ["dotnet", "app.dll"]

Create Image and Run:

    docker build -t blackie1019/gcpugdemo:local .
    docker run -d -p 8080:8080 -t blackie1019/gcpugdemo:local