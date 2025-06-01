🚀 Full-Stack Deployment Guide (Node.js + React)

- Use this guide to deploy any full-stack JavaScript application with:
- Backend: Node.js (Express or similar)
- Frontend: React (or other SPA frameworks)
- Database: MongoDB (cloud/local)
- Process Manager: PM2
- Web Server: Nginx

1. 🔁 Clone Your Project
```bash
~ git clone <your_repo_url>
~ cd <your_project_directory>
```

2. 🛠️ Backend Setup
Navigate to your backend folder:
```bash
~ cd <backend-folder-name>
```

Create a .env file:

```bash
~ nano .env
```

```bash
Example contents:

MONGO_URI=mongodb+srv://<user>:<password>@cluster.mongodb.net/<dbname>?retryWrites=true&w=majority
PORT=5000
JWT_SECRET=your_secret_key
Replace placeholders with actual values.

```

Install dependencies:

```bash
~ npm install
```

Start with PM2:

```bash
~ pm2 start <entry-file>.js --name backend-app
~ pm2 save
~ pm2 startup
```

3. 🌐 Frontend Setup
Navigate to your frontend folder:

```bash
~ cd ../<frontend-folder-name>
```

Install dependencies and build:

```bash
~ npm install
~ npm run build
```

Move build to Nginx directory:

```bash
~ sudo mkdir -p /var/www/html
~ sudo cp -r dist/* /var/www/html

For Create React App, replace dist with build.

```

4. ⚙️ Nginx Setup
Edit default site config:

```bash
~ sudo nano /etc/nginx/sites-available/default


Paste or edit:

nginx
Copy
Edit
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    index index.html index.htm;

    server_name _;

    location / {
        try_files $uri /index.html;
    }

    location /api/ {
        proxy_pass http://localhost:5000/;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```
Test and reload Nginx:

```bash
~ sudo nginx -t
~ sudo systemctl reload nginx
```

✅ Done!
Visit http://<your-server-ip> in your browser.

🧪 Troubleshooting
Check backend logs:

```bash
~ pm2 logs backend-app
```

Restart backend:

```bash
~ pm2 restart backend-app
```

Rebuild frontend (after changes):

```bash
~ npm run build
```

🔒 Bonus: SSL with Let's Encrypt (Optional)
Use Certbot to add HTTPS:

```bash
~ sudo apt install certbot python3-certbot-nginx
~ sudo certbot --nginx
```
