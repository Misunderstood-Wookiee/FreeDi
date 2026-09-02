# FreeDi Beacon RevH Workflow

## Summary

This branch adds Beacon RevH support and integrates a two-stage Beacon contact-calibration workflow into the Plus4, Q1 Pro, X-Max3, X-Plus3, and X-Smart3 printer configurations.

## Changes (2026-09-02)

- Added Beacon RevH configuration and machine-specific homing center positions for all supported machines.
- Preserved supported probe alternatives as commented configuration blocks:
  - Plus4 and Q1 Pro: stock `[probe]` with `[auto_z_offset]` and `[output_pin bed_sensor]`.
  - X series: stock `[probe]` or `[bltouch]`; early X-Max3 units commonly shipped with BLTouch.
- Updated the Plus4, Q1 Pro, X-Max3, X-Plus3, and X-Smart3 `PRINT_START` workflows to:
  - Purge and wipe the nozzle before probing and meshing on Plus4 and Q1 Pro. The X-series profiles retain a placeholder for a machine-specific purge and wipe routine.
  - Heat the nozzle to 150C, stabilize it for 10 seconds (`G4 P10000`), and run coarse Beacon Z-offset calibration.
  - Perform bed meshing using either KAMP adaptive meshing or the configured static mesh.
  - Heat the nozzle to 150C again, stabilize it for 10 seconds, and run fine Beacon Z-offset calibration.
  - Heat the nozzle to the requested print temperature only after fine calibration.
- Added console status messages via `RESPOND` for Beacon operations and shared final-temperature heating.
- Added clear guidance for switching probe workflows; Beacon-only commands are marked `BEACON ONLY`.
- Added a commented `AUTO_Z_LOAD_OFFSET` alternative after bed meshing for Plus4 and Q1 Pro to use the stock Z-offset workflow.
- Added X-series `PRINT_START` nozzle-preparation placeholders. No X-series purge or wipe motion is enabled until a machine-specific wiper mod and coordinates are installed and defined.

## Validation

- Confirmed Beacon is active for all five machine profiles.
- Confirmed alternative probe sections are disabled by default.
- Verified Beacon calibration command order.
- Verified Jinja blocks and `RESPOND` message quoting.
- Confirmed Beacon comments are aligned.
- Editor diagnostics report no errors.

## Deployment Note

Before using Beacon, replace the placeholder serial path in the selected `printer.cfg`:

`usb-Beacon_Beacon_RevH_YOURBEACONID-if00`

For X-series machines, define a safe purge and nozzle-wipe routine for contact calibration in `PRINT_START` not doing so may result in ooze preventing a clean contact.
