# Duress Protocol (Emergency Trigger)

As per Founder-Security-Policy (2026-03-14), Lockless-Core implements an automated emergency response system.

## Trigger Mechanism
- If a pre-defined "Duress PIN" is entered, the KDF derives a valid-looking but decoy-key.
- Simultaneously, a background process is initiated to broadcast an emergency signal.

## Actions
- **Location Data:** If available, coordinates are attached to the signal.
- **Silent Alarm:** The signal is sent through stored channels (Email-Bridge) without visual feedback on the device.
- **Memory Wipe:** Immediate clearing of all sensitive buffers in RAM.
