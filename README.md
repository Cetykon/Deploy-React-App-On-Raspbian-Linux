# Deploy-React-App-On-Raspbian-Linux
### This repo contains a simple guide on how to self-host your own web react app.


# How to Run a React Website on a Raspberry Pi

## Prerequisites
- You will need to have **Raspbian OS** installed.


## Steps

### 1. Open Terminal
Press `Ctrl+Alt+T` to open the terminal.

---

### 2. Update Libraries
Run the following commands to make sure your libraries are up to date:
```bash
sudo apt update
sudo apt upgrade
```

---

### 3. Install Git
Install Git by running:
```bash
sudo apt install git
```

---

### 4. Install Node.js and npm
Run the following commands to install Node.js and npm:
```bash
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
```

Verify the installation:
```bash
node -v
npm -v
```

---

### 5. Clone Your Git Project
Navigate to your preferred directory:
```bash
cd /path/to/prefer_directory
```

Clone your project:
```bash
git clone https://github.com/your-repo/your-project.git
```
> **Note:** When cloning, you will need to input your credentials. You may need to create a github key and input it as your password.

Navigate to your project:
```bash
cd your-project
```

---

### 6. Build the React Application
Navigate to the folder where your React app is located:
```bash
cd /path/to/your_app
```

Install dependencies and build the project:
```bash
npm install
npm run build
```

---

### 7. Install Nginx
Install Nginx:
```bash
sudo apt install nginx
```

---

### 8. Configure Nginx
Edit the configuration file for your project (use your preferred editor, e.g., `nano` or `micro`):
```bash
sudo nano /etc/nginx/sites-available/your_project
```

#### Example Configuration
Replace `server_name` and `root` paths with your values:
```nginx
server {
    listen 80;
    server_name 48.46.47.37;

    location / {
        root /home/cetykon/WebsiteHosting/IEP_Chatbot_Frontend/iepchatbot/build;
    }

    # Optionally, you can add a catch-all location block for errors
    location = /404.html {
        internal;
    }
}
```

Enable the configuration:
```bash
sudo ln -s /etc/nginx/sites-available/your_project /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

If needed, disable or remove the default configuration:
```bash
sudo rm /etc/nginx/sites-enabled/default
```

Ensure the symbolic link to your configuration exists:
```bash
sudo ln -s /etc/nginx/sites-available/your_project /etc/nginx/sites-enabled/
```

---

### 9. Set Permissions
Ensure Nginx has permission to read the files:
```bash
ls -l /home/cetykon/WebsiteHosting/IEP_Chatbot_Frontend/iepchatbot/build/index.html
sudo chown -R www-data:www-data /home/cetykon/WebsiteHosting/IEP_Chatbot_Frontend/iepchatbot/build
sudo chmod -R 755 /home/cetykon/WebsiteHosting/IEP_Chatbot_Frontend/iepchatbot/build
sudo chmod 755 /home/cetykon
sudo chmod 755 /home/cetykon/WebsiteHosting
sudo chmod 755 /home/cetykon/WebsiteHosting/IEP_Chatbot_Frontend
sudo chmod 755 /home/cetykon/WebsiteHosting/IEP_Chatbot_Frontend/iepchatbot
sudo chmod 755 /home/cetykon/WebsiteHosting/IEP_Chatbot_Frontend/iepchatbot/build
```

---

### 10. Restart Nginx
Once everything is set up, restart Nginx:
```bash
sudo systemctl restart nginx
```

---

### Additional Tips
- To find your public IP, use:
```bash
curl ifconfig.me
```

