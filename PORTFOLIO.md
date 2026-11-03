# Portfolio draft: PSCAD solar farm example study

**One-line description:** Independent study and static documentation of a third-party PSCAD solar farm example with plant-level control, power converters, and grid-fault behavior.

## Project summary (100–150 words)

During my DENSYS master's studies, I examined Manitoba Hydro International's PSCAD solar farm example to understand how a grid-connected PV plant is represented for electromagnetic-transient studies. The supplied model combines a PV array, boost converter, grid-side voltage-source converter, plant controller, filters, phase-locked loop, and a scaling interface for 100 inverter units. I reviewed the technical guide and project files to map the controls, nominal operating conditions, simulation settings, and reference scenarios. The guide reports PV-array characteristics and a farm response to a load connection and an AB-to-ground fault; I have not independently reproduced those results. The working copy was renamed from the official example, but no original electrical-model change is evident in the files reviewed. **[Add your own design, analysis, or simulation contribution with evidence before making a stronger portfolio claim.]**

## Engineering challenge and approach

- **Challenge:** understand the relationships between PV-array behavior, DC-link/MPPT control, plant-level POC control, inverter current control, and fault response.
- **Approach:** read the complete MHI guide and statically inspect the workspace, two PSCAD cases, component definitions, settings, and file dependencies.
- **Contribution statement:** the student says they modeled this example as solo coursework. Personal model design, parameter changes, simulations, and conclusions are not established by the current files; the renamed working copy came from an earlier assistant action. Add a process record or independently authored case before claiming specific design achievements.
- **Tools and methods:** PSCAD/EMTDC file review, power-system and converter-control interpretation, technical documentation, provenance and publication audit. No PSCAD execution is claimed for this preparation.

## Evidence-backed highlights

- Mapped the main solar-farm case, supporting PV-array case, and PSCAD workspace links.
- Summarized PPC control modes, MPPT/DC-voltage choices, PLL-based inverter controls, and 100-unit scaling from the MHI guide.
- Recorded declared main-case 20 s / 15 µs and array-case 2.5 s / 50 µs simulation settings for a future reproducible study.
- Identified a stale machine-specific snapshot path and separated generated build files from actual simulation results.
- Documented MHI attribution and the need to confirm rights before publishing source files or figures.

**Reported results:** MHI's guide reports about 0.25 MW peak array power, 1.015 kV open-circuit voltage, 0.325 kA short-circuit current, and reactive-power injection in its illustrated POC fault scenario. These findings belong to MHI's report; none was reproduced or validated in this review.

**Skills demonstrated:** PSCAD case structure, PV and inverter control concepts, EMT study framing, technical reading, reproducibility planning, engineering documentation.

**Suggested visuals:** an original, attributed system block diagram; student-produced PSCAD traces only after an actual documented run. Do not reuse MHI figures publicly without permission.

**Suggested GitHub topics:** `pscad`, `emtdc`, `solar-farm`, `photovoltaics`, `power-systems`, `model-review`.

**CV bullet:** Studied an MHI PSCAD solar farm example and documented its PV, converter, plant-control, and fault-study structure; **[add verified original analysis or results]**.

**LinkedIn project description:** As part of my DENSYS studies, I reviewed an MHI PSCAD solar farm example and mapped its major components, controls, and simulation settings. The published guide provides reference PV and fault-response figures, which I have not independently reproduced. **[Add specific personal engineering work and results after verification.]**

**Attribution/contact placeholders:** [student name], [DENSYS institution/course], [contact], [exact original contribution], [publication permission or official-link-only approach].
