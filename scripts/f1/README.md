# F1 Session Sensors (Home Assistant)

A template sensor that unifies multiple F1 sources into clear, UI friendly states.

## What’s included

- [**F1 Sessions**](./f1_sessions)
  Progress aware, current vs next session, countdowns, local times, and per session status.
  - State shows the next session with a human readable countdown
  - Attributes include `progress`, `espn_prog`, `current_session_name`, `next_session_name`, `*_seconds_left`, `*_local_start`, `weekend_type`, and per session `*_status`

---

## Requirements
- Home Assistant Template integration enabled
- [ESPN Team Tracker](https://github.com/vasqued2/ha-teamtracker) integration for F1
- [F1 Sensor](https://github.com/Nicxe/f1_sensor) integration
- F1 sensors already available in your setup from [F1 Sensor](https://github.com/Nicxe/f1_sensor):
  - `sensor.f1_session_status` (live, ended, finished, finalized, pre, suspended)
  - `sensor.f1_track_status` (CLEAR, YELLOW, RED, VSC, SC)
  - `sensor.f1_flag` attributes: `Track flag`, `Sc mode`
  - `binary_sensor.f1_safety_car` (on when SC is deployed)
  - `sensor.f1_sessions` with per session seconds and local start attributes
  - `sensor.f1_next_race` attributes for session start datetimes
  - Optional: `sensor.f1_last_race_results` for winner text

> If your entity names differ, update them in the YAML.

---

## Notes

Time handling uses as_datetime(...).astimezone(now().tzinfo) so countdowns and labels are local.

If your data source uses finalized vs finished, both paths are handled by progress_full.
