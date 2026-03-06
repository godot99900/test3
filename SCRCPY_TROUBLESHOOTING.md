# Scrcpy Video Stream Troubleshooting

If you're getting "Video stream is disconnected" error, try these fixes:

## Quick Fixes (Try in order)

### 1. Restart ADB and Scrcpy
```bash
adb kill-server
adb start-server
adb devices
```

### 2. Check Device Settings
- Enable **USB Debugging** in Developer Options
- Disable **Screen Timeout** (set to "Never")
- Enable **Stay Awake** while charging
- Disable **Sleep mode** or **Battery optimization** for system apps

### 3. USB Connection
- Use a **good quality USB cable** (not just charging cable)
- Try a different **USB port** (prefer USB 3.0 ports)
- Avoid using **USB hubs** - connect directly to PC
- Try **USB 2.0 mode** if USB 3.0 fails

### 4. Phone-Specific Issues

#### For Samsung Devices:
- Disable **Game Launcher**
- Disable **Edge Screen** features
- Set **Performance mode** in Device Care

#### For Xiaomi/Redmi:
- Disable **MIUI Optimization** in Developer Options
- Grant **USB Debugging (Security Settings)** permission
- Disable **Memory Extension/RAM Expansion**

#### For Realme/Oppo:
- Disable **System Cloning/App Cloning**
- Turn off **RAM Expansion**

### 5. Scrcpy Alternative Settings

If the current settings don't work, you can try different scrcpy parameters by editing `window_controller.py` around line 84:

**Option A - Lower Quality (More Stable):**
```python
self.scrcpy_client = scrcpy.Client(
    device=self.device,
    max_width=1280,  # Lower resolution
    bitrate=4000000,  # 4 Mbps
    max_fps=15,      # Lower FPS
)
```

**Option B - Minimal Settings:**
```python
self.scrcpy_client = scrcpy.Client(device=self.device)
```

### 6. Check for Conflicts
```bash
# Kill any existing scrcpy processes
taskkill /F /IM scrcpy.exe
```

### 7. Test Scrcpy Standalone
Download scrcpy from https://github.com/Genymobile/scrcpy/releases and test:
```bash
scrcpy --max-fps=30 --max-size=1920
```

If standalone scrcpy works but the bot doesn't, the issue is with the Python scrcpy library.

### 8. Alternative: Use Emulator Instead
If using a physical device continues to fail, consider using an Android emulator:
- **LDPlayer** (recommended)
- **BlueStacks**
- **MEmu**

Emulators typically have better ADB/scrcpy compatibility.

## Still Not Working?

1. Check your device is visible: `adb devices`
2. Check scrcpy server can start: `adb shell ls /data/local/tmp/scrcpy-server.jar`
3. Join the Discord for support (link in README)
