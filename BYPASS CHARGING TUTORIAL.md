# Bypass Charging Tutorial

## Overview
Bypass charging allows your device to run directly from the charger power without charging the battery. This feature helps prevent battery degradation during extended gaming or heavy usage sessions.

---

## Prerequisites
- XtraAether Kernel must be installed
- Root access (Magisk/KernelSU)
- Vendor and vendor_dlkm partitions must be mounted as read-write (not read-only)

---

## Installation Steps

### 1. Extract Kernel Module
- Extract or open the XtraAether Kernel ZIP file
- Navigate to the `modules` folder
- Locate the file: `qti_battery_charger_main.ko`

### 2. Copy Module to System
Copy the module file to both locations:
```
vendor/lib/modules/qti_battery_charger_main.ko
vendor_dlkm/lib/modules/qti_battery_charger_main.ko
```

### 3. Reboot Device
Reboot your phone to load the new kernel module.

---

## Usage

### Enable Bypass Charging
```bash
su -c "echo 1 > /sys/class/qcom-battery/bypass_charging_enable"
```

### Disable Bypass Charging
```bash
su -c "echo 0 > /sys/class/qcom-battery/bypass_charging_enable"
```

### Check Current Status
```bash
su -c "cat /sys/class/qcom-battery/bypass_charging_enable"
```
- Output `1` = Bypass charging enabled
- Output `0` = Normal charging mode

---

## Important Notes

### Safety Features
- Thermal-based current limiting is automatically applied
- The kernel monitors temperature to prevent overheating
- Bypass charging will automatically disable if temperature exceeds safe limits

### Real-World Testing
Tested on AxionOS 2.5 (Android 16) with Delta Force:
- Gaming duration: 15-20 minutes
- Battery level: 45% to 46% (minimal increase)
- Result: Battery charging is significantly slowed during heavy gaming
- Behavior: Similar to Vivo iQOO Z10 bypass charging implementation

This demonstrates that bypass charging is working correctly - the device runs primarily on charger power while minimizing battery charging during intensive tasks.

### When to Use
- Extended gaming sessions
- Video streaming while charging
- Heavy workload scenarios
- When you want to preserve battery health

### When NOT to Use
- When you need to charge the battery
- During normal daily usage
- If device temperature is already high

### Battery Health Benefits
- Reduces charge cycles
- Prevents heat buildup during charging
- Extends overall battery lifespan
- Maintains optimal battery temperature

### Similar Implementations
This bypass charging implementation works similarly to:
- Vivo iQOO Z10 bypass charging
- ASUS ROG Phone bypass charging mode
- Other gaming-focused devices with battery protection

---

## Troubleshooting

### Module Not Loading
1. Verify vendor partitions are mounted read-write
2. Check if module file exists in both locations
3. Ensure correct file permissions (644)
4. Reboot device

### Bypass Not Working
1. Verify kernel module is loaded:
   ```bash
   lsmod | grep qti_battery_charger
   ```
2. Check sysfs node exists:
   ```bash
   ls -la /sys/class/qcom-battery/bypass_charging_enable
   ```
3. Ensure you have root access

### Device Overheating
- Bypass charging will automatically disable
- Remove case if using one
- Reduce screen brightness
- Close background apps
- Allow device to cool down

---

## Advanced Usage

### Create Toggle Script
Create a script to easily toggle bypass charging:

```bash
#!/system/bin/sh
# bypass_toggle.sh

BYPASS_PATH="/sys/class/qcom-battery/bypass_charging_enable"
CURRENT=$(cat $BYPASS_PATH)

if [ "$CURRENT" = "1" ]; then
    echo 0 > $BYPASS_PATH
    echo "Bypass charging disabled"
else
    echo 1 > $BYPASS_PATH
    echo "Bypass charging enabled"
fi
```

### Automatic Enable on Charger Connect
Use Tasker or similar automation app:
- Trigger: Power Connected
- Action: Run shell command (enable bypass)

---

## Compatibility
- Device: Xiaomi POCO F5 (Marble)
- Chipset: Snapdragon 7+ Gen 2
- Android: 14 - 16
- ROM: AOSP-based ROMs
- Kernel : XtraAether-Mamad-Ibn-Solowie or latest future

---

## Credits
- Xtra Manager Software Community
