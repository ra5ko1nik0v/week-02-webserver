# Week 02 - Nginx Web Server

## What Is This Project?

This is my second weekly linux project while learning Arch linux. The project focused on setting up a small web sever with nginx and serving my own HTML page.

## What Have I Learned?

I learned how nginx serves files over HTTP, how systemd manages the nginx service, how to inspect listening ports and runnig processes, and how to read nginx access and error logs.

I also learned the difference between a service being active and enabled, and how to safely test configuration changes before reloading nginx.

## What Files Are Included?

The project contains:

- site/index.html - the webpage served by nginx
- nginx/nginx.conf - the nginx configuration used for this project

## How Did I Test Nginx?

I tested the server using curl and inspected access logs to see the request.

I also deliberatly broke the nginx configuration by remiving a semicolon. I used nginx -t to identify the configuration error, fixed it, tested the configuration agains, and then safely reloaded nginx.

## What Do I Need To Improve?

I still need a better udnerstanding of nginx configuration, HTTP, networking, logs, and troubleshooting. The gola is to become more comfortable understanding how the different parts of a web server work together
