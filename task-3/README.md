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

Design a hardware-only precharge controller for a Formula SAE electric vehicle. The controller must safely charge the inverter DC-link capacitor before connecting the traction battery directly to the inverter.

The design must use discrete analog electronics and logic components. Microcontrollers, FPGAs, CPLDs, and other programmable logic devices are not permitted.

The design must include a complete schematic, component selection, analytical calculations, and functional timing diagrams.

### Overview

#### Traction system

- Traction-system (TS) voltage: 400–600 V DC.
- DC-link capacitance: 500 µF nominal.
- The DC-link capacitor is initially discharged before every precharge attempt.
- No external load current is drawn during precharge.
- Maximum continuous current through the main AIRs after precharge: 5 A.
- The battery source and auxiliary supply share a common low-voltage reference, but the TS and DC-link voltage-sensing circuits must provide the isolation required by the applicable Formula Student rules.

#### Controller supplies and signals

- low voltage supply: unregulated 16–24 V DC.
- Shutdown-circuit supply: 12 V DC.
- ENABLE input: external CMOS logic signal referenced to controller ground.
- The auxiliary supply and TS voltage are established before ENABLE is asserted.
- The shutdown circuit is the safety-related supply and must be incorporated into the relay-control architecture.
- The controller must remain functional over the full specified auxiliary-supply range.

### Specs

The controller operates three normally open relays (AIR = accumulator insulaton relay):

- AIR−: connects the negative battery pole to the inverter DC-link negative terminal.
- AIR+: connects the positive battery pole directly to the inverter DC-link positive terminal.
- Precharge relay: connects the positive battery pole to the DC-link positive terminal through a series precharge resistor.
- The precharge branch is connected in parallel with AIR+.
- All three relays must be selected and driven using a consistent, documented coil-voltage and driver architecture. Relay contacts and -insulation must be suitable for the 400–600 V DC traction system.
- All three relays coils must be driven by shutdown supply.

Assume **ENABLE** is low at power-up. An external test setup restores the DC-link to 0 V between attempts; you do not need to design a discharge circuit.

The **controller** must implement the following behaviour:

- Must start precharge sequence only if ENABLE is asserted high after checking shutdown supply is present.
- Must open all relays if enable goes low for more than 50ms
- Must open all relays after maxium 250ms if shutdown supply or Low voltage supply goes low. 
- The dc-link must reach 95% of TS voltage within 10 seconds under all specified operating conditions, including component tolerances.
- No programmable logic is allowed.
- The precharge current must never exceed 1 A at the maximum source voltage, including the selected resistor's tolerance.

#### Precharge sequence

After ENABLE is asserted and shutdown supply is present:

- Close AIR−.
- Close the precharge relay while keeping AIR+ open.
- Charge the DC-link capacitor through the precharge resistor. 
- Close AIR+.

Select the relays and precharge resistor. Calculate the voltage-divider values and nominal threshold, initial current including resistor tolerance, nominal charge time, and resistor pulse power, energy and average dissipation. Include capacitor tolerance for the energy rating. Justify relay and driver ratings, the supply's current budget and regulator dissipation.


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
- Include a short explanation of the circuit, component choices and calculations inside `docs/`, together with annotated timing diagrams or simulations covering successful precharge at 24 V and 48 V, completion memory, removal of **ENABLE** before and after completion, a new attempt, power-up and loss of supply. Simulations are not mandatory; explain how the schematic produces the expected behaviour.
- If you also design a PCB, export the production Gerber files inside `output/`.
- If you have not already done so, submit your [application form](https://eagletrt.it/apply).
- If you have questions, contact [electronics@eagletrt.it](mailto:electronics@eagletrt.it).
- You can also visit our lab on floor -2 of Povo 2 if we are slow to reply.
- You have **2 weeks (14 days)** to work on this project. **This is a firm deadline; meeting it is part of the assessment.**

## Links

- [Website](https://www.eagletrt.it)
- [Instagram](https://www.instagram.com/eagletrt)
- [LinkedIn](https://www.linkedin.com/company/eagletrentoracingteam)
