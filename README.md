# PlantBox Command Service - Command Reference

This document describes the available serial and NFC commands for the PlantBox Arduino project, their usage, and the feedback you can expect via the serial console.

---

## General Usage

- All commands start with a `/` (slash).
- Commands can be sent via serial (USB) or via NFC (if supported).
- Most commands provide feedback via the serial console.

---

## Command List

### 1. `/alarm` - Alarm Control

- **/alarm now**
  - Triggers the alarm immediately.
  - **Feedback:** `[ALARM] Triggered now`
- **/alarm seconds <duration>**
  - Triggers the alarm for `<duration>` seconds.
  - **Feedback:** `[ALARM] For seconds: <duration>`
- **/alarm minutes <duration>**
  - Triggers the alarm for `<duration>` minutes.
  - **Feedback:** `[ALARM] For minutes: <duration>`
- **/alarm lights**
  - Triggers the alarm using lights only.
  - **Feedback:** `[ALARM] Lights alarm triggered`
- **/alarm jingle <notes>**
  - Plays a custom jingle. Format: `pitch,duration;pitch,duration;...` (e.g., `440,500;880,250;0,250`)
  - **Feedback:**
    - `[ALARM] Jingle: <notes>`
    - `[ALARM] Playing jingle with <n> notes` or `[ALARM] Invalid jingle format`

---

### 2. `/rgb` - RGB Light Control

- **/rgb on**
  - Turns the RGB lights on (white).
  - **Feedback:** `[RGB] Set to white (on)`
- **/rgb off**
  - Turns the RGB lights off.
  - **Feedback:** `[RGB] Turned off`
- **/rgb R,G,B**
  - Sets the RGB lights to the specified color (0-255 for each).
  - **Feedback:** `[RGB] Set to: R, G, B` or `[RGB] Invalid RGB values. Use 0-255 for each.`

---

### 3. `/pump` - Pump Control

- **/pump <duration>**
  - Starts the pump for `<duration>` seconds at the current max strength (from settings).
  - **Feedback:** `[PUMP] Started for <duration> seconds at max strength <value>`
- **/pump <strength> <duration>**
  - Starts the pump for `<duration>` seconds at a scaled strength (1-100, mapped between min/max in settings).
  - **Feedback:** `[PUMP] Started for <duration> seconds at scaled strength <value> (input: <strength>)`
- **/pump set min <strength>**
  - Sets the minimum pump strength (0-100) and saves to EEPROM.
  - **Feedback:** `[PUMP] Set min strength to <strength>` or error if out of range.
- **/pump set max <strength>**
  - Sets the maximum pump strength (0-100) and saves to EEPROM.
  - **Feedback:** `[PUMP] Set max strength to <strength>` or error if out of range.

---

### 4. `/soil` - Soil Sensor & Calibration

- **/soil test**
  - Reads and prints the current soil sensor value.
  - **Feedback:** `[SOIL] Test value: <value>`
- **/soil set dry**
  - Calibrates and stores the current soil value as "dry".
  - **Feedback:** `[SOIL] Set dry value: <value>`
- **/soil set wet**
  - Calibrates and stores the current soil value as "wet".
  - **Feedback:** `[SOIL] Set wet value: <value>`

---

### 5. `/reservoir` - Reservoir Sensor & Calibration

- **/reservoir test**
  - Reads and prints the current reservoir sensor value.
  - **Feedback:** `[RESERVOIR] Test value: <value>`
- **/reservoir set dry**
  - Calibrates and stores the current reservoir value as "dry" (alarm threshold).
  - **Feedback:** `[RESERVOIR] Set dry value: <value>`
- **/reservoir set wet**
  - Reads and prints the current reservoir value as "wet" (no storage).
  - **Feedback:** `[RESERVOIR] Set wet value (no storage field): <value>`

---

### 6. `/settings` - EEPROM Settings

- **/settings read**
  - Prints all settings bytes (0-22) from EEPROM.
  - **Feedback:** `[SETTINGS] EEPROM: <hex values>`
- **/settings write <23 bytes>**
  - Writes 23 bytes to EEPROM. Bytes can be separated by space, comma, or semicolon.
  - **Feedback:** `[SETTINGS] Written 23 bytes to EEPROM` or error if not enough bytes.

---

### 7. `/schedule` - Schedule a Command

- **/schedule in <seconds|minutes> <duration> <command>**
  - Schedules another command to run after the specified delay.
  - Example: `/schedule in seconds 5 alarm now` (runs `/alarm now` after 5 seconds)
  - **Feedback:**
    - `[SCHEDULE] Command scheduled in <duration> <unit>: <command>`
    - When executed: `[SCHEDULE] Executing scheduled command: /<command>`

---

## Error & Usage Feedback

- If a command is malformed or arguments are out of range, the system prints a usage message or error to the serial console.
- Unknown commands print: `[COMMAND] Unknown: <command> ARGS: <args>`

---

## Notes

- All commands are case-insensitive.
- Only one scheduled command can be pending at a time (the last scheduled command replaces any previous one).
- Settings changes (min/max pump strength, calibration, etc.) are persisted to EEPROM where applicable.

---

For further details, see the source code in `lib/commandService/commandService.cpp`.
