# 🔐 Activity: Enabling HTTPS with Let's Encrypt and Apache on Ubuntu

Much of this is sourced from: [https://letsencrypt.org/getting-started/](https://letsencrypt.org/getting-started/)

---

## ✅ Pre-requisites

Before proceeding, ensure the following:

1. You have a domain name (e.g., `yourdomain.com`) **with an A record pointing to your VM’s public IP**.
2. You are running the **Apache web server** on your cloud-based Ubuntu machine.
3. Ports **22 (SSH), 80 (HTTP), and 443 (HTTPS)** are open in your VM firewall (e.g., AWS Security Group).

---

## ✅ Step 1: Verify DNS and Apache

### 🔹 SSH Access Test

On your **local machine**, run:

```bash
ssh -i pemkey.pem ubuntu@yourdomain.com
```

✅ You should connect without issues.

---

### 🔹 HTTP Access Test

On your local CLI:

```bash
wget http://yourdomain.com
```

Or visit in your browser:

```
http://yourdomain.com
```

✅ You should see the Apache welcome page or your site content.

---

## ✅ Step 2: Obtain TLS Certificate with Let's Encrypt

### 🔹 Visit Certbot Site

Go to: [https://certbot.eff.org/](https://certbot.eff.org/)

- Choose:
  - **Software**: `Apache`
  - **System**: `Linux (snap)`

Follow the on-screen instructions, summarized below:

---

### 🔹 Install Certbot via Snap

```bash
sudo apt update
sudo apt install snapd -y
sudo snap install core; sudo snap refresh core
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

---

### 🔹 Run Certbot for Apache

```bash
sudo certbot --apache
```

Follow the prompts:
- Choose your domain(s)
- Certbot will verify ownership and install the certificate

---

## ✅ Step 3: Test HTTPS Access

Visit:

```
https://yourdomain.com
```

- ✅ Look for the 🔒 **lock icon** in your browser.
- Click it → View certificate → **Issuer should be Let's Encrypt**

---

## ✅ Step 4: Confirm Auto-Renewal

Run a dry run to ensure auto-renew works:

```bash
sudo certbot renew --dry-run
```

✅ Look for the message: **"Congratulations, all renewals succeeded."**

---

## 🧠 Recap

| Step | Purpose |
|------|---------|
| Set DNS A Record | Links domain to server IP |
| Verify HTTP | Confirms Apache + domain reachable |
| Certbot Install | Adds Let's Encrypt client |
| Run Certbot | Issues and installs HTTPS cert |
| Browser Test | Confirms secure setup |
| Auto-renew Test | Validates cert will auto-renew |

---
