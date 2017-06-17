---
layout: post
category : ASP.NET
tagline: "Supporting tagline"
tags : [ASP.NET,authentication,authorization,claim-based]
---

This tutorial will teach you how to use your own database user table to do authentication in cookies, then use claim-based authorization to control security permission.

### Add denpendicies into `projefct.csproj`

After creating a new project or use your current project, add following denpendencies into your `.csproj` file.

~~~
<PackageReference Include="Microsoft.AspNetCore.Authentication" Version="1.1.2" />
<PackageReference Include="Microsoft.AspNetCore.Authentication.Cookies" Version="1.1.2" />
~~~

you could do that by using command `dotnet add package PACKAGENAME` if you are coding in MacOS.

### Setting in `Startup.cs`

Find your `public IConfigurationRoot Configuration { get; }` method, add following codes.

~~~
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
~~~

This will add your authorization service into the application. As showed above, I have two different user roles, one is "admin" represents administrator, and the other one is "normal" represents normal user. These two different policies will help us differ the different permissions to some methods, we'll talk about that later in this article, and for policies/roles, you could add as many as you need.

`.RequireAssertion(context => context.User.HasClaim("Admin", "true"))` this tells the services if a user has claim("Admin","true"), then this user holds "AdminPolicy".

Add following codes in `public void Configure()` method before `app.UseMvc()`.

~~~
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    AuthenticationScheme = "Cookies",
    LoginPath = new PathString("/User/Login"),
    AccessDeniedPath = new PathString("/Home/PermissionDenied"),
    AutomaticAuthenticate = true,
    AutomaticChallenge = true
});
~~~

* `AuthenicationScheme` is the name of your authentication, you could name it whatever you want.

* `LoginPath` is the path for login page, when a unlogged_in user want to view pages need to be logged in, this page will be redirected to.

* `AccessDeniedPath` is the path for showing permission denied, will be redirected to when a logged_in user tring to view pages he/she doesn't have permission to.

* `AutomaticAuthenticate` is a flag indicates this middleware run on every request.

* `AutomaticChallenge` is a flag indicates the middleware will direct to `LoginPath` or `AccesDeniedPath` when authorization fails. 

### Add login logic in Controller.

First add a simple View for submit user_id and password.

~~~
<form asp-action="Login">
    <div class="form-horizontal">
        <hr />
        <div asp-validation-summary="ModelOnly" class="text-danger"></div>
        <div class="form-group">
            <label asp-for="id" class="col-md-2 control-label">Id</label>
            <div class="col-md-10">
                <input asp-for="id" class="form-control" />
                <span asp-validation-for="id" class="text-danger"></span>
            </div>
        </div>
        <div class="form-group">
            <label asp-for="passWord" class="col-md-2 control-label">Password</label>
            <div class="col-md-10">
                <input type="password" asp-for="passWord" class="form-control" />
                <span asp-validation-for="passWord" class="text-danger"></span>
            </div>
        </div>
        <div class="form-group">
            <div class="col-md-offset-2 col-md-10">
                <input type="submit" value="submit" class="btn btn-default" />
            </div>
        </div>
    </div>
</form>
~~~

Then receive the user_id and password in Controller.

~~~
public IActionResult Login(){

    return View();
}

[HttpPost]
public async Task<IActionResult> Login(int id, string passWord){
    // Select User from database.
    var user = await _context.Users.SingleOrDefaultAsync(m => (m.id == id));
    // if user exist, create authenticate in cookie.
    if (user.passWord == passWord)
    {
        if (user.isAdmin){
            var claims = new List<Claim>
            {
                new Claim("Admin", "true"),
                new Claim(ClaimTypes.Name, "admin"),
                new Claim(ClaimTypes.Sid, user.id.ToString())
            };
            var claimsIdentity = new ClaimsIdentity(claims, "Admin");
            var claimsPrinciple = new ClaimsPrincipal(claimsIdentity);
            await HttpContext.Authentication.SignInAsync("Cookies", claimsPrinciple,
                new AuthenticationProperties
                {
                    IsPersistent = true
                }
            );
            return Redirect("/Home/index");
        }
        else{
            var claims = new List<Claim>
            {
                new Claim("Normal", "true"),
                new Claim(ClaimTypes.Name, "normal"),
                new Claim(ClaimTypes.Sid, user.id.ToString())
            };
            var claimsIdentity = new ClaimsIdentity(claims, "Normal");
            var claimsPrinciple = new ClaimsPrincipal(claimsIdentity);
            await HttpContext.Authentication.SignInAsync("Cookies", claimsPrinciple,
                new AuthenticationProperties
                {
                    IsPersistent = true
                }
            );
            return Redirect("/Home/index");
        }

    }
    return Redirect("/User/Login?Pass=0");
}
~~~

The codes above will first get the user_id and password from form. Then retrieve the user from database, if password is correct, create user athentication based on user roles.

* `IsPersistent` is a flag indicates authentication will be destroied once the browser is closed. Could also add `ExpiresUtc` to indicate experies time. For example `ExpiresUtc = DateTime.UtcNow.AddMinutes(20)` this indicates authentication will be destoried after 20 mins.

You could store whatever you want in cookie by adding new Claim, and this information could be retrieved anytime later once authentication is created. The way to retrieve is by `HttpContext.User.Identity`, which is really powerful when you are dealing with default layout `_layout` change based on authorization.

### Destroy authentication after user logged out.

~~~
public async Task<IActionResult> Logout(){

    await HttpContext.Authentication.SignOutAsync("Cookies");
    return Redirect("/User/Login");
}
~~~

Simply use `await HttpContext.Authentication.SignOutAsync("Cookies");` to destroy the authentication.

### Authorize Controller

To set permissions to Controller or some methods inside Controller. Simply add `[Authorize]` above the Controller/method.

~~~
[Authorize(Policy = "AdminPolicy")]
public IActionResult VacationBalance()
{
    return View();
}
~~~





