---
layout: post
category : ASP.NET
tagline: "Supporting tagline"
tags : [ASP.NET]
---
{% include JB/setup %}

Today I left my big heavy windows laptop at home and tried to use macOS to code ASP.NET.

The set-up is pretty easy, just need to install `ASP.NET Core` and `VS Code` as you IDE. 

BTW, there are a couple of extensions on VS Code are really good and helpful, I installed `ASP.NET Helper`, `C#`, `C# Extensions`, `HTML CSS Support` and the most important one `ASP.NET Core Scaffolding`, this could enable you to do code first scaffolding Controller and Views just like in VS Studio! Amazing!

After set-up environment, simply locate to your work path, and then run `dotnet new mvc`, this will scaffold a mvc framework website like this.

<img src="/assets/photos/asp-net demo.png" alt="asp-net-demo" style="width: 630px;"/>

Next step is to create your own database and scaffold Controller and Views. Here I use Sqlite as the database, but you can use whatever EntityFramework supported.

1. Add EntityFramework dependencies into `project.csproj`.

~~~
<PackageReference Include="Microsoft.EntityFrameworkCore" Version="1.1.2" />
<PackageReference Include="Microsoft.EntityFrameworkCore.Sqlite" Version="1.1.2" />
<PackageReference Include="Microsoft.EntityFrameworkCore.Tools" Version="1.1.1" />
<DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="1.0.0" />
~~~

2. Create a new model in Models folder and then write down your model.

~~~
using System;

namespace tenorchem.Models
{
    public class User
    {
        public int id { get; set; }
        public string userName { get; set; }
        public string passWord { get; set; }
        public Boolean isAdmin { get; set; }
    }

}
~~~

3. Create DBContext in Models folder.

~~~
using Microsoft.EntityFrameworkCore;

namespace tenorchem.Models
{
    public class ApplicationDbContext : DbContext
    {
        public DbSet<User> Users {get; set;}

        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            optionsBuilder.UseSqlite("Filename=./TenorchemDB.db");
        }

    }
}
~~~

4. Add services in `startup.cs`

~~~
        public void ConfigureServices(IServiceCollection services)
        {
            // Add framework services.
            services.AddDbContext<ApplicationDbContext>(options => options.UseSqlite("Data Source=./TenorchemDB.db"));
            services.AddMvc();
        }
~~~
add following code into ConfigureServices, then your application knows you are using this DBContext for connecting database.
~~~ 
services.AddDbContext<ApplicationDbContext>(options => options.UseSqlite("Data Source=./TenorchemDB.db"));
~~~


5. Using `ASP.NET Core Scaffolding` to scaffold Controller and Views.

Just follow the instruction written on extension's description, and all the magic will happen.

Goto `localhost:5000/user` to check the magic, basic CRUD functions are finished!

<img src="/assets/photos/CRUD-demo-index.png" alt="index" style="width: 630px;"/>
<img src="/assets/photos/CRUD-demo-Create.png" alt="create" style="width: 630px;"/>
<img src="/assets/photos/CRUD-demo-details.png" alt="details" style="width: 630px;"/>



