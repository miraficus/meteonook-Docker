# 🚀 **MeteoNook Docker Setup Guide for Synology NAS**

Welcome to the **MeteoNook Docker Setup Guide**! This guide will walk you through setting up MeteoNook on your **Synology NAS** using Docker. Even if you’re new to Docker or Synology, don’t worry—I’ve got you covered! Let’s get started. 💻✨

---

## 🌟 **What is MeteoNook?**

MeteoNook is a weather prediction tool for **Animal Crossing: New Horizons**. 🎮🌦️ It helps you predict the weather patterns in your game based on seed values.

Here are the sources used for this project:

- **MeteoNook source code**: [https://github.com/Treeki/MeteoNook](https://github.com/Treeki/MeteoNook)
- **Tonky MeteoNook fork**: [https://github.com/herpiko/tonky-meteonook](https://github.com/herpiko/tonky-meteonook)
- **Commit version related to this build**: [a7ea07aa9b3db8859b0f476c549a1a2245ad1b07](https://github.com/Treeki/MeteoNook/commit/a7ea07aa9b3db8859b0f476c549a1a2245ad1b07)

---

## 🏗️ **Step 1: Install Docker on Synology NAS**

First, let’s install **Container Manager** (Docker) on your NAS:

1. Open **Package Center** in your Synology DSM web interface.
2. Search for **Container Manager** (this replaces the old Docker package).
3. Click **Install** and wait for the installation to complete.

Once installed, you’re ready to set up your project! 🚀

---

## 📂 **Step 2: Create a Folder for MeteoNook**

Next, we’ll create a shared folder where the Docker container will store the app files:

1. Open **File Station** on your Synology NAS.
2. Navigate to your **USB drive** (or another storage location).
3. Click **Create** → **Create New Folder** and name it something like:
   ```
   meteo-docker
   ```
4. **Upload** the `Dockerfile` and any other required files (e.g., your MeteoNook project files) into this folder.

Now the `Dockerfile` is ready for use. ✅

---

## 🔑 **Step 3: Enable SSH & Access the Terminal**

Now, we need to access the NAS terminal via **SSH** to run the Docker commands:

### ✅ **Enable SSH on Synology NAS**

1. Open **Control Panel** on your NAS.
2. Go to **Terminal & SNMP** → **Terminal** tab.
3. Check **Enable SSH service** and click **Apply**.

### 🔌 **Connect to Your NAS via SSH**

1. Open a terminal (on Mac/Linux) or use **PuTTY** (on Windows).
2. Connect to your NAS by running:

   ```bash
   ssh admin@your-nas-ip
   ```

   Replace `your-nas-ip` with the actual IP address of your NAS.
3. Enter your **admin password** when prompted.

Now you have terminal access to your NAS! 🎉

---

## 🔨 **Step 4: Build and Run the Docker Container**

Now that SSH is set up, we can build and run the container. **Since Synology requires `sudo`,** you must add `sudo` before every command.

### 🧱 **Build the Docker Image**

Navigate to the folder where you uploaded your `Dockerfile`:

```bash
cd /volumeUSB1/usbshare/meteo-docker
```

Then build the image:

```bash
sudo docker build -t meteonook-usb .
```

### 🚀 **Run the Docker Container**

Now, run the container in detached mode:

```bash
sudo docker run -d \
  -p 1337:1337 \
  -v /volumeUSB1/usbshare/meteo-docker:/app \
  --name meteonook-usb-app \
  meteonook-usb
```

This starts the container **in the background** and maps port `1337`.

---

## 🖥️ **Step 5: Set Up via Synology’s GUI (Optional)**

If you prefer using the Synology **Container Manager** instead of SSH, follow these steps:

1. Open **Container Manager** on DSM.
2. Go to **Container** → Click **Create** → **Select Image**.
3. Choose the **meteonook-usb** image that you built earlier.
4. In **Volume Settings**:
   - Mount path: `/app`
   - Host path: `/volumeUSB1/usbshare/meteo-docker`
5. In **Port Settings**:
   - Local port: `1337`
   - Container port: `1337`
6. Click **Apply & Start**.

Your app should now be running! 🎉

---

## ✅ **Step 6: Verify Everything is Working**

Let’s check if the container is running correctly.

### 🏃 **Check Running Containers**

```bash
sudo docker ps
```

### 📂 **Verify Your Files Inside the Container**

```bash
sudo docker exec meteonook-usb-app ls -la /app
```

### 🌍 **Open the App in Your Browser**

Go to:

```
http://your-nas-ip:1337
```

If you see the MeteoNook interface, everything is working! 🎉

---

## 💡 **Pro Tips & Troubleshooting**

- **Auto-restart the container on boot**:

  ```bash
  sudo docker update --restart unless-stopped meteonook-usb-app
  ```

- **Check logs for debugging**:

  ```bash
  sudo docker logs meteonook-usb-app
  ```

- **Fix file permissions if needed**:

  ```bash
  sudo chmod -R 755 /volumeUSB1/usbshare/meteo-docker
  ```

---

## 🎉 **You Did It!**

Congrats! 🎊 Your MeteoNook app is now running on your Synology NAS. You can now use it to predict the weather in **Animal Crossing: New Horizons**! 🌦️

