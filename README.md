# Home Assistant Configuration by Emilio

This repository contains my full Home Assistant configuration, scripts, templates, dashboards, and automations.  
It serves as both a backup of my setup and a resource for others who want to explore advanced Home Assistant automations.

## License
MIT License – see [LICENSE](LICENSE) for details.

---
## Scripts in This Repository
### 1) [Car Automation](./scripts/climate_control)
  Automatically adjusts your Hyundai Elantra climate system based on weather (temperature, humidity, fog, snow, day/night, etc.).
  
### 2) [Spoolman (Bambu Lab AMS)](./scripts/spoolman)
Automations for **Bambu Lab AMS + Spoolman** spool management
- [Popup Spools](./scripts/spoolman/popup_spools) - Browser popup to assign spools to AMS slots.  
- [Apply Temporary Slots](./scripts/spoolman/apply_tmp_slots) - Confirms spool assignments.  
- [Update Spool Weights](./scripts/spoolman/update_spool_weights) - Updates Spoolman usage after a print.  

### 3) [F1 Session Status](./scripts/f1)
Progress aware sensors that turn raw F1 data into clear session states, countdowns, and per session status. Built for dashboards and automations.

## What you get
- [**sensor.f1_session_state**](./scripts/f1/f1_session_state) - One readable flag state: CHEQUERED, RED, Virtual Safety Car, SAFETY CAR, YELLOW, GREEN, UNKNOWN.  
  Useful for chips, badges, and quick alerts.
- [**sensor.f1_sessions**](./scripts/f1/f1_session_state) - Next session countdown in the state, with attributes for progress, current vs next, local start times, and per session status automation-friendly.
