# Solar Farm static file and engineering audit

Date: 2026-11-03. Scope: `PSCAD_SolarFarm_Video_2026-10-26` only. The full 20-page MHI technical guide was read. PSCAD files and other folder contents were inspected as files. **No PSCAD session, compile, script, or simulation was run during this review.**

## Complete directory inventory

| Current path | Role | Proposed repository treatment |
| --- | --- | --- |
| `model/SolarFarm.pswx` | PSCAD v4.6.3 workspace linking the two cases with relative paths | Keep local; public redistribution needs review |
| `model/SolarFarm_Model.pscx` | Main farm case with PPC, solar-farm/converter module, custom components and embedded graphs | Keep local; unchanged during this review |
| `model/PV_Array_250kW.pscx` | Supporting PV characteristic case | Keep local; unchanged |
| `source/Simple Solar Farm.zip` | Official download archive, 59 KB | Provenance copy; exclude from public staging until rights cleared |
| `source/official/Simple Solar Farm/` | Extracted official workspace and two `.pscx` cases | Duplicate source reference; exclude from public staging |
| `docs/Official_Simple_Solar_Farm.pdf` | MHI's 2019 20-page model guide, 1.35 MB, including reference plots | Primary technical source; exclude from public staging until rights cleared |
| `docs/Resources.md` | Source and help links prepared earlier | Keep; review citations before publication |
| `diagnostics/compiler_2026-10-28/` | Local Fortran test source/executable, result, and diagnosis | Local-only; unrelated to model validation |
| `diagnostics/prior_build_SolarFarm_Model.gf132/` | Generated `.f`, `.dta`, `.map`, and `SConstruct` files from an earlier attempted build | Generated, stale after renaming; local-only; not evidence of a successful run |

No independent study report, presentation, input dataset, run output (`.out`), snapshot (`.snp`), post-processing file, or separately saved result figure was found. No `.git` directory or existing Git history was found in this project folder. The 1.35 MB PDF and 586 KB main case are below usual Git LFS thresholds; rights, rather than size, are the publication constraint. The archive and extracted files duplicate one another by design. The working PV case is byte-identical to the official source; the working main case differs from the official source only by prior naming substitutions (`SimpleSolarFarm` → `SolarFarm_Model`, `Simple_PPC` → `PPC`, `SimpleSF` → `SolarFarm`, and title text). This comparison supports **renaming**, not original electrical-model development.

## Proposed and final structure; path mapping

Keep `model/`, `source/`, `docs/`, and `diagnostics/` at their current paths. Add top-level `README.md`, `.gitignore`, `PORTFOLIO.md`, and `CHANGELOG.md`, plus this audit under `docs/`. **Old path → proposed path: identity for every pre-existing file.** No file was moved or renamed during the static review. The private repository includes the working model and guide with MHI attribution, while duplicate downloads and local diagnostics remain only on this computer. Do not make the repository public until redistribution rights are confirmed.

## Technical summary and evidence categories

| Statement | Source | Status |
| --- | --- | --- |
| Grid-connected solar farm with PPC at POC, PV array, boost MPPT/DC-voltage controller, DC/AC VSC, filtering, PLL, and a scaling interface for 100 units | MHI guide, pp. 1, 6–16 | Report-supported description |
| PV nominal irradiance 1,000 W/m², temperature 28 °C, maximum power about 0.25 MW per array | MHI guide, pp. 1, 3–5 | Report-supported operating point |
| PPC POC-voltage, power-factor, and fixed-Q modes; high/low-voltage ride-through thresholds 1.15/0.85 pu; Q limits ±0.6 pu | MHI guide, p. 3, Table 1 | Reported parameter table, not current-dialog verification |
| Solar farm: 100 units; inverter base voltage 0.65 kV line-to-line; DC base 0.93 kV; leakage 0.2 pu; P/Q ramp 1 pu/s; frequency deadband 0.4 Hz | MHI guide, pp. 7–8, Table 2 and p. 10 | Reported settings; confirm actual component values before study |
| Main case 20 s, 15 µs time step, 495 µs sample step; PV case 2.5 s, 50 µs time and sample steps | `.pscx` Settings near the top of each case | File-declared simulation settings; not executed in this review |
| Workspace references both cases by `./`-relative paths | `model/SolarFarm.pswx` | Static relationship; both targets exist |
| 100 units × 0.25 MW is about 25 MW nominal array maximum | Arithmetic interpretation of report values | Not a demonstrated AC export rating or simulation result |

The guide's PV sweep reports maximum power about 0.25 MW, open-circuit voltage 1.015 kV, and short-circuit current 0.325 kA (p. 4, Fig. 6). Its farm example connects a load at 3.5 s and applies an AB-to-ground fault at 5 s; the guide states that the farm injects reactive power under its illustrated control configuration (p. 17, Fig. 23). These are **MHI's reported findings**. The folder has no generated results to independently assess them, no validation against measured equipment, and no student-authored results report.

## Case, component, and path map

`SolarFarm.pswx` → `SolarFarm_Model.pscx` (main) + `PV_Array_250kW.pscx` (supporting array sweep). The main case embeds `PPC`, `SolarFarm`, `PI_AntiWindUp`, `LLTX_SCALER`, `deadband`, `FaleedMultimeter`, `Main`, and `Station` definitions and uses PSCAD `master:` components. The supporting case contains its `Main` and `Station` definitions. No separate custom source library, DLL, external model, MATLAB or Python integration, or standalone input data was found in the working model folder. The generated Fortran under `diagnostics/` is build output, not hand-authored source.

Human execution workflow: open the workspace in a compatible PSCAD installation → inspect actual component parameters and event switches → choose a study copy and configuration → select a supported compiler → build → run → inspect graph frames and output → document settings and compare with MHI's reference figures. This workflow is **instructions for a future human run**, not a record of completed steps.

## Discrepancies, dependencies, and risks

- The guide names `SimpleSolarFarm.pscx`; the working case is `SolarFarm_Model.pscx` after earlier naming edits. The guide also refers to `PV_Array_Setup_250kW.pscx`, while the actual supporting file is `PV_Array_250kW.pscx`. Open the workspace's actual paths.
- Main case `startup_filename` is an absolute path on an older `C:\Documents and Settings\farid\...` machine to `Active_Rect_10kVA.emt\runtime.snp`. It is machine-specific and unrelated in name to this farm. The case's `StartType=0` suggests ordinary start, but PSCAD semantics and runtime impact have not been checked here. Propose clearing or replacing the path **only after** inspecting the setting in PSCAD and obtaining approval for a model-setting change.
- The guide targets PSCAD X4 v4.6.3, as do the case headers. This machine reportedly has PSCAD Free 5.1 and GFortran 13.2 from an earlier diagnostic. Compatibility, compiler choice in PSCAD, license limits, and case build status remain unconfirmed by this review.
- Prior generated build files retain old names and cannot establish that the renamed case builds or runs. A standalone compiler test in `diagnostics/` is not a PSCAD run.
- MHI's PDF states **Copyright © 2019 Manitoba Hydro International Ltd. All Rights Reserved.** No permission to redistribute the model, source archive, PDF, or embedded figures was found. The lecture video is also a third-party teaching source. Do not treat availability for download as a public-republication license.
- The student describes this as a solo project but supplied no separate report, modified electrical case, run outputs, or detailed contribution record. The observed working-file changes are naming only and were made in an earlier assistant session. The portfolio text must not claim original model design, verified simulations, or authored guide results.
- No large file currently requires Git LFS. If validated raw time-series outputs are later included, assess size and reproducibility before choosing Git LFS or an external data release.

## License recommendation

Do not add a blanket license to the folder while third-party rights are unresolved. For original student-authored notes, consider CC BY 4.0; for any independently authored code, consider MIT. Keep MHI assets under their own terms or link to the official download. No license file was added.
