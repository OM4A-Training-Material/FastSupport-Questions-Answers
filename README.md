# ❓ Questions & Answers by Model

---

## 🧮 GENeSYS-MOD

**Q: How do I install GENeSYS-MOD and do I need any licenses?**\
A: To install, follow the [Installation Guide](https://genesysmod.readthedocs.io). You do not need any licenses to run the model—everything is open-source. If your institution provides access to a commercial solver (e.g. Gurobi), you are welcome to use it.

**Q: How do I fill the Excel input datasets—where do I find templates and naming conventions?**\
A: Templates and conventions are available in the Input Data Guide and Hourly Data Guide at [this repository](https://github.com/OM4A-Training-Material).

**Q: What switches and configuration options are available, and how do they affect model behaviour?**\
A: The Run Guide explains all configuration options. Access it [here](https://docs.google.com/document/d/1LI9mHE5MGleJ4G8OTMvSU3DDtScnruNpQI6xX-WcEyQ/edit?usp=sharing). A mirror will soon be available on ReadTheDocs.

**Q: Which solvers are supported (Gurobi, CPLEX, HiGHS, Ipopt), and how do I choose or configure them?**\
A: All solvers except CPLEX can be used. Specify your chosen solver in the run-file—you can change it at any time.

---

## ⚡ openTEPES

**Q: How can I install it?**\
A:

- openTEPES works on both Windows and Ubuntu.
- Installation guides are available here:
  - [ReadTheDocs](https://opentepes.readthedocs.io/en/latest/Download.html)
  - [PDF Installation Manual](https://pascua.iit.comillas.edu/aramos/openTEPES_installation.pdf)
- Recommended solvers:
  - **Gurobi** (free academic license)
  - **HiGHS** (open-source)
  - **GAMS/CPLEX** (if licensed)

**Q: What PC do I need?**\
A:

- Depends on the case study:
  - Time (periods, load levels)
  - Network complexity
  - Stochasticity
  - Binary variables
- Rule of thumb: 1 GB RAM per 1 million optimization rows.
- Example: Case studies provided can run on a laptop with 16 GB RAM.

**Q: What are the first steps after installing?**\
A:

- Try the 7 bundled case studies.
- Check system memory if any case does not run.

**Q: What common issues should I check for?**\
A:

- All defined items must appear in the corresponding dictionary files.
- At least two nodes and one transmission line must be defined.
- At least one generator must be defined.
- All demands must be linked to connected nodes.

**Q: How can I simplify or reduce my input data for test runs?**\
A:

- Remove durations in `oT_Data_Duration` after 168 hours.
- Use 2–3 hour time steps in `oT_Data_Parameter`.
- Use scenarios with 0.0 probability or periods with 0.0 weight.
- Leave the node column empty or set the start year beyond study year to ignore generators/lines.
- Empty cells in CSVs are read as 0.0; for solar PV at night, insert 0.000001 explicitly.
- Unused columns can be left out of CSV input files.

**Q: How do I analyze the outputs?**\
A:

- Ensure solver reached optimality (check logs).
- If not optimal, relax tight constraints.
- Check output balance files: energy not served, curtailment, tech outputs.
- Drill into area-level results if system-level outputs look off.

---

## 🧰 InfraFair

**Q: Are there any operating system requirements to run InfraFair?**\
A: No. You can run InfraFair on any machine that has Python (version higher than 3.8) installed.

**Q: How can InfraFair be installed?**\
A: After ensuring Python is installed, use the following command:\
`pip install InfraFair`

**Q: How can InfraFair be run?**\
A: You can run InfraFair in two ways:

- Locate the main code with: `pip show InfraFair`
- Or call the function directly in your script with:

```python
from InfraFair.InfraFair import InfraFair_run
InfraFair_run()
```

(Note: You must install the package first with `pip install InfraFair`.)

**Q: What kind of input data does InfraFair require?**\
A: It needs:

- A map of network flows, injections, and withdrawals (e.g., from OpenTEPES).
- Asset-specific data (e.g., cost).
- See the full list in the [documentation](https://infrafair.readthedocs.io/en/latest/7_Input_Data.html).

**Q: What kind of assets can be modelled in InfraFair?**\
A: Any asset connecting buses and carrying flow:

- Lines, transformers, shunt capacitors/reactors, phase shifters, breakers.
- 3-winding transformers must be split into 3 lines with a virtual node.

**Q: Does InfraFair require a specific format of input data?**\
A: Yes, two `.xlsx` Excel files are required with specific column names.\
Templates: [Example on GitHub](https://github.com/IIT-EnergySystemModels/InfraFair/blob/main/Examples/EU_ex)

**Q: On which networks can InfraFair be applied?**\
A: Any energy network: electricity, gas, heat, or hydrogen.\
Required: Flow data per asset, and source/sink data for each node.

---

## 🚗 EV-PV

**Q: How do I install EVPV?**  
A: To install the EVPV-Simulator, follow the [Installation Guide](https://evpv-simulator.readthedocs.io/en/latest/user_guide/installation.html). You’ll need Python installed on your machine. Then, you can install the model using `pip`.

**Q: What are the first steps after installing?**  
A: 
- Familiarize yourself with the documentation available on [ReadTheDocs](https://evpv-simulator.readthedocs.io), YouTube tutorials, and the OM4A training platform.  
- Try running EVPV in basic mode using the "Addis Ababa Simple Example" provided.

**Q: How can I run EVPV?**  
A: EVPV can be run in two ways:  
1. **Basic usage:** via the command-line interface (CLI).  
2. **Advanced usage:** by importing EVPV into your own Python script as a package.  
More details are available on [ReadTheDocs](https://evpv-simulator.readthedocs.io).

**Q: What inputs are needed to run the model?**  
A: To run EVPV for your case study, you will need:  
- A configuration file containing all parameters specific to your case study  
- A GeoJSON file with the boundary of your region of interest  
- A TIFF file representing the residential population distribution  
- Two CSV files listing the latitude and longitude of workplaces and other POIs

**Q: How long does it take for the model to run?**  
A: It depends on several factor, such as:
- The number of traffic zones  
- Whether OpenRouteService (ORS) is used for routing  
- The number of EVs simulated  
- The number of days considered for EV-PV complementarity analysis  

As a reference, the Addis Ababa examples typically run in under 2–3 minutes on a standard laptop.

**Q: Where can I find details about the methodology?**  
A: See the documentation on [ReadTheDocs](https://evpv-simulator.readthedocs.io) and refer to the [reference paper](https://arxiv.org/pdf/2503.03671).

**Q: Is it possible to define different PV system types per location?**  
A: No. Currently, only one PV system type can be defined per simulation run (e.g., rooftop, ground-mounted with or without tracking).

**Q: What is the maximum possible spatial resolution?**  
A: There is no hard limit. However:
- Higher spatial resolution increases computation time  
- The gravity model used for commuting may not work reliably at very fine resolutions  
- Input data must also be available at the desired resolution

**Q: Will additional graphics or visualizations be added to the model?**  
A: No major additions are planned. However:
- Many raws outputs can easily be visualized using Excel or other tools  
- Spatial results are already rendered as interactive HTML maps  
- Future integration with the OM4A GIS tool will enable built-in graphical outputs
