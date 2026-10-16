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

Develop a precharge controller (**controller**) inspired by the DC-link of an electric Formula SAE car.

Before connecting the battery directly to the inverter, the **controller** must charge the inverter's input capacitor through a resistor to limit the inrush current.

### Overview

The **controller** has the following specifications:

- It is powered by an unstable auxiliary DC supply ranging from 9 V to 17 V.
- It receives an external **ENABLE** signal referenced to the board's ground: 0 V means disabled and 5 V means enabled.
- It controls a normally open **main relay** that connects the source directly to the DC-link.
- It controls a normally open **precharge relay** that connects the source to the DC-link through a **precharge resistor**.
- It measures the source voltage and the DC-link voltage.

The precharge relay and resistor form a series branch connected in parallel with the main relay. The source, DC-link and auxiliary supply share a common ground.

The **source** has the following specifications:

- Voltage range: 24 V to 48 V.
- Its voltage can be considered constant during each precharge attempt.

The **DC-link** has the following specifications:

- Capacitance: 4,700 µF, with a tolerance of ±20%.
- Initial voltage: 0 V.
- No load current is drawn during precharge.
- After precharge, the main relay must support a continuous load current of 5 A.

### Specs

Assume **ENABLE** is low at power-up. The auxiliary supply must be established and the source voltage present before **ENABLE** rises. An external test setup restores the DC-link to 0 V between attempts; you do not need to design a discharge circuit.

The **controller** must implement the following behaviour:

- When **ENABLE** is low, both relays must be open and the completion memory must be reset.
- When **ENABLE** becomes high, close the precharge relay while keeping the main relay open.
- Limit the initial precharge current to at most 2 A over the full source voltage range, including the chosen resistor's tolerance.
- Command the main relay to close when the DC-link voltage reaches a nominal threshold of 95% of the source voltage. The threshold must follow the source voltage: a fixed DC-link voltage threshold is not sufficient.
- Store completion in hardware and keep the main relay closed until **ENABLE** is removed or the auxiliary supply is lost; continued operation must not depend on the comparator remaining in the same state.
- **Keep the precharge relay closed for the entire time ENABLE is high**, including after the main relay closes. The closed main relay bypasses the resistor, so a timed handover between the relays is not required.
- Removing **ENABLE** at any point must reset completion and open both relays. Loss of the auxiliary supply must also cause both relays to open.

Resetting completion when **ENABLE** is low must take priority over a simultaneous completion signal.

Assume the source, capacitor and relays operate correctly and the capacitor charges normally. A timeout or fault latch is not required.

No programmable logic is allowed.

Select the relays and precharge resistor. Calculate the voltage-divider values and nominal threshold, initial current including resistor tolerance, nominal charge time, and resistor pulse power, energy and average dissipation. Include capacitor tolerance for the energy rating. Justify relay and driver ratings, the supply's current budget and regulator dissipation.

Assume at most one precharge attempt every 10 s. Use the resistor's pulse-rating data, not only its continuous power rating, to justify the choice. The relays, resistor and DC-link capacitor may be external to the controller PCB, but their connections must be shown in the schematic.

Nominal calculations are sufficient for the voltage-ratio threshold and charge time. State the component tolerances you chose, but a complete worst-case analysis is not required beyond the current and energy checks above. Component voltage, current and thermal ratings must still be suitable for the stated operating ranges.

For verification, treat the relays as ideal switches in functional timing diagrams and neglect contact resistance in the charging calculation. Detailed noise immunity and mechanical switching times are not required. Welded-contact detection and active DC-link discharge are outside the scope of the assignment.

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
