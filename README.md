🛠️ 1. ติดตั้ง Node.js และ Git
ดาวน์โหลดและติดตั้งจาก:

https://nodejs.org

https://git-scm.com (ถ้ายังไม่มี)

📁 2. สร้างโปรเจกต์ Electron
bash
คัดลอก
แก้ไข
mkdir my-electron-app
cd my-electron-app
npm init -y
npm install --save-dev electron electron-builder
🧱 3. สร้างไฟล์โปรเจกต์
🔹 main.js
js
คัดลอก
แก้ไข
const { app, BrowserWindow } = require('electron');

function createWindow() {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
  });

  win.loadFile('index.html');
}

app.whenReady().then(createWindow);
🔹 index.html
html
คัดลอก
แก้ไข
<!DOCTYPE html>
<html>
  <head><title>My App</title></head>
  <body>
    <h1>Hello from Electron!</h1>
  </body>
</html>
🧾 4. แก้ไข package.json
ให้แก้ให้เป็นแบบนี้:

json
คัดลอก
แก้ไข
{
  "name": "my-electron-app",
  "version": "1.0.0",
  "main": "main.js",
  "scripts": {
    "start": "electron .",
    "pack": "electron-builder --dir",
    "dist": "electron-builder"
  },
  "devDependencies": {
    "electron": "^37.2.0",
    "electron-builder": "^26.0.12"
  },
  "build": {
    "appId": "com.example.myapp",
    "productName": "MyElectronApp",
    "files": [
      "**/*"
    ],
    "directories": {
      "output": "dist"
    },
    "win": {
      "target": "nsis"
    },
    "nsis": {
      "oneClick": false,
      "perMachine": true,
      "allowToChangeInstallationDirectory": true
    }
  }
}
🧠 (ถ้ามีไฟล์ icon.ico) เพิ่ม "icon": "icon.ico" ใน "win"

🚀 5. ทดสอบรันแอป
bash
คัดลอก
แก้ไข
npm start
🧼 6. แก้ปัญหา "symlink permission"
เปิด Developer Mode บน Windows:

ไปที่ Settings → Privacy & security → For developers → เปิด Developer Mode

หรือใช้ CMD แบบ Administrator เวลา build:

bash
คัดลอก
แก้ไข
cd C:\xampp\htdocs\my-electron-app
npm run dist
📦 7. สร้างไฟล์ติดตั้งโปรแกรม .exe
bash
คัดลอก
แก้ไข
npm run dist
ผลลัพธ์จะอยู่ในโฟลเดอร์ dist/ เช่น:

คัดลอก
แก้ไข
dist/
├── MyElectronApp Setup 1.0.0.exe   ← ไฟล์ติดตั้ง
├── MyElectronApp-1.0.0.exe
├── latest.yml
