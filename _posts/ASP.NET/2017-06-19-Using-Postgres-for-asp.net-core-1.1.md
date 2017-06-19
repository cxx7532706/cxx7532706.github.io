---
layout: post
category : ASP.NET
tagline: "Supporting tagline"
tags : [ASP.NET,Postgres]
---

Today I tried to transfer my database from sqLite3 to Postgres for my current project, so that I could deploy it on cloud server in the future.

Thanks to my previous Ruby On Rails experience, I am quite familiar with Postgres and PgAdmin. 

The setting is pretty easy and straight forward.

### Add package to your 'project.csprop'.

`<PackageReference Include="Npgsql.EntityFrameworkCore.PostgreSQL" Version="1.1.0" />`, then run `dotnet restore`.

Or this could also be done by `dotnet add package Ngsql.EntityFrameworkCore.PostgreSQL`. Choose whichever you like!

### Add ConnectionStrings in 'appsettings.json'.

Open your `appseetings.json` file, add following code.

~~~
  "ConnectionStrings": {
    "DefaultConnection":"Host=localhost;Database=tenorchem;Username=postgres;Password=postgres"
    }
~~~

Change your username and password for your postgres user.

### Configuring 'Startup.cs'.

~~~
public void ConfigureServices(IServiceCollection services)
        {
            // Add framework services.
            services.AddAuthorization(options =>
            {
                options.AddPolicy("AdminPolicy", policyBuilder =>
                {
                    policyBuilder.RequireAuthenticatedUser()
                        .RequireAssertion(context => context.User.HasClaim("Admin", "true"))
                        .Build();
                });
                options.AddPolicy("NormalPolicy", policyBuilder =>
                {
                    policyBuilder.RequireAuthenticatedUser()
                        .RequireAssertion(context => context.User.HasClaim("Normal", "true"))
                        .Build();
                });
            });
            //services.AddDbContext<ApplicationDbContext>(options => options.UseSqlite("Data Source=./TenorchemDB.db"));
            services.AddDbContext<ApplicationDbContext>(options => options.UseNpgsql(Configuration.GetConnectionString("DefaultConnection")));
            services.AddMvc();
        }
~~~

Find `ConfigureServices(IServiceCollection services)` method, add 
~~~
services.AddDbContext<ApplicationDbContext>(options => options.UseNpgsql(Configuration.GetConnectionString("DefaultConnection")));
~~~

For now, all the seeting is done.

### Run 'dotnet ef migrations add postgres' then 'dotnet ef database update'. 

<img src="/assets/photos/postgres-1.png" alt="postgres-1" style="width: 630px; margin: 0 auto; display:block;"/>

Now you can open your `pgAdmin` to check the database and tables.

<img src="/assets/photos/postgres.png" alt="postgresDemo" style="margin: 0 auto; display:block;"/>



