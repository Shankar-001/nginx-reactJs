# 1. Install Nginx:

First install Nginx Using Package Manager

```bash
sudo apt update
sudo apt install nginx
```

# 2. Build Your React App:

Your React app must be constructed. Use create-react-app or your preferred build tool. You can build it with:

```bash
npm run build
```

# 3. Copy Build to Nginx Directory:

Copy the build folder to the root directory of the Nginx web server, which is usually /var/www/html/:

```bash
sudo cp -r build/* /var/www/html/
```

# 4. Configure Nginx:

Create a React app Nginx server block configuration file. For instance, create "myreactapp" or "your_own_name" in /etc/nginx/sites-available/:

```bash
sudo nano /etc/nginx/sites-available/myreactapp
```

```bash
server {
    listen 80;
    server_name your_domain_or_ip;

    location / {
        root /var/www/html;
        index index.html;
        try_files $uri $uri/ /index.html;
    }

    # Additional configurations if needed
    # ...

}
```
For example
```bash
server {
    listen        80;
    listen        [::]:80;

    root          /var/www/html;
    index         index.html index.htm index.nginx-debian.html;

    server_name   111.11.11.111;

    location / {
        try_files $uri $uri/ =404;
    }

    # Additional configurations if needed
    # ...

}
```

# 5. Enable the Nginx Configuration:

Change myreactapp with your own folder name

```bash
sudo ln -s /etc/nginx/sites-available/myreactapp /etc/nginx/sites-enabled/
```

# 6. Test Nginx Configuration:

Ensure there are no syntax errors in your Nginx configuration:

```bash
sudo nginx -t
```

# 7. Adjust Firewall Settings: (optional)

If you are using a firewall, make sure it allows traffic on port 80:

```bash
sudo ufw allow 80
```

# 8. Access Your React App:

Launch a web browser and go to the IP address of your server or domain. Your React app should be open and functioning.

Recall that this is a simple configuration. You might need to modify the Nginx configuration further, depending on the needs of your application (e.g., for HTTPS, additional security settings, proxying to a backend server, etc.).
