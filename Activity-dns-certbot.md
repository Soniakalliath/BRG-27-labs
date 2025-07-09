# 🌐 Lab Guide: Setting Up DNS and Let's Encrypt on Ubuntu

---

## 🔷 Part A: DNS – Linking Domain Name to Cloud VM

### ✅ Step A1: Purchase a Domain Name
- Choose a registrar:
  - Namecheap, GoDaddy, AWS Route 53, or Cloudflare Registrar
- Register a domain (e.g., `yourdomain.com`)
- Turn off auto-renew if not needed
- Avoid ccTLDs from OFAC-restricted countries (e.g., `.ir`, `.sy`)

---

### ✅ Step A2: Get Your Cloud VM’s Public IP
SSH into your Ubuntu VM:

```bash
curl ifconfig.me
```

Or get the public IP from your cloud provider's dashboard.

---

### ✅ Step A3: Add an A Record in DNS
In your domain registrar’s DNS panel:

| Field     | Value                        |
|-----------|------------------------------|
| Type      | A                            |
| Name      | `@` or `yourdomain.com`      |
| Value     | Your Cloud VM’s Public IP    |
| TTL       | Auto or 30 minutes           |

Optional:

| Field     | Value                        |
|-----------|------------------------------|
| Type      | A                            |
| Name      | `www`                        |
| Value     | Same Public IP               |
| TTL       | Auto                         |

---

### ✅ Step A4: Test DNS Resolution

Wait 5–30 minutes for DNS to propagate.

Test using:

```bash
nslookup yourdomain.com
dig yourdomain.com
```

Browser:

```
http://yourdomain.com
```

You should see the Apache welcome page.

---

## 🟢 Part B: Let's Encrypt – Enabling HTTPS with Certbot

### ✅ Step B1: Install Certbot and Apache Plugin

```bash
sudo apt update
sudo apt install certbot python3-certbot-apache -y
```

---

### ✅ Step B2: Run Certbot to Obtain TLS Certificate

```bash
sudo certbot --apache
```

Follow the prompts to:
- Select your domain
- Automatically configure HTTPS

---

### ✅ Step B3: Verify HTTPS is Working

Open your site in browser:

```
https://yourdomain.com
```

- Click the lock icon
- View certificate details
- Issuer should be **Let's Encrypt**

---

### ✅ Step B4: Enable and Test Auto-Renewal

Test certbot renewal:

```bash
sudo certbot renew --dry-run
```

If successful:  
✔️ "Congratulations, all renewals succeeded"

---

## ✅ Summary

| Component      | Purpose                          |
|----------------|----------------------------------|
| Domain Name    | Internet address for your site   |
| DNS A Record   | Links domain to VM's IP          |
| Apache2        | Web server hosting your site     |
| Certbot        | TLS certificate management       |
| HTTPS Enabled  | Secure connection to your site   |

---
