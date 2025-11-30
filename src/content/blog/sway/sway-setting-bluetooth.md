---
author: Taro Gray
pubDatetime: 2025-11-30T21:00:00.000Z
title: Setting bluetooth on sway
postSlug: sway-setting-bluetooth
featured: true
tags:
  - Sway
description: 
---

###Table of contents

Here is the **exact, clean, reliable sequence** to connect Bluetooth using `bluetoothctl` on Sway / Wayland / Linux.
This works on Fedora / Asahi Linux perfectly.

---

## **1. Start bluetoothctl**

Open a terminal and run:

```bash
bluetoothctl
```

You will enter the interactive prompt:

```
[bluetooth]#
```

---

## **2. Turn Bluetooth on**

```bash
power on
```

Expected output:

```
Changing power on succeeded
```

---

## **3. Enable scanning**

```bash
scan on
```

This will start printing discovered devices, like:

```
[NEW] Device AA:BB:CC:DD:EE:FF AirPods
```

💡 **Keep an eye on the MAC address**
Example: `AA:BB:CC:DD:EE:FF`

---

## **4. Pair with the device**

Use the MAC address you found:

```bash
pair AA:BB:CC:DD:EE:FF
```

If your device requires confirmation, accept it.

Expected:

```
Pairing successful
```

---

## **5. Trust the device** (recommended)

This tells Linux to auto-reconnect later:

```bash
trust AA:BB:CC:DD:EE:FF
```

Output:

```
Changing AA:BB:CC:DD:EE:FF trust succeeded
```

---

## **6. Connect to the device**

```bash
connect AA:BB:CC:DD:EE:FF
```

If it succeeds:

```
Connection successful
```

---

## **7. Optional: Stop scanning**

```bash
scan off
```

---

## **8. Exit bluetoothctl**

```bash
quit
```

---

## Common Problems

### Bluetooth is "blocked"

Check rfkill:

```bash
rfkill list
```

Unblock if needed:

```bash
sudo rfkill unblock bluetooth
```

---

### PipeWire not handling audio

Restart pipewire:

```bash
systemctl --user restart pipewire pipewire-pulse wireplumber
```

---

### Device says "Failed to connect"

Try removing and pairing again:

```bash
remove AA:BB:CC:DD:EE:FF
pair AA:BB:CC:DD:EE:FF
connect AA:BB:CC:DD:EE:FF
```

---

### Want auto-connect on boot?

I can set that up too using:

* `bluetoothctl trust`
* `systemd user service`
* or bluez-auto-connect script

---

```
If your AirPods are successfully **paired + trusted + connected**, then **audio should automatically route through PipeWire**.
But depending on the profile, Bluetooth may be connected but **not actually set as the audio output** yet.

Here’s exactly what to do so you can *hear* audio.
```

---

## ✅ Step 1 — Check that the Bluetooth connection is active

Run:

```bash
bluetoothctl info AA:BB:CC:DD:EE:FF
```

You should see:

```
Connected: yes
```

If not, reconnect:

```bash
bluetoothctl connect AA:BB:CC:DD:EE:FF
```

---

## ✅ Step 2 — Make your AirPods the audio output (PipeWire / PulseAudio)

AirPods often connect in the wrong profile first
(sometimes "headset" mode instead of "A2DP" audio mode).

Run:

```bash
pactl list sinks short
```

You should see something like:

```
bluez_output.AA_BB_CC_DD_EE_FF.a2dp-sink
```

If yes, set it as default:

```bash
pactl set-default-sink bluez_output.AA_BB_CC_DD_EE_FF.a2dp-sink
```

Then move all current audio to the AirPods:

```bash
pactl list sink-inputs short
```

You’ll see numbers like `0`, `1`, etc.

Move each:

```bash
pactl move-sink-input <ID> bluez_output.AA_BB_CC_DD_EE_FF.a2dp-sink
```

But you can shortcut this with:

```bash
pactl set-card-profile bluez_card.AA_BB_CC_DD_EE_FF a2dp-sink
```

---

## ⚠️ AirPods commonly connect in *HFP/HSP* mode (bad audio)

Fix it with:

```bash
pactl set-card-profile bluez_card.AA_BB_CC_DD_EE_FF a2dp-sink
```

This forces “High Quality Audio” mode (A2DP).

---

## 🎧 Step 3 — Test audio

Play anything:

```bash
paplay /usr/share/sounds/alsa/Front_Center.wav
```

Or open any browser → YouTube → play video.

If you hear sound: **AirPods are working**.

---

