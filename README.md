# Infinite Web Arena - Coming Soon Page

## Quick Start

### 1. Install Dependencies

```bash
npm install
```

### 2. Start the Express Server

```bash
# Production
npm start

# Development (with auto-reload)
npm run dev
```

The server will run on `http://localhost:3000`

### 3. Configure Nginx

#### Linux/Mac

1. Copy the nginx configuration:
```bash
sudo cp nginx.conf /etc/nginx/sites-available/coming-soon
sudo ln -s /etc/nginx/sites-available/coming-soon /etc/nginx/sites-enabled/
```

2. Test nginx configuration:
```bash
sudo nginx -t
```

3. Restart nginx:
```bash
sudo systemctl restart nginx
# or
sudo service nginx restart
```

#### Windows

1. Copy the configuration to nginx conf directory:
```bash
copy nginx.conf C:\nginx\conf\sites-enabled\coming-soon.conf
```

2. Include this in your main `nginx.conf`:
```nginx
http {
    # ... other config ...
    include sites-enabled/*.conf;
}
```

3. Reload nginx:
```bash
nginx -s reload
```

### 4. Access Your Site

Visit `http://localhost` or `http://your-domain.com`

Nginx will proxy requests from port 80 to your Express server on port 3000.

## Production Deployment

### Using PM2 (Recommended)

1. Install PM2 globally:
```bash
npm install -g pm2
```

2. Start the server with PM2:
```bash
pm2 start server.js --name "coming-soon"
```

3. Save PM2 configuration:
```bash
pm2 save
pm2 startup
```

4. Monitor your application:
```bash
pm2 status
pm2 logs coming-soon
```

### Manual Start (Background)

```bash
# Linux/Mac
nohup node server.js > server.log 2>&1 &

# Or using screen
screen -S coming-soon
node server.js
# Press Ctrl+A then D to detach
```

## File Structure

```
coming-soon/
├── index.html      # Main HTML file
├── banner.gif      # Banner image
├── server.js       # Express server
├── package.json    # Dependencies
├── nginx.conf      # Nginx configuration
└── README.md       # This file
```

## Troubleshooting

### Port 3000 already in use
```bash
# Linux/Mac
lsof -ti:3000 | xargs kill -9

# Windows
netstat -ano | findstr :3000
taskkill /PID <PID> /F
```

### Nginx not proxying correctly
- Check if Express server is running: `curl http://localhost:3000`
- Check nginx error logs: `sudo tail -f /var/log/nginx/error.log`
- Verify nginx is running: `sudo systemctl status nginx`

### Cannot access from external network
- Make sure firewall allows port 80
- Update `server_name` in nginx.conf to your domain or IP

