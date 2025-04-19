# 🌦️ Meteonook Docker

Meteonook is a simple weather web app designed to display real-time local weather data using data pulled from Home Assistant. This repository provides a Dockerized version to run Meteonook on your **Synology NAS** or any Docker-compatible system.

---

## 📦 Features

- Easy deployment with Docker
- Persistent storage
- Customizable storage location
- Custom port configuration
- Works great on Synology NAS

---

## 🚀 Quick Start

To get started quickly with default settings:

```bash
docker run -d \
  --name meteonook \
  -p 1337:1337 \
  -v /volumeUSB1/usbshare/meteo-docker:/app/data \
  rfkgaming89/meteonook
```

---

## 🛠️ Customizing Your Setup

### 🔧 1. Change Where the Files Are Stored

By default, Docker stores Meteonook data in:

```
/volumeUSB1/usbshare/meteo-docker
```

To store data somewhere else (like another volume or folder):

#### 🖱️ If you're using Synology GUI:

1. **Open File Station** and go to the location where you want to store your data (e.g., `/volume1/docker/meteo-docker`).
2. **Create a new folder** (e.g., `meteo-docker`).
3. Ensure the Docker user has **read/write permissions** to the folder.
4. When creating the container, update the **volume mapping** accordingly:
   ```
   /your/custom/path:/app/data
   ```

#### 🖥️ If using CLI:

Change the `-v` flag like this:

```bash
-v /volume1/docker/meteo-docker:/app/data
```

---

### 🌐 2. Change the Web Port

By default, Meteonook runs on **port 1337** inside the container. You can change the external port to avoid conflicts with other services.

For example, to run on **port 8123**, change the `-p` flag:

```bash
-p 8123:1337
```

This means:
- **8123** = external port (the one you access in your browser)
- **1337** = internal port (used by the app inside the container)

You can now access Meteonook at:

```
http://<your-nas-ip>:8123
```

> 🔒 Make sure the port you choose isn’t already in use by another service.

---

## 📂 Example Full Docker Run (with custom path and port)

```bash
docker run -d \
  --name meteonook \
  -p 8123:1337 \
  -v /volume1/docker/meteo-docker:/app/data \
  rfkgaming89/meteonook
```

---

## 🧼 Stopping and Removing the Container

To stop the container:

```bash
docker stop meteonook
```

To remove the container:

```bash
docker rm meteonook
```

---

## 🙌 Credits

Here are the sources used for this project:

- MeteoNook original source code: [https://github.com/Treeki/MeteoNook](https://github.com/Treeki/MeteoNook)
- Tonky MeteoNook fork: [https://github.com/herpiko/tonky-meteonook](https://github.com/herpiko/tonky-meteonook)
- Commit version related to this build: [a7ea07aa9b3db8859b0f476c549a1a2245ad1b07](https://github.com/Treeki/MeteoNook/commit/a7ea07aa9b3db8859b0f476c549a1a2245ad1b07)

