Perfect 👍 — here’s a **complete, step-by-step guide** to configure a **custom domain from Hostinger to GitHub Pages** — from start to finish.

---

## 🌐 **Goal**

You have a domain from **Hostinger** (e.g., `yourdomain.com`)
You have a website hosted on **GitHub Pages** (e.g., `username.github.io`)
You want visitors to reach your site at `yourdomain.com` (or `www.yourdomain.com`).

---

## 🧭 **Step 1: Prepare Your GitHub Pages Site**

1. Go to your **GitHub repository** (the one hosting your site).
2. Click **Settings → Pages** (on the left sidebar).
3. Under **Source**, make sure your site is published (e.g., from the `main` branch or `gh-pages`).
4. In the **Custom domain** box, type your domain — for example:

   * `yourdomain.com` → if you want the apex/root domain, or
   * `www.yourdomain.com` → if you want to use the “www” subdomain.
5. Click **Save**.
6. GitHub will automatically create a `CNAME` file in your repository containing your domain name.
7. Keep this tab open — you’ll come back later to enable HTTPS once DNS works.

---

## 🔧 **Step 2: Set Up DNS in Hostinger (hPanel)**

### 🔹 Log In

1. Go to [hostinger.com](https://www.hostinger.com) → **Login → hPanel**.
2. Go to **Domains → [Your Domain] → DNS / Nameservers**.

---

### 🔹 If you’re using the **root domain** (`yourdomain.com`)

You’ll add **A records** that point directly to GitHub Pages servers.

1. Remove any existing **A**, **AAAA**, or **CNAME** records for `@` (root).
2. Add **4 A records** as follows:

| Type | Name | Value           | TTL     |
| ---- | ---- | --------------- | ------- |
| A    | @    | 185.199.108.153 | Default |
| A    | @    | 185.199.109.153 | Default |
| A    | @    | 185.199.110.153 | Default |
| A    | @    | 185.199.111.153 | Default |

3. (Optional) For IPv6 support, add **AAAA records**:

| Type | Name | Value               |
| ---- | ---- | ------------------- |
| AAAA | @    | 2606:50c0:8000::153 |
| AAAA | @    | 2606:50c0:8001::153 |
| AAAA | @    | 2606:50c0:8002::153 |
| AAAA | @    | 2606:50c0:8003::153 |

4. (Recommended) Create a CNAME record for `www`:

| Type  | Name | Value              | TTL     |
| ----- | ---- | ------------------ | ------- |
| CNAME | www  | username.github.io | Default |

*(Replace `username` with your actual GitHub username.)*

---

### 🔹 If you’re using a **subdomain** (`www.yourdomain.com` or `blog.yourdomain.com`)

You’ll add a **CNAME record** instead of A records.

| Type  | Name          | Value              | TTL     |
| ----- | ------------- | ------------------ | ------- |
| CNAME | www (or blog) | username.github.io | Default |

> ⚠️ Remove any A or AAAA records for the same subdomain before saving.

---

## ⏳ **Step 3: Wait for DNS Propagation**

* It can take **30 minutes to 24 hours** for the DNS changes to spread globally.
* You can check propagation using:
  🔗 [https://dnschecker.org](https://dnschecker.org) — enter your domain and check “A” or “CNAME”.

---

## 🔍 **Step 4: Verify on GitHub**

After the DNS records have propagated:

1. Go back to your **GitHub repository → Settings → Pages**.
2. Make sure your domain appears correctly under **Custom domain**.
3. GitHub will verify that your DNS points correctly.
4. Once verified, toggle **“Enforce HTTPS”** (this enables SSL from GitHub).

   * It might take a few minutes to issue the certificate.
   * If the toggle doesn’t appear immediately, refresh the page after a few minutes.

---

## 🧾 **Step 5: (Optional) Redirect “www” to Root Domain or Vice Versa**

If you want both `yourdomain.com` and `www.yourdomain.com` to work:

* If you set up **A records for root domain** (`@`), then add a CNAME for `www → username.github.io`.
* If you set up **CNAME for www**, GitHub automatically handles redirection from the root to `www`.

---

## ✅ **Step 6: Test Everything**

1. Visit `https://yourdomain.com` (or `https://www.yourdomain.com`).
2. It should load your GitHub Pages site.
3. HTTPS should be enabled, and your site should display normally.

---

## 🧰 **Troubleshooting Tips**

| Problem                                  | Fix                                                    |
| ---------------------------------------- | ------------------------------------------------------ |
| Domain not resolving                     | Double-check your DNS records and propagation.         |
| HTTPS not available                      | Wait for GitHub to issue SSL (can take up to 1 hour).  |
| “Custom domain already taken” error      | Ensure no other repo is using the same domain.         |
| GitHub says “Not resolving to Pages IPs” | Make sure A records exactly match the four GitHub IPs. |

---

Would you like me to create an **example DNS record table** specifically for your domain (e.g., `mywebsite.com`)?
If you tell me your domain and GitHub username, I’ll show exactly what to enter in Hostinger.
