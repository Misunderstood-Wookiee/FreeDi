## Summary

This branch adds Beacon RevH support and integrates a two-stage Beacon contact-calibration workflow into the Plus4 and Q1 Pro printer configurations.

## Changes

- Added Beacon RevH configuration for both machines.
- Preserved stock probe and Qidi `auto_z_offset` settings as commented alternatives.
- Added machine-specific Beacon homing center positions.
- Updated both `PRINT_START` macros to:
  - Purge and wipe the nozzle.
  - Heat the nozzle to 150C for coarse contact calibration.
  - Stabilize the nozzle for 30 seconds.
  - Run coarse Beacon Z-offset calibration.
  - Perform bed meshing.
  - Heat to print temperature.
  - Run fine Beacon Z-offset calibration.
- Added console and LCD status messages for Beacon operations.
- Added clear guidance for switching between Beacon and `auto_z_offset`.

## Validation

- Confirmed Beacon is active for both machines.
- Confirmed stock probe and `auto_z_offset` sections are disabled by default.
- Verified Beacon calibration command order.
- Verified Jinja blocks and `RESPOND` message quoting.
- Confirmed Beacon comments are aligned.
- Editor diagnostics report no errors.

## Deployment Note

Replace the placeholder Beacon serial path before use:

`usb-Beacon_Beacon_RevH_YOURBEACONID-if00`
