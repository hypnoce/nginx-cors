# nginx-cors
Dockerized NGINX web server allowing Cross Origin Resource Sharing ([CORS](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing))

## Problem
Have you loaded your web app from one location and are trying to request resources from another origin?
If that origin does not respond appropriately to the browser's preflight OPTIONS request, then your browser will block the call.
You could fix this issue by having those services respond correctly - but what if you do not own them?
What if you only want to activate them in development without adding additional code?

## Solution
In order to work around this we have configured an NGINX server to intercept all OPTIONS calls and return the appropriate response allowing CORS from all origins.
Reverse proxying your service through this NGINX should solve your issue.
You could also place this NGINX in a Traefik set up and route all OPTIONS requests to it therefore only requiring one instance for all your services.


## Implementation

We pull the light Alpine based docker image of NGINX and decorate it with CORS configuration.

## How to use it
Clone this repo and `cd` into it.   
`docker build . -t nginx-cors` to create the image.  
`docker run -d -p 8080:8080 nginx-cors` to run it exposing the `8080` port on the host.  
Of course you could also run this in your k8s cluster.  

The running instance on its own with our configuration is not of great use - you will have to either enrich the configuration with your services in order to reverse proxy them through NGINX or your could drop it along side them in a Traefik instance.

##### TODO:  
[ ] Explain how this would be configured in Traefik  
[ ] Explain how this would run in K8s  

Enjoy.
