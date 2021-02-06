# Deploy a web server using respberrypi

A step by step procedure on how to deploy a web server using raspberry pi.

# Getting Started

## Raspberry Pi Setup

1. Setup your hardware and use the [NOOBS][noobs] to install the Raspberry Pi OS flavor of Linux.
2. Connect to your Raspberry Pi from another machine using [SSH][ssh] or [VNC][vnc]

_If your device supports mDNS, you can reach your Raspberry Pi by using its hostname and the .local suffix_
```ping raspberrypi.local```

# Web App

1. Create a NodeJS web application that servers html and start the server.
2. Install nginx. Nginx can be used for load balancing if multiple raspberry pis are configured. (Not required for a single pi)
```
sudo apt update
sudo apt install nginx
sudo /etc/init.d/nginx start
```
3. Modify nginx default config in `/etc/nginx/sites-available` file, to redirect any request coming to root url to the nodejs file
```
location / {
    proxy_pass http://localhost:8080
}
```
4. Restart nginx
```
sudo /etc/init.d/nginx restart
```

Now we can view the web app using our internal IP on the private network

# Connect to the Internet

Internet Service Provider (ISP) usually provides us a dynamic IP, which changes on a regular basis. Some workarounds are:

- Request a static IP address from ISP.

- Use NoIP. Runs a background program that checks dynamic IP every 5 minutes, then updates the DNS when it changes.

- Use Ngrok to forward localhost to a URL.

## Port Forwarding

In case we dont want to request a static IP address from ISP, we can expose the website to internet by port forwarding request from router to raspberry pi.
Use [this][pot_fwd] site to get router specific instructions for port forwarding.

<!-- Markdown link & img dfn's -->
[noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[vnc]: https://www.raspberrypi.org/documentation/remote-access/vnc/README.md
[pot_fwd]: https://portforward.com/router.htm

