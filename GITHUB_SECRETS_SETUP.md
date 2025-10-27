# 🔐 GitHub Secrets Setup Guide

## Required Secrets (Add to GitHub Repository)

Go to: **Settings → Secrets and variables → Actions → New repository secret**

Add these 4 secrets:

---

### 1. **EC2_HOST** (Most Important!)
**Value**: Your EC2 instance public IP or hostname

Examples:
- `3.85.123.45` (public IP)
- `ec2-12-34-56-78.us-east-1.compute.amazonaws.com` (public DNS)
- `your-domain.com` (if using a domain)

**How to get it:**
1. Go to AWS EC2 Console
2. Select your instance
3. Copy the **Public IPv4 address** or **Public IPv4 DNS**

---

### 2. **EC2_USER**
**Value**: The SSH username for your EC2 instance

Common values:
- `ec2-user` (for Amazon Linux)
- `ubuntu` (for Ubuntu)
- `admin` (for other Linux distros)

**How to know:**
- Amazon Linux → `ec2-user`
- Ubuntu → `ubuntu`
- Debian → `admin` or `root`

---

### 3. **EC2_SSH_KEY**
**Value**: Complete content of your `.pem` file

**How to get it:**
```bash
# On your local machine
cat your-key.pem

# Copy EVERYTHING including these lines:
# -----BEGIN RSA PRIVATE KEY-----
# ... (all the content) ...
# -----END RSA PRIVATE KEY-----
```

**IMPORTANT**: Copy the entire file, including the BEGIN and END lines!

---

### 4. **APP_DIRECTORY**
**Value**: Full path where the app is cloned on EC2

Example: `/home/ec2-user/vaccine-management`

**How to set it:**
```bash
# SSH into EC2
ssh -i your-key.pem ec2-user@your-ec2-ip

# Find the path
pwd
# It will show something like: /home/ec2-user/vaccine-management
```

---

## 📝 Step-by-Step: Adding Secrets

1. Open your GitHub repository
2. Click **Settings** (top menu)
3. Click **Secrets and variables** (left sidebar)
4. Click **Actions**
5. Click **New repository secret** (button)
6. For each secret:
   - **Name**: Enter exact name (e.g., `EC2_HOST`)
   - **Secret**: Paste the value
   - Click **Add secret**

Repeat for all 4 secrets.

---

## ✅ Verification

After adding all secrets, you should see them listed in the secrets page:
- EC2_HOST
- EC2_USER  
- EC2_SSH_KEY
- APP_DIRECTORY

---

## 🚨 Common Mistakes

❌ **Wrong**: EC2_HOST value is empty or incorrect IP  
✅ **Right**: Use the actual public IP from AWS console

❌ **Wrong**: EC2_SSH_KEY is missing BEGIN/END lines  
✅ **Right**: Copy the entire .pem file content

❌ **Wrong**: APP_DIRECTORY uses relative path  
✅ **Right**: Use absolute path like `/home/ec2-user/vaccine-management`

---

## 🧪 Test Your Setup

1. Add all 4 secrets
2. Make a small change (add a comment to any file)
3. Commit and push to `master` branch
4. Go to **Actions** tab
5. Watch the workflow run

If you see: `ERROR: EC2_HOST secret is not set!`  
→ You missed adding a secret or there's a typo in the name

If you see: `Connecting to EC2_HOST: 3.85.123.45`  
→ Good! Secrets are set correctly

