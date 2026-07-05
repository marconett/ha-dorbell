# Measuring the Bell Voltage

One multimeter measurement at the gong terminals (**0/3** for my Grothe Gong 165) answers the two questions the sender design depends on: (1) is there voltage only while the button is pressed, and (2) does it stay constant for the whole press?

## Safety

- Measure **only** at gong terminals 0 and 3 (8–12 V AC).
- **Never** measure on the mains/230 V side of the bell transformer.
- The system must be powered on.

## Multimeter setup

1. Mode: **AC voltage** (V~ / ACV, not DC).
2. Range: 20 V~ or autorange.
3. Leads: black in **COM**, red in **VΩ** (not the current/"A" jack).
4. Enable **min/max** if available, it catches short spikes.

## Procedure

1. **Idle:** probes on terminals 0 and 3 (polarity irrelevant), nobody ringing. Note the value.
2. **Press and hold** the doorbell button (easiest with two people). Keep the probes in place.
3. **Watch the display for 3–5 s** while holding, the meter needs ~1 s to settle. Note how high the value goes and whether it holds steady or drops.
4. Cross-check with a few short presses and one long press.

## Interpreting the result

**Question 1: idle vs. pressed:**

- **Idle ≈ 0 V, pressed ≈ 8–12 V** -> ideal case, the sender design works as-is. ✅
- **Idle low (2–4 V), pressed clearly higher** -> standing voltage present; the module would need permanent power plus a threshold trigger (transistor + Zener). Design change required.
- **Idle ≈ pressed** -> the terminals reveal nothing about ringing; power/trigger from the bell wires is impossible. Use a battery-powered sensor that detects the gong physically instead.

**Question 2: while held:**

- **Value stays constant for the whole press** -> the module is powered (and transmits) continuously while ringing, as the design assumes. ✅
- **Only a brief spike, then back to ~0 V despite holding** -> only a short pulse; a larger buffer capacitor or different trigger logic would be needed.

## Notes

- Also check once in **DC mode**: a significant DC reading at idle points to a different wiring scheme. Investigate before building.
