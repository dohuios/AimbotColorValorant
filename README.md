# Aimbot Valorant Project

This is an educational project implementing a color-based aimbot for Valorant, using ImGui, OpenCV, and a kernel-mode driver. **Do not use in live games, as it violates Valorant's terms of service and may result in bans.**

## Prerequisites
- Windows 10/11 (x64)
- Visual Studio 2022 with Desktop development with C++ and Windows Driver Kit (WDK)
- Visual Studio Code with C/C++ extension
- Visual C++ Redistributable 2015-2022 (x64/x86)
- OpenCV 4.8.0
- ImGui (included in src/imgui)

## Setup
1. **Install Dependencies**:
   - Download Visual Studio 2022: https://visualstudio.microsoft.com/
   - Install Visual C++ Redistributable: https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist
   - Download OpenCV 4.8.0: https://opencv.org/releases/
     - Extract to `AimbotProject/opencv`
     - Set environment variable `OPENCV_DIR` to `C:\AimbotProject\opencv\build`
   - Download ImGui: https://github.com/ocornut/imgui
     - Copy files to `AimbotProject/src/imgui`

2. **Project Structure**:

AimbotProject/
   ├── src/
   │   ├── Aimbot.cpp
   │   ├── AimbotDriver.c
   │   ├── imgui/
   ├── opencv/
   ├── .vscode/
   │   ├── tasks.json
   │   ├── launch.json
   ├── bin/
   └── README.md


3. **Build User-Mode (VS Code)**:
- Open `AimbotProject` in VS Code
- Set `OPENCV_DIR` and `DIRECTX_SDK` environment variables
- Press `Ctrl+Shift+B` to build
- Output: `bin/Aimbot.exe`

4. **Build Driver (Visual Studio 2022)**:
- Create an Empty WDM Driver project named `AimbotDriver`
- Add `src/AimbotDriver.c`
- Build for Release, x64
- Output: `x64/Release/AimbotDriver.sys`

5. **Sign Driver**:
```cmd
bcdedit /set testsigning on

   (Optional) Sign with certificate:

signtool sign /f certificate.pfx /p password /t http://timestamp.digicert.com x64/Release/AimbotDriver.sys

Usage
uninstall FACEIT for testing

Test in Custom Game or Training Mode
Install Driver:
cmd
sc create AimbotDriver binPath= "C:\AimbotProject\x64\Release\AimbotDriver.sys" type= kernel
sc start AimbotDriver
Run Aimbot:
Copy opencv_world480.dll to bin/ or C:\Windows\System32

Run bin/Aimbot.exe as administrator

Configure via ImGui:
Aimbot: Enable, FOV, smoothness, speed, delay, key

Aim Assist: Similar to aimbot

Triggerbot: FOV X/Y, delay, sleep, key

Offset: Head Offset X/Y for headshots
In-Game:
Press assigned keys (e.g., LButton for aimbot, CapsLock for always aim)

Triggerbot auto-fires when crosshair is on purple target
Head Offset Tuning
Head Offset X: Horizontal adjustment (-: left, +: right). Start at 0.0.

Head Offset Y: Vertical adjustment (-: up, +: down). Start at -10.0.

Test in Training Mode:
If aiming at body, decrease Y (e.g., -10.0 to -12.0)

If off left/right, adjust X (±1.0 to ±3.0)
Typical values: X = 0.0, Y = -8.0 to -15.0 (depends on resolution)

License
For educational use only. No warranty provided.
