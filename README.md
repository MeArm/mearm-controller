# MeArm Web Controller Pro 🤖🌐

A sleek, lightweight, single-page web application to control your physical MeArm 4-axis robotic arm directly from your web browser. 

This project bypasses the need for local desktop software installations (like Python or Tkinter) by leveraging the modern native **Web Serial API** to send smooth position updates to your hardware over a standard USB cable.

## 🚀 Live Demo

<img width="567" height="587" alt="WebController" src="https://github.com/user-attachments/assets/c32171d7-9b01-46ca-bfcc-d09ed9e131f7" />

👉 **[Launch Live Web Controller](https://mearm.github.io/mearm-controller/)**

---

## ✨ Features
* **Zero Desktop Dependencies:** Runs entirely inside modern desktop web browsers—no Python, Node.js, or local servers required.
* **Bi-directional Controls:** Use fluid visual sliders or type precise degree coordinates via numeric input fields.
* **Auto-Reconnection Support:** Safely handles accidental cable unplugs, clearing active resource locks automatically without needing a browser refresh.
* **State Persistence:** Automatically remembers and loads your last configuration positions using localized browser caching (`localStorage`).
* **Live Hardware Feedback:** Features an integrated console terminal that displays real-time debugging responses sent back from the robot.
* **Rate-Throttled Stream:** Locks packet transmission to a safe, hardware-friendly 25Hz (~40ms interval) throttle to prevent data flooding.

---

## 🛠️ Hardware Requirements
1. **MeArm Robotic Arm** (or any 4-axis servo robot setup).
2. **Microcontroller Board:** Raspberry Pi Pico, Arduino, or ESP32 running a basic serial reader firmware.
3. **USB Connection Cable** linking the microcontroller to your computer.

---

## 💻 Browser Compatibility
Because this app communicates directly with computer hardware ports over USB, it requires a secure sandbox environment and a browser that supports the **Web Serial API**:

| Google Chrome | Microsoft Edge | Opera | Mozilla Firefox | Apple Safari |
| :---: | :---: | :---: | :---: | :---: |
|  Yes |  Yes |  Yes | ❌ No | ❌ No |

> ⚠️ **Note:** The Web Serial API requires a **Secure Context**. It will work on `http://localhost` during local development, but once deployed online, it **must** be served over an encrypted `https://` connection (which GitHub Pages handles automatically). It is currently not supported on mobile browsers (iOS/Android).

---

## 🛰️ Serial Protocol Format
The controller builds and streams plain-text ASCII data packets over the serial connection at **115200 baud**. Each motion event pushes a single line terminated with a newline (`\n`) character containing 4 comma-separated integer angles:

`Base,Left,Right,Claw\n`

**Example Packet:**
`90,120,45,40\n`
* `90` -> Base rotation angle (Range: 1° to 179°)
* `120` -> Left shoulder servo angle (Range: 35° to 170°)
* `45` -> Right elbow servo angle (Range: 30° to 130°)
* `40` -> Claw gripper angle (Range: 80° to 170°)

---

## 📦 Rapid Deployment Instructions
Since the app is built into a single static file, you can publish it globally using GitHub Pages in under a minute:

1. Fork or upload this repository to your GitHub account as a **Public** repository.
2. Ensure your primary file is named exactly `index.html`.
3. Go to the repository **Settings** tab.
4. Select **Pages** from the left-hand navigation sidebar.
5. Under *Build and deployment*, change the **Branch** dropdown target from *None* to **main** (or *master*) and click **Save**.
6. Wait 30 seconds for the deployment workflow to complete, then open your generated secure `https://` link!

---

## 📝 License
This project is open-source and free to modify or distribute for your own custom hardware creations. Enjoy tinkering!
