# Deploying Local Applications Using Cloudflared Tunnel

## Overview

`cloudflared` is a command-line tool provided by **Cloudflare** that establishes a secure tunnel between your local machine and the Cloudflare network. This allows developers to expose a local web service to the public internet without needing to open firewall ports, configure NAT, or obtain a static IP address. It is widely used to securely serve internal services, dashboards, or development websites over HTTPS using custom domain names.

This document provides a comprehensive step-by-step guide to deploying a local web application (such as a Dash dashboard) using Cloudflare Tunnel on a Windows machine, with a custom domain managed via Cloudflare DNS.

---

## Prerequisites

* A registered domain name added to your Cloudflare account
* A local web service running (e.g., Dash app on `http://localhost:8050`)
* Windows environment with administrative privileges

---

## Step 1: Install `cloudflared`

1. Download `cloudflared` from the [official Cloudflare site](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/installation/#windows)
2. Place `cloudflared.exe` in a known directory (e.g., `C:\cloudflared`)
3. (Optional) Add the directory to the **system PATH** variable for global command-line access

---

## Step 2: Authenticate with Cloudflare
!!! info "Note"
    You need to Open CMD NOT Powershell to run the following commands.


```bash
cloudflared login
```

* A browser window will open prompting you to log in and select your domain
* On success, a `.cloudflared/.cert.pem` file will be generated at `C:\Users\<YourUsername>\.cloudflared\.cert.pem`

---

## Step 3: Create a Tunnel

```bash
cloudflared tunnel create dash-tunnel
```

* This generates a unique Tunnel ID and corresponding credentials `.json` file

---

## Step 4: Configure the Tunnel

Create a `config.yml` file in:

```
C:\Users\<YourUsername>\.cloudflared\config.yml
```

Example:

```yaml
tunnel: dash-tunnel
credentials-file: "C:\Users\Now Now\.cloudflared\your-dash-tunnel-name.json" # The name you gave to the tunnel when you created it

ingress:
  - hostname: dash.geopulse.fun # The custom domain you added to Cloudflare
    service: http://localhost:8050    # The local port your service is running on
  - service: http_status:404    # A 404 page to handle non-matched routes

```

Ensure paths are correctly quoted if they contain spaces.

---

## Step 5: Route DNS to the Tunnel

```bash
cloudflared tunnel route dns dash-tunnel dash.geopulse.fun
```

* This command creates a DNS `CNAME` record pointing your subdomain to the tunnel

---

## Step 6: Start the Tunnel

### Option A: Temporary (development)

```bash
cloudflared tunnel --config "C:\Users\Now Now\.cloudflared\config.yml" run dash-tunnel
```

### Option B: Persistent as a Windows Service

```bash
cloudflared service install
```

* This will run the tunnel automatically on system boot
* Alternatively, create a Task Scheduler entry to launch it on user login

---

## Step 7: Verify Public Access

Visit:

```
https://dash.geopulse.fun
```

If everything is configured correctly, you should see your local Dash app accessible over HTTPS.

---

## Additional Recommendations

* Use `cloudflared tunnel info dash-tunnel` to verify tunnel health
* Keep your Dash app auto-started with Docker's `--restart=always` flag
* Use GitHub Pages + Cloudflare DNS together for static site hosting
* Consider implementing Basic Auth or Access Policies via Cloudflare Zero Trust for private dashboards

---

## Summary

By combining `cloudflared`, a local web service, and Cloudflare's secure global edge network, you can safely expose applications for development, collaboration, or even lightweight production use with minimal infrastructure and maximum security.
