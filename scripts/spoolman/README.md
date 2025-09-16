# AMS Spool Management for Home Assistant + Spoolman

This collection of scripts integrates **Bambu Lab AMS trays** with **Spoolman** inside Home Assistant.  
It provides an end-to-end workflow for assigning spools to slots, confirming assignments, and updating filament usage automatically after prints.

---

## Scripts Included

### 1. Popup Spools
- Opens a **Browser Mod popup** to assign spools to AMS slots interactively.  
- Features:
  - 4 slot buttons (tap = assign picked spool, hold = clear slot).  
  - Dynamic list of spools from Spoolman (`sensor.spoolman_spool_*`).  
  - “Picked Spool” display and **Confirm button**.  
- Uses `input_number.tmp_slot_*` helpers to store temporary slot selections.  
- Starts selection mode with `input_boolean.awaiting_slot_selection`.

### 2. Apply Temporary Slots
- Confirms the spool assignments made in the popup.  
- Copies values from:
  - `input_number.tmp_slot_1_id` → `input_number.spool_slot_1_id`  
  - … (slots 2–4 as well)  
- Turns off `input_boolean.awaiting_slot_selection`.  
- Closes the popup with **Browser Mod**.  
- Mode set to `restart` so running it resets cleanly.

### 3. Update Spool Weights
- Updates Spoolman’s spool usage after a print finishes.  
- Reads `sensor.a1_print_weight` attributes for AMS 1 Tray 1–4.  
- Extracts used grams (`12.3 g` → `12.3`).  
- Maps trays → spool IDs (`input_number.spool_slot_*_id`).  
- For each slot:
  - Sends a **mobile notification** with slot, spool ID, and grams used.  
  - If valid spool ID and usage > 0 → patches Spoolman (`spoolman.patch_spool`)  
    - Increments `used_weight`.  
    - Updates `last_used` timestamp.

---

##  Requirements

- **Home Assistant** (core)  
- **[Spoolman](https://github.com/Donkie/Spoolman)** integration (`spoolman.patch_spool`)  
- **[Bambu Lab integration](https://github.com/greghesp/ha-bambulab)** for `sensor.a1_print_weight`  
- **[Browser Mod](https://github.com/thomasloven/hass-browser_mod)** – for popup UI  
- **[Button-Card](https://github.com/custom-cards/button-card)** – slot buttons  
- **[Auto-Entities Card](https://github.com/thomasloven/lovelace-auto-entities)** – dynamic spool list 
- Home Assistant Helpers:
  - `input_number.tmp_slot_1_id` … `input_number.tmp_slot_4_id`  
  - `input_number.spool_slot_1_id` … `input_number.spool_slot_4_id`  
  - `input_number.picked_spool_id`  
  - `input_boolean.awaiting_slot_selection`

---

##  Workflow

1. **Assign Spools**  
   - Run `script.popup_spools`.  
   - Pick a spool → tap slot button → assign spool.  
   - Press **Confirm** → runs `script.apply_tmp_slots`.

2. **Confirm Assignments**  
   - Temporary slot IDs are copied to permanent slot IDs.  
   - Selection mode ends, popup closes.

3. **Update Usage**  
   - After a print, run `script.update_spool_weights`.  
   - Spoolman is patched with grams consumed.  
   - Phone receives a notification per slot.

---

## Notes
- Replace `notify....` with your own notifier entity.  
- `browser_id` can be changed or removed if you want popups to appear on all devices.  
- The scripts are modular: you can run `Update Spool Weights` independently.  
- Regex in the update script ensures weights like `"12.3 g"` are converted to numbers.

---

## License
MIT License – see [LICENSE](../LICENSE).
