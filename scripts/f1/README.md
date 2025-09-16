# F1 Session Sensors (Home Assistant)

Two template sensors that unify multiple F1 sources into clear, UI friendly states.

## What’s included
- **F1 Session State**  
  Normalizes track and session flags into one readable state:
  - `CHEQUERED`, `RED`, `Virtual Safety Car`, `SAFETY CAR`, `YELLOW`, `GREEN`, `UNKNOWN`
  - Attributes expose raw values and booleans for quick theming

- **F1 Sessions**  
  Progress aware, current vs next session, countdowns, local times, and per session status.
  - State shows the next session with a human readable countdown
  - Attributes include `progress`, `espn_prog`, `current_session_name`, `next_session_name`, `*_seconds_left`, `*_local_start`, `weekend_type`, and per session `*_status`

## Requirements
- Home Assistant Template integration enabled
- F1 sensors already available in your setup:
  - `sensor.f1_session_status` (live, ended, finished, finalized, pre, suspended)
  - `sensor.f1_track_status` (CLEAR, YELLOW, RED, VSC, SC)
  - `sensor.f1_flag` attributes: `Track flag`, `Sc mode`
  - `binary_sensor.f1_safety_car` (on when SC is deployed)
  - `sensor.f1_sessions` with per session seconds and local start attributes
  - `sensor.f1_next_race` attributes for session start datetimes
  - Optional: `sensor.f1_last_race_results` for winner text

> If your entity names differ, update them in the YAML.

## Install
1. Save the YAML into `config/templates/f1.yaml` (or your templates folder).
2. In `configuration.yaml`, include templates if not already:
   ```yaml
   template: !include_dir_merge_list templates
