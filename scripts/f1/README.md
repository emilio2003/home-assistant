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

---

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

---

## Entities created

sensor.f1_session_state

state: CHEQUERED | RED | Virtual Safety Car | SAFETY CAR | YELLOW | GREEN | UNKNOWN

attributes:

track_status, safety_car

is_chequered, is_red, is_vsc, is_safety_car, is_yellow, is_green

sensor.f1_sessions

state: friendly next session countdown, for example:
Qualifying in 1h 23m

key attributes:

progress, espn_prog, progress_full

current_session_name, current_session_local_start

next_session_name, next_session_seconds, next_session_local_start

weekend_type (Race week, Sprint week, No race this week)

Per session: fp1|fp2|fp3|sprint_quali|sprint|quali|race
each with *_seconds_left, *_local_start, *_status
where status is In Progress, Starting, Scheduled Later, Ended, or Not Scheduled

---

## Notes

Priority in F1 Session State: finished, red, VSC, SC, yellow, green, unknown.

Time handling uses as_datetime(...).astimezone(now().tzinfo) so countdowns and labels are local.

If your data source uses finalized vs finished, both paths are handled by progress_full.
