
# SETUP SSL

## Generate SSL certificate using certbot

```sh
# Update package list to get latest package information
sudo apt update

# Install required dependencies:
# - python3: Python 3 interpreter needed for Certbot
# - python3-venv: Virtual environment module to create isolated Python environment
# - libaugeas0: Augeas library used by Certbot for configuration file parsing
sudo apt install python3 python3-venv libaugeas0

# Create a Python virtual environment at /opt/certbot/
# This isolates Certbot and its dependencies from system Python packages
sudo python3 -m venv /opt/certbot/

# Upgrade pip (Python package installer) to the latest version in the virtual environment
sudo /opt/certbot/bin/pip install --upgrade pip

# Install Certbot and the nginx plugin:
# - certbot: The Let's Encrypt client tool for obtaining SSL certificates
# - certbot-nginx: Plugin that allows Certbot to automatically configure nginx
sudo /opt/certbot/bin/pip install certbot certbot-nginx

# Create a symbolic link to make certbot command available system-wide
# This allows you to run 'certbot' from anywhere without specifying the full path
sudo ln -s /opt/certbot/bin/certbot /usr/bin/certbot

# Obtain SSL certificate using standalone mode:
# - certonly: Only obtain certificate, don't install it automatically
# - --standalone: Run a temporary web server for domain validation (requires port 80 to be free)
# - -d: Specify domain names to include in the certificate (replace example.com with your actual domain)
# Note: Replace 'example.com' and 'admin.example.com' with your actual domain names
# 
# IMPORTANT: If you don't have a domain yet, see alternatives below
sudo certbot certonly --standalone -d example.com -d admin.example.com

# Copy the full certificate chain (certificate + intermediate CA certificates)
# Location: /etc/letsencrypt/live/example.com/fullchain.pem
# Note: Replace '/path/to/your/destination/' with your actual destination directory
sudo cp /etc/letsencrypt/live/example.com/fullchain.pem /path/to/your/destination/

# Copy the private key (keep this secure and restrict file permissions!)
# Location: /etc/letsencrypt/live/example.com/privkey.pem
# Note: Replace '/path/to/your/destination/' with your actual destination directory
sudo cp /etc/letsencrypt/live/example.com/privkey.pem /path/to/your/destination/
```

## What if I don't have a domain yet?

If you don't have a registered domain name, you have several options:

### Option 1: Self-Signed Certificate (Development/Testing Only)

For local development or testing, you can generate a self-signed certificate:

```bash
# Install openssl if not already installed
sudo apt install openssl

# Generate a self-signed certificate valid for 365 days
# This will create both the certificate and private key
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /path/to/privkey.pem \
  -out /path/to/fullchain.pem \
  -subj "/C=US/ST=State/L=City/O=Organization/CN=localhost"

# Set appropriate permissions for the private key
sudo chmod 600 /path/to/privkey.pem
```

**Note:** Browsers will show a security warning for self-signed certificates. This is normal and expected - you can proceed by accepting the exception. **Never use self-signed certificates in production.**

### Option 2: Get a Free Domain

Several services offer free domains or subdomains:

- **Freenom** (`.tk`, `.ml`, `.ga`, `.cf` domains) - Free for first year
- **No-IP** - Free dynamic DNS hostnames
- **DuckDNS** - Free dynamic DNS service
- **Cloudflare** - Free domain registration (limited TLDs)

Once you have a domain, point it to your server's IP address using DNS A records, then use the Certbot commands above.

### Option 3: Use a Testing Service (Temporary)

For temporary testing, you can use services that provide SSL-enabled tunnels:

- **ngrok** - Creates secure tunnels to localhost with HTTPS
- **Cloudflare Tunnel** - Free secure tunnel service
- **localtunnel** - Open source alternative

These services give you a temporary HTTPS URL without needing your own domain.

### Option 4: Use IP Address (Limited)

**Let's Encrypt does NOT issue certificates for IP addresses** - you must have a domain name. However, for local development, you can:

1. Add an entry to `/etc/hosts` on your local machine:
   ```
   127.0.0.1 myapp.local
   ```
2. Use a self-signed certificate with `CN=myapp.local` (see Option 1)

### Recommendation

- **For Production:** Get a real domain (even a free one) and use Let's Encrypt
- **For Development:** Use self-signed certificates or localhost
- **For Testing:** Use ngrok or similar tunneling services


## Options

```sh
# options
echo "0 0,12 * * * root /opt/certbot/bin/certbot renew --quiet" | sudo tee -a /etc/crontab
```

## Example mapping to nginx

```yaml
services:
    nginx.webserver:
        image: nginx:stable
        ports:
        - "80:80"
        - "443:443"
        volumes:
        - ./nginx.fe.conf:/etc/nginx/nginx.conf
        - /etc/letsencrypt:/etc/letsencrypt:ro
        depends_on:
        - client.web
        networks:
        - client-network
    
    client.web:
        build:
            context: ./Client
            dockerfile: Dockerfile
        ports:
        - "3000:3000"
        networks:
        - client-network

    admin.web:
        build:
            context: ./Admin
            dockerfile: Dockerfile
        ports:
        - "4000:3000"
        networks:
        - client-network

networks:
  client-network:
    name: client-network
    driver: bridge
```

## Example nginx.conf
```conf
events {

}

http {
    # HTTP to HTTPS redirection
    server {
        listen 80;
        listen [::]:80;
        server_name ybzone.io.vn admin.ybzone.io.vn;

        # Redirect all HTTP traffic to HTTPS
        return 301 https://$host$request_uri;
    }

    # Main server block for ybzone.io.vn
    server {
        listen 443 ssl; 
        listen [::]:443 ssl;
        server_name ybzone.io.vn;

        ssl_certificate /etc/letsencrypt/live/ybzone.io.vn/fullchain.pem; # Path to your self-signed certificate
        ssl_certificate_key /etc/letsencrypt/live/ybzone.io.vn/privkey.pem; # Path to your self-signed certificate key

        # Optional: Add SSL settings for better security
        # l_protocols TLSv1.2 TLSv1.3;
        # ssl_prefer_server_ciphers on;
        # ssl_ciphers EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH;
        # ssl_session_cache shared:SSL:10m;
        # ssl_session_timeout 1d;
        # ssl_session_tickets off;

        location / {
            proxy_pass http://client.web:3000;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }

    # Server block for admin.ybzone.io.vn
    server {
        listen 443 ssl; 
        listen [::]:443 ssl;
        server_name admin.ybzone.io.vn;

        ssl_certificate /etc/letsencrypt/live/ybzone.io.vn/fullchain.pem; # Path to your self-signed certificate
        ssl_certificate_key /etc/letsencrypt/live/ybzone.io.vn/privkey.pem; # Path to your self-signed certificate key

        # Optional: Add SSL settings for better security
        # l_protocols TLSv1.2 TLSv1.3;
        # ssl_prefer_server_ciphers on;
        # ssl_ciphers EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH;
        # ssl_session_cache shared:SSL:10m;
        # ssl_session_timeout 1d;
        # ssl_session_tickets off;

        location / {
            proxy_pass http://admin.web:3000;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }

    server {
        listen 80;
        listen [::]:80; # ensures that the server listens on both IPv4 and IPv6 on port 80.

        server_name ybzone.io.vn;  # Added the missing semicolon

        root /var/www/html;
        index index.html index.htm index.nginx-debian.html;

        location / {
            proxy_pass http://client.web:3000;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
            proxy_set_header Host $host;
        }
    }

    server {
        listen 80;
        listen [::]:80; # ensures that the server listens on both IPv4 and IPv6 on port 80.

        server_name admin.ybzone.io.vn;  # Added the missing semicolon

        root /var/www/html;
        index index.html index.htm index.nginx-debian.html;

        location / {    
            proxy_pass http://admin.web:3000;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
            proxy_set_header Host $host;
        }
    }
}
```