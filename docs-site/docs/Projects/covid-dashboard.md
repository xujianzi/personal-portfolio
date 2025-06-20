# Deploying Dash Locally and Making It Publicly Accessible via Ngrok

This guide walks you through all the steps to deploy your Dash app locally using Docker and PostgreSQL, and share it publicly using Ngrok.

---

## 1. Prerequisites

Before starting, ensure you have:

* A working Dash app running locally on port 8050
* Docker installed and the app running inside a container
* PostgreSQL running on your local Windows machine, accessible to the Dash app

---

## 2. Verify Local Deployment

Ensure your Dash app is accessible via your browser at:

```
http://localhost:8050
```

Make sure:

* The Dash app binds to `0.0.0.0` (not just `127.0.0.1`) inside Docker
* The Docker container can connect to the PostgreSQL database via `host.docker.internal`

Example Dash app launch code:

```python
if __name__ == '__main__':
    app.run_server(host='0.0.0.0', port=8050, debug=False)
```

---

## 3. Set Up PostgreSQL for Docker Access

### 3.1 Find Configuration Files

Run this SQL command in pgAdmin or psql to find the path to config files:

```sql
SHOW config_file;
SHOW hba_file;
```

### 3.2 Edit postgresql.conf

* Locate and open `postgresql.conf`
* Change:

  ```conf
  listen_addresses = '*'
  ```

### 3.3 Edit pg\_hba.conf

* Open `pg_hba.conf`
* Add this line:

  ```conf
  host    all             all             172.17.0.0/16           md5
  ```

  This allows Docker container IPs to connect

### 3.4 Restart PostgreSQL Service

* Open `services.msc`
* Find `postgresql-x64-14` (or your version)
* Right-click > Restart

---

## 4. Install and Configure Ngrok

### 4.1 Download Ngrok

* Visit: [https://ngrok.com/download](https://ngrok.com/download)
* Download the Windows version and unzip it to a folder (e.g., `C:\ngrok`)

### 4.2 Register for a Free Account

* Visit: [https://dashboard.ngrok.com/signup](https://dashboard.ngrok.com/signup)
* After login, copy your **auth token**

### 4.3 Authenticate Ngrok

Open PowerShell or CMD in the Ngrok folder and run:

```powershell
./ngrok authtoken YOUR_AUTHTOKEN_HERE
```

---

## 5. Expose Dash to the Public

In the same folder, run:

```powershell
./ngrok http 8050
```

You’ll see an output like:

```
Forwarding    https://abcd1234.ngrok.io -> http://localhost:8050
```

Share this HTTPS URL with others—they can now access your Dash app over the internet.

---

## 6. Optional: One-Click Startup Script

Create a `start_ngrok.bat` file with:

```bat
@echo off
cd /d C:\ngrok
ngrok http 8050
pause
```

Double-click to launch the tunnel easily.

---

## 7. Notes and Considerations

* **Free Ngrok** tunnels last up to 8 hours
* Each session creates a **new** URL unless you upgrade for custom subdomains
* For production use, consider persistent hosting (e.g., cloud VM + reverse proxy)

---

You’re now ready to share your Dash app from your local machine with anyone in the world!
