Nginx TLS Tunnel: Forwarding Traffic from Iranian Server to External VPS

This guide explains how to tunnel TLS traffic from an Iranian server to a foreign VPS using Nginx's stream module. This setup allows the use of a "dirty" external IP by proxying through the Iranian server, with Cloudflare's help.

Requirements

Iranian VPS with Ubuntu/Debian

External VPS with service running on port 443

Domain added to Cloudflare DNS with proxy (orange cloud) enabled

Step 1: Update and Install Nginx

Run the following commands on the Iranian server:

sudo apt update
sudo apt install nginx

Step 2: Create Stream Configuration Directory

sudo mkdir /etc/nginx/streams-enabled

Step 3: Create the Stream Proxy File

Open a file using nano:

nano /etc/nginx/streams-enabled/ssl-passthrough.conf

Paste the following configuration:

stream {
    server {
        listen 443;
        proxy_pass domain-kharej-proxy-on:443;
    }
}

Replace domain-kharej-proxy-on with the domain of your external VPS that you've proxied through Cloudflare.

Save and exit the file:

Press Ctrl + X

Press Y to confirm

Press Enter to save

Step 4: Include the Stream Config in Nginx

Run the following command to include the new stream directory:

sudo sh -c 'echo "include /etc/nginx/streams-enabled/*;" >> /etc/nginx/nginx.conf'

Step 5: Restart Nginx

Apply the changes:
