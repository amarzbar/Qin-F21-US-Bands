*Based on the method by XDA Forums user [CatStoleTheCrown](https://xdaforums.com/m/catstolethecrown.10492659/)*  
Unlock LTE Bands 2, 4, 12, 13, 17, 66, 71 (from the US Qin F30 Kosher)

I broke each step up to make it more clear.

---

### 🚨 Disclaimer

**Proceed at your own risk.** Flashing or modifying your device could result in a non-working (bricked) phone if done incorrectly. Backup everything and be cautious.

---

## ✅ Requirements

- **Windows PC** (Only works on Windows)
- **Qin F21 Pro** with:
  - **Unlocked bootloader**
  - **TWRP installed**
    - Follow this thread: [Unlock + TWRP Guide](https://xdaforums.com/t/tools-mod-scripts-mlgmxyysds-qin-f21-pro-unlock-tool.4368277/)
- SP Flash Tool (included in above guide)
- ADB (Download & know how to use it):  
  [ADB Setup](https://www.xda-developers.com/install-adb-windows-macos-linux/)
- **Files package (provided by CatStoleTheCrown)**  
  📦 [Download F30_US_LTE_Bands_Package.zip](https://www.mediafire.com/file/3fba0dugos3lkdv/F30_US_LTE_Bands_Package.zip/file)

You only need to follow the above-linked custom firmware guide **up to the point of flashing `boot_2.img` in TWRP** – rooting is optional.

---

## 🔧 Step-by-Step Guide

### Step 1: Backup Identifiers

Go to **Settings > About Phone**, and **write down**:

- IMEI
- WiFi MAC Address
- Bluetooth Address

Use the included `.txt` file to record them.

---

### Step 2: Boot into TWRP

Power off the phone. Then hold:

- **Heart/Owl button (top left)**
- **Star button (bottom left)**  
  Keep holding until you see the **Douqin logo** and enter TWRP.

---

### Step 3: Backup Original NV Partitions via ADB

Connect phone via USB (TWRP allows ADB access). Run:

```bash
adb pull /dev/block/by-name/nvdata
adb pull /dev/block/by-name/nvram
adb pull /dev/block/by-name/nvcfg
```

Save these files somewhere **safe** – they contain your unique hardware identifiers!

---

### Step 4: Power Off the Device

In TWRP, tap **Reboot > Power Off**.

---

### Step 5: Flash LTE Band Partitions via SP Flash Tool

1. Launch **SP Flash Tool**
2. Load the scatter file:  
   `MT6761_Android_scatter - edited.txt`
3. **Uncheck everything** except:
   - `nvcfg`
   - `nvdata`
   - `nvram`
   - `md1img_a`

   > ⚠️ **Uncheck `preloader`!** It must be present for flashing, but **should NOT be flashed**.

4. Ensure the file paths for each are set correctly.
5. Click **Download (green arrow)**.
6. With phone **powered off**, hold **Back button (top right)** and plug in the USB.
7. Flashing should begin. Wait for **success confirmation**.

---

### Step 6: Restore Identifiers via SN Write Tool

1. Open **SN Write Tool**
2. Set:
   - **ComPort**: USBVCOM
   - **Target Type**: Smart Phone
3. Click **System Config**
   - Under **Write Option**, check:
     - IMEI
     - BT Address
     - WiFi Address
   - Under **Database File**:
     - Check both **"Load AP DB from DUT"** and **"Load Modem DB from DUT"**
   - Click **MD1_DB** and choose:  
     `MDDB_InfoCustomAppSrcP_MT6761_S00_...EDB`
   - Click **AP_DB** and choose:  
     `APDB_MT6761_S01__W1947...`
4. Click **Save** and return to main window
5. Click **Start**. Enter:
   - IMEI (without spaces)
   - BT Address (without colons)
   - WiFi Address (without colons)
6. Hold **Back button**, plug in phone, and click **OK**
7. Wait for **Green PASS** confirmation

   > If a second window pops up, just close it if you already saw PASS.

---

### Step 7: Boot Up & Verify

Turn on your phone and go to **Settings > About Phone**. Ensure:

- IMEI is correct
- WiFi MAC is correct
- Bluetooth MAC is correct

To check active bands:

1. Dial: `*#*#3646633#*#*`
2. Navigate to **Band Mode**
3. Scroll to confirm bands 2, 4, 12, 13, 17, 66, 71 are active.

---

## 📌 Notes

- BACKUP your partitions and identifiers before doing anything.
- If you skip SN Write Tool, you'll get dummy identifiers that may **conflict with other devices**.
- This method does **not unlock your bootloader** — you must already have it unlocked.
- Band coverage includes:
  - **T-Mobile**
  - **Verizon**
  - Some AT&T support, depending on region.

---

**Huge credit to [CatStoleTheCrown on XDA Forums](https://xdaforums.com/m/catstolethecrown.10492659/)** for this amazing work in enabling US LTE compatibility on the Qin F21 Pro.
