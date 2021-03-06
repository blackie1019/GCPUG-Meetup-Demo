# HelloWorld with ASP.NET Core #

## CMD ##

### Create Web MVC Project ###

    mkdir mvc
    cd mvc

    dotnet new mvc
    dotnet restore
    dotnet run

### Add Web API Project ###

    mkdir webapi
    cd webapi

    dotnet new webapi
    dotnet restore
    dotnet run

Browse [http://localhost:5000/api/values](http://localhost:5000/api/values)

### Add External Package - Swagger for Web API Project  ###

    cd webapi
    dotnet add package Swashbuckle.AspNetCore
    dotnet restore

Go to app > Startup.cs and modify:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Logging;
using Swashbuckle;
using Swashbuckle.AspNetCore.Swagger;
namespace webapi
{
    public class Startup
    {
        public Startup(IHostingEnvironment env)
        {
            var builder = new ConfigurationBuilder()
                .SetBasePath(env.ContentRootPath)
                .AddJsonFile("appsettings.json", optional: false, reloadOnChange: true)
                .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true)
                .AddEnvironmentVariables();
            Configuration = builder.Build();
        }
        public IConfigurationRoot Configuration { get; }
        // This method gets called by the runtime. Use this method to add services to the container.
        public void ConfigureServices(IServiceCollection services)
        {
            // Add framework services.
            services.AddMvc();
            services.AddSwaggerGen(c =>
            {
                c.SwaggerDoc("v1", new Info { Title = "My API", Version = "v1" });
            });
        }
        // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
        public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
        {
            loggerFactory.AddConsole(Configuration.GetSection("Logging"));
            loggerFactory.AddDebug();
            app.UseMvc();
            app.UseSwagger();
            app.UseSwaggerUI(c =>
            {
                c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
            });
        }
    }
}
```

Execute :

    dotnet run

Browse [http://localhost:5000/swagger](http://localhost:5000/swagger)