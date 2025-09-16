# 🎛️ Popup Spool Assignment for AMS Slots

This script creates a **browser popup** in Home Assistant that lets you interactively assign filament spools to AMS (Automatic Material System) slots using **Spoolman** data.  
It provides a visual interface with four slot buttons, a picked spool selector, and a dynamic list of available spools.

---

## 🚀 What It Does
- **Copies current spool IDs** into temporary variables (`tmp_slot_1_id` … `tmp_slot_4_id`).  
- **Resets the picked spool** to `0`.  
- **Shows a popup (via Browser Mod)** that contains:
  - **4 Slot buttons**:  
    - Tap → assign the currently picked spool ID to that slot  
    - Hold → clear the slot (set to 0)  
    - Shows the current spool ID or `–` if empty  
  - **Picked Spool display** showing which spool is currently selected.  
  - **Confirm button** that runs another script (replace `script.1757699810474` with your “confirm assignment” script).  
  - **Dynamic Spool list (auto-entities)**:  
    - Displays all `sensor.spoolman_spool_*` entities.  
    - Each shows the spool’s name, ID, material, and color.  
    - Tap → set that spool as the current **picked spool**.

---

## 🛠️ Requirements
- **Home Assistant** (core)  
- **[Browser Mod](https://github.com/thomasloven/hass-browser_mod)** – for the popup UI  
- **[Spoolman](https://github.com/Donkie/Spoolman)** – spool management integration  
- **[Auto-Entities Card](https://github.com/thomasloven/lovelace-auto-entities)** – for dynamic spool listing  
- **[Button-Card](https://github.com/custom-cards/button-card)** – for the interactive slot buttons  
- Helpers in HA:
  - `input_number.tmp_slot_1_id` … `input_number.tmp_slot_4_id`
  - `input_number.spool_slot_1_id` … `input_number.spool_slot_4_id`
  - `input_number.picked_spool_id`
  - `input_boolean.awaiting_slot_selection`
 
---

## ▶️ Usage
1. Call the script `script.popup_spools`.  
2. A popup will open in your browser.  
3. Select a spool from the bottom list → it becomes the **Picked spool**.  
4. Tap a slot (1–4) to assign it, or hold to clear it.  
5. Press **Confirm** to finalize the slot assignment.  

---

## 📝 Notes
- The confirm button currently calls `script.1757699810474`.  
  Replace this with your actual “update AMS slots” script.  
- You can customize the `browser_id` field if you want the popup to always appear on a specific device.  

---

## 📜 License
MIT License – see [LICENSE](../LICENSE).
