# MyElectronApp

สร้างแอป Desktop ด้วย Electron และ build เป็นไฟล์ติดตั้ง `.exe` บน Windows

---

## ขั้นตอนทั้งหมด

1. ติดตั้ง Node.js และ Git จาก  
   https://nodejs.org  
   https://git-scm.com (ถ้ายังไม่มี)

2. เปิดเทอร์มินัล (Command Prompt, PowerShell หรือ Terminal) แล้วรันคำสั่ง:

   ```bash
   mkdir my-electron-app
   cd my-electron-app
   npm init -y
   npm install --save-dev electron electron-builder
สร้างไฟล์ main.js แล้วใส่โค้ดนี้:

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
สร้างไฟล์ index.html แล้วใส่โค้ดนี้:

html
คัดลอก
แก้ไข
<!DOCTYPE html>
<html>
  <head>
    <title>My App</title>
  </head>
  <body>
    <h1>Hello from Electron!</h1>
  </body>
</html>
แก้ไขไฟล์ package.json ให้เป็นดังนี้:

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
      "target": "nsis",
      "icon": "icon.ico"
    },
    "nsis": {
      "oneClick": false,
      "perMachine": true,
      "allowToChangeInstallationDirectory": true
    }
  }
}
หมายเหตุ:
ถ้าไม่มีไฟล์ icon.ico ให้ลบ "icon": "icon.ico" ในส่วน "win" ออก

ทดสอบรันแอปด้วยคำสั่ง:

bash
คัดลอก
แก้ไข
npm start
หากเจอปัญหา permission symlink บน Windows ให้ทำอย่างใดอย่างหนึ่งนี้:

เปิด Developer Mode ใน Windows:
Settings → Privacy & security → For developers → เปิด Developer Mode

หรือใช้ Command Prompt/PowerShell แบบ Administrator แล้วรันคำสั่ง:

bash
คัดลอก
แก้ไข
npm run dist
สร้างไฟล์ติดตั้ง .exe ด้วยคำสั่ง:

bash
คัดลอก
แก้ไข
npm run dist
ไฟล์ติดตั้งจะถูกสร้างในโฟลเดอร์ dist/ เช่น:

คัดลอก
แก้ไข
dist/
├── MyElectronApp Setup 1.0.0.exe
├── MyElectronApp-1.0.0.exe
├── latest.yml
