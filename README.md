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

I still need a better udnerstanding of nginx configuration, HTTP, networking, logs, and troubleshooting. The gola is to become more comfortable understanding how the different parts of a web server work together.

## How to Run This Project

The project was developed on Arch Linux using nginx
The nginx document root was configured as /srv/week-02-webserver/

After installing nginx and configuring the document root to point to the webpage, the service can be started using sudo systemctl start nginx

To check whether nginx is running type systemctl status nginx

The webpage can then be accessed locally at http://127.0.0.1

The repository configuration should be reviewed and adapted to the local system before use.


## HTTP Testing

I used curl to test how the web server reposnts to HTTP requests

Retrive the webpage: curl 127.0.0.1:80

Display only the HTTP response headers: curl -I 127.0.0.1:80

The server returned 200 OK, meaning that the request succeeded

I also investigated the Content-Length header, which reported 113 bytes. I verified the response body size by using: curl -s 127.0.0.1:80 | wc -c. The results was also 113 bytes.

To test how nginx handles missing resources, I used: curl -I http://127.0.0.1/doesnotexist

This returned a 404 Not Found, meaning that nginx recieved the request but couldn't find the requested resource.

## Log Analysis

I investigated the nginx access log: /var/log/nginx/access.log

To view the latest requests: tail -n 5 /var/log/nginx/access.log

To count HTTP status codes, I combined several Linux commands: awk '{print $9}' /var/log/nginx/access.log | sort | uniq -c

The pipeline works by:
1. Using awk to extract the HTTP staus codes from each log entry
2. Using sort to group identical status codes
3. Using uniq -c to count how many times each code appears

My results at the time of testing were
23 200
1 301
3 404

This hepled me understand how Linux CL-tools can be combined to investigate server activity

## Configuration and Troubleshooting

I practiced validating nginx configuration files using sudo nginx -t

I also deliberately introduced a configuration error by removing a semicolon. nginx identigied the error, allowing me to correct it before reloading the service.

During further testing, nginx reported a warn related to types_hash_max_size.

I investigated the confiration and tested different values. Increasing the setting to 4096 eliminated the warn:

types_hash_max_size 4096;

After calidating the configuration, I relaoded nginx without restarting the service.

This taught me the importance of making controlled configuration changes and testing them before applying them.

## What I Need to Improve

I want to continue developing my understanding of networking, HTTP, nginx configuration, Linux permissions, and service troubleshooting. My long-term goal is to become comfortable administrating Linux servers and eventually move into Linux system adminsitration and DevOps.

This project helped me move beyond simply running commands toward understanding how Linux services work and how to investigate problems when they occur
