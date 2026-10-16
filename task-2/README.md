# Recruitment for E-Agle TRT | Electronics division

Welcome to the recruitment _test_ for the electronics team of E-Agle Trento Racing Team.

This test gives us an initial understanding of applicants' abilities without the pressure of a formal exam.

It also introduces you to the tools we use, so you can get up to speed with the team's workflow before you need to use them under pressure.

## What we'll look into

- Schematic quality: clear connections, consistent labels, tidy organisation into functional blocks and good KiCad practices.
- Circuit correctness: operation that meets the requirements, suitable components and calculations that support the design.
- Technical reasoning: clear explanations of the circuit architecture, component choices and sizing that demonstrate your understanding.
- Documentation quality: clear and complete explanations, calculations and verification, consistent with the submitted schematic.
- `git` usage: fork, branch, clone, commit, push, pull.

## Assignment

Develop a Brake System Plausibility Device (**BSPD**) inspired by an electric Formula SAE car.

The **BSPD** must disable the tractive system if significant braking and high motor current occur at the same time for longer than an allowed interval.

### Overview

The **BSPD** has the following specifications:

- It is powered by an unstable DC supply ranging from 9 V to 17 V.
- It has a normally open relay whose contact permits the car's shutdown circuit to close.
- It receives analogue signals from a brake pressure sensor and a tractive-system current sensor.
- Both sensor signals are referenced to the board's ground.
- The board must provide a regulated 5 V supply for the external sensors. Their combined current consumption is at most 30 mA.

The **brake pressure sensor** has the following specifications:

- Pressure range: 0 bar to 100 bar.
- Linear output: 0.5 V at 0 bar and 4.5 V at 100 bar.
- Output impedance: at most 100 Ω.

The **current sensor** has the following specifications:

- Current range: 0 A to 100 A, representing current drawn by the inverter.
- Linear output: 0.5 V at 0 A and 4.5 V at 100 A.
- Output impedance: at most 100 Ω.

The maximum tractive-system voltage is 400 V. The sensors and the traction power path are external to the board: no high voltage or traction current must be routed through the PCB.

### Specs

The **BSPD** must open the relay when both of the following conditions remain true continuously for a nominal interval of 500 ms:

- Brake pressure is above 30 bar.
- Tractive-system current is above 12.5 A, corresponding to 5 kW at the maximum tractive-system voltage.

The current threshold is fixed: measuring the instantaneous tractive-system voltage or calculating its actual power is not required.

The **BSPD** must implement the following behaviour:

- Using nominal component values, a simultaneous event shorter than 500 ms must not cause a shutdown.
- The timer must reset when either condition is no longer present. In particular, two 250 ms simultaneous events separated by 100 ms without the simultaneous condition must not cause a shutdown.
- Once a sustained event opens the relay, the fault must remain stored even if the sensor signals return to normal. Only power cycling the board may clear it.
- At power-up, initialise the fault memory to "no fault" and the timer to zero. The relay may close once the board's supply is established. If the simultaneous condition is already present, start the same 500 ms timing interval; a separate start-up interlock is not required.
- Loss of the board's power supply must cause the relay to open.

Assume both sensors are connected and their outputs remain between 0.5 V and 4.5 V. Sensor fault detection is not required.

The relay contact switches only the low-voltage shutdown circuit, not the traction power path. Assume a maximum contact load of 24 V DC and 1 A. Select a relay with suitable DC contact and coil ratings, and include its driver and flyback protection.

No programmable logic is allowed.

Calculate the sensor voltages and resistor values for the thresholds, the nominal delay, the supply's current budget and regulator dissipation, and the relay driver's component values and ratings.

Nominal calculations are sufficient for the thresholds and timing. State the component tolerances you chose, but a complete worst-case analysis is not required. Component voltage, current and thermal ratings must still be suitable for the stated operating ranges.

For verification, use stable sensor signals away from the thresholds and treat the relay as an ideal switch in functional timing diagrams. Detailed noise immunity and mechanical switching times are not required.

## KiCad instructions

- Include at least one hierarchical sheet in the schematic.
  - _A hierarchical sheet is not necessary for a project this small, but it lets you learn how to use hierarchy without the complexity of a larger assignment._

- Write the required calculations directly on the schematic as text notes near the relevant circuit blocks. Include formulas, numerical substitutions, units and results, not just the final component values.

- Include connectors, power-supply decoupling, relay drivers and the necessary protection circuits.

- Use [Mouser](https://www.mouser.com/) as the reference catalogue for component selection. Record the manufacturer, manufacturer part number and Mouser part number or product link in the schematic fields for each selected physical component, so they can be exported in the BOM.

- Run the electrical rules check (ERC), fix unintended errors and explain any remaining warnings.

- Use JLCPCB as the manufacturing reference if you choose to design a PCB.

## General instructions

- You may use AI tools to help you understand concepts, but you must design the circuit, draw the schematic, carry out the calculations and write the documentation yourself. Any submitted work found to be AI-generated, or that you cannot explain when asked, will result in disqualification and your application will not be considered. Practices that demonstrate your authorship, such as meaningful progress commits and notes explaining your design decisions, will be appreciated.
- Create a repository on your GitHub account and copy this project into it. If you do not have an account, create one. **Do not clone this repository!**
- Use the existing KiCad project as a starting point, or create a new one for this assignment.
- Create a branch named `name_surname` from `master` and commit your progress on that branch.
- Commit your progress throughout the assignment. **Do not commit only the finished project.**
- When you are done, export the schematic inside `docs/`.
- Export a bill of materials (BOM) from KiCad as a CSV file inside `docs/`. Include component references, quantities, values, manufacturers, manufacturer part numbers and Mouser part numbers or product links.
- Include a short explanation of the circuit, component choices and calculations inside `docs/`, together with annotated timing diagrams or simulations covering normal operation, short and sustained simultaneous events, timer reset between events, fault memory, power-up and loss of supply. Simulations are not mandatory; explain how the schematic produces the expected behaviour.
- If you also design a PCB, export the production Gerber files inside `output/`.
- If you have not already done so, submit your [application form](https://eagletrt.it/apply).
- If you have questions, contact [electronics@eagletrt.it](mailto:electronics@eagletrt.it).
- You can also visit our lab on floor -2 of Povo 2 if we are slow to reply.
- You have **2 weeks (14 days)** to work on this project. **This is a firm deadline; meeting it is part of the assessment.**

## Links

- [Website](https://www.eagletrt.it)
- [Instagram](https://www.instagram.com/eagletrt)
- [LinkedIn](https://www.linkedin.com/company/eagletrentoracingteam)
