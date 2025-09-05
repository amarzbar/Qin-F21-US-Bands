# Qin F21 Pro - US LTE Band Unlock Guide

**Original Author:** anon97982153  
**Date:** April 3  
**Based on method by:** XDA Forums user CatStoleTheCrown

## Overview
Unlock LTE Bands 2, 4, 12, 13, 17, 66, 71 (from the US Qin F30 Kosher)

## ⚠️ Disclaimer
Proceed at your own risk. Flashing or modifying your device could result in a non-working (bricked) phone if done incorrectly. Backup everything and be cautious.

## Requirements

### Hardware/Software
- **Windows PC** (Only works on Windows)
- **Qin F21 Pro** with:
  - Unlocked bootloader
  - TWRP installed
  - Follow this thread: [Unlock + TWRP Guide]

### Tools Needed
- **SP Flash Tool** (included in above guide)
- **ADB** (Download & know how to use it): [ADB Setup]
- **Files package** (provided by CatStoleTheCrown): Download `F30_US_LTE_Bands_Package.zip`

### Prerequisites
You only need to follow the above-linked custom firmware guide up to the point of flashing `boot_2.img` in TWRP – rooting is optional.

## Step-by-Step Guide

### Step 1: Backup Identifiers
1. Go to **Settings > About Phone**
2. Write down the following (use included .txt file):
   - IMEI
   - WiFi MAC Address
   - Bluetooth Address

### Step 2: Boot into TWRP
1. Power off the phone
2. Hold the following buttons simultaneously:
   - **Heart/Owl button** (top left)
   - **Star button** (bottom left)
3. Keep holding until you see the Douqin logo and enter TWRP

### Step 3: Backup Original NV Partitions via ADB
1. Connect phone via USB (TWRP allows ADB access)
2. Run the following commands:
   ```bash
   adb pull /dev/block/by-name/nvdata
   adb pull /dev/block/by-name/nvram
   adb pull /dev/block/by-name/nvcfg
   ```
3. **Save these files somewhere safe** – they contain your unique hardware identifiers!

### Step 4: Power Off the Device
In TWRP, tap **Reboot > Power Off**

### Step 5: Flash LTE Band Partitions via SP Flash Tool
1. Launch SP Flash Tool
2. Load the scatter file: `MT6761_Android_scatter - edited.txt`
3. **Uncheck everything except:**
   - nvcfg
   - nvdata
   - nvram
   - md1img_a

   > ⚠️ **Important:** Uncheck preloader! It must be present for flashing, but should NOT be flashed.

4. Ensure the file paths for each are set correctly
5. Click **Download** (green arrow)
6. With phone powered off, hold **Back button** (top right) and plug in the USB
7. Flashing should begin. Wait for success confirmation

### Step 6: Restore Identifiers via SN Write Tool
1. Open **SN Write Tool**
2. Set:
   - **ComPort:** USBVCOM
   - **Target Type:** Smart Phone
3. Click **System Config**
4. Under **Write Option**, check:
   - IMEI
   - BT Address
   - WiFi Address
5. Under **Database File:**
   - Check both "Load AP DB from DUT" and "Load Modem DB from DUT"
6. Click **MD1_DB** and choose: `MDDB_InfoCustomAppSrcP_MT6761_S00_...EDB`
7. Click **AP_DB** and choose: `APDB_MT6761_S01__W1947...`
8. Click **Save** and return to main window
9. Click **Start** and enter:
   - IMEI (without spaces)
   - BT Address (without colons)
   - WiFi Address (without colons)
10. Hold **Back button**, plug in phone, and click **OK**
11. Wait for **Green PASS** confirmation

> **Note:** If a second window pops up, just close it if you already saw PASS.

### Step 7: Boot Up & Verify
1. Turn on your phone
2. Go to **Settings > About Phone** and ensure:
   - IMEI is correct
   - WiFi MAC is correct
   - Bluetooth MAC is correct

#### Check Active Bands:
1. Dial: `*#*#3646633#*#*`
2. Navigate to **Band Mode**
3. Scroll to confirm bands **2, 4, 12, 13, 17, 66, 71** are active

## Important Notes

### Safety Reminders
- **BACKUP** your partitions and identifiers before doing anything
- If you skip SN Write Tool, you'll get dummy identifiers that may conflict with other devices
- This method does not unlock your bootloader — you must already have it unlocked

### Carrier Compatibility
Band coverage includes:
- T-Mobile
- Verizon  
- Some AT&T support, depending on region

## Credits
Huge credit to **CatStoleTheCrown** on XDA Forums for this amazing work in enabling US LTE compatibility on the Qin F21 Pro.

---
*Source: XDA Forums | Qin F21 Pro Topic | F30 Network Files*
