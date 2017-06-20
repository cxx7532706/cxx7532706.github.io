---
layout: post
category : AWS
tagline: "Supporting tagline"
tags : [AWS, ASP.NET, Ubuntu]
---

Deploying your app on a virtual machine on cloud is not a hard thing anymore. It is really cheap to buy a could-based server for small application. It only cost me 5 dollars a month to have a Ubuntu instance with 512 MB RAM, 20GB SSD and 512 GB data transfer on Amazon Web Service(AWS).

### How does it work on cloud server

It's just like you run your application on your local machine, you got the connection for cloud instance. Setting the environment, installing a couple of package for you application.

After all those things done, simply run you application. It will be run on `localhost:port` just like your local computer.

For now, if you open your browser, type your virtual machine address `xx.xx.xx.xx:port`, you will be able to use your app.

<img src="/assets/photos/Deploy-1.png" alt="Before" style="width: 800px; margin: 0 auto; display:block;"/>

Now, the application is run like this. However, this way is a bit unsafe, if the application crash, everything might crashing. 

So instead, we use a middleware between www and dotnet, which is Nginx.

<img src="/assets/photos/Deploy-2.png" alt="Before" style="width: 800px; margin: 0 auto; display:block;"/>

### Install Nginx

`sudo apt-get install nginx`

Then `sudo service nginx start`, to start it. You could use `systemctl status nginx.service` to check if it is running.

Modify the config file in `/etc/nginx/sites-available/default`, change it to following.

~~~
server {
    listen 80;
    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection keep-alive;
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
~~~

This will make Nginx know they are connecting from port 80 to port 5000.

Run `sudo nginx -t` to verify your config file, and then `sudo nginx -s reload` to load the new configuration.

Nginx is now setup to forward requests from `localhost:80` to `localhost:5000`. So you do not need to specify the port anymore when you run application on Virtual machine now. But you still need to manully run and restart it once it is stoped.

### Creating Linux Service

There is a way to make your Ubuntu automatically run and restart your app by adding your `project.dll` into system services.

Locate to `/etc/systemd/system/`, create a file `projectName.service` by `sudo nano projectName.service`.

~~~
[Unit]
Description=Example .NET Web API Application running on Ubuntu

[Service]
WorkingDirectory=/var/aspnetcore/project
ExecStart=/usr/bin/dotnet /var/project/project.dll
Restart=always
RestartSec=10  # Restart service after 10 seconds if dotnet service crashes
SyslogIdentifier=dotnet-example
User=www-data
Environment=ASPNETCORE_ENVIRONMENT=Production 

[Install]
WantedBy=multi-user.target
~~~

`WorkingDirectory` is the directory for your publish files.
`ExecStart`: name the file to run your app.

Save the file. run `systemctl enable projectName.service` to enable the service.

To start the service, run `systemctl start projectName.service`.

Then you application will automatically start when the cloud server is started.


