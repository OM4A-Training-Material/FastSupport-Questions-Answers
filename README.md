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
**Q: Are there any operating system requirements to run InfraFair?**  
A: No. You can run InfraFair on any machine that has Python (version higher than 3.8) installed. Therefore, the only requirement is to have Python installed.

**Q: How can InfraFair be installed?**  
A: The simple way to install InfraFair, after making sure you have Python installed, is through the pip installation by typing the following command in the command prompt: `pip install InfraFair`.

**Q: How can InfraFair be run?**  
A: In order to run InfraFair, you can either run the main code by locating it on your machine through the command: `pip show InfraFair`, or by calling the main function of InfraFair, `InfraFair_run()`, within your Python script. For the latter, you need to import the function by including the following line of code:  
`from InfraFair.InfraFair import InfraFair_run`.  
For both options, you need to have InfraFair installed with the pip command: `pip install InfraFair`.

**Q: What kind of input data does InfraFair require?**  
A: InfraFair requires a map of flows in all the assets in the network and the injections and withdrawals for all the nodes in the network. This map of flows and nodal injections and withdrawals could be obtained from solving the network dispatch (for instance, when running OpenTEPES). In addition to these data, data about the modelled assets are required by InfraFair, for instance, the cost of each asset in the network to be allocated by InfraFair. For the complete list of input data, please refer to the model documentation: [https://infrafair.readthedocs.io/en/latest/7_Input_Data.html](https://infrafair.readthedocs.io/en/latest/7_Input_Data.html).

**Q: What kind of assets can be modelled in a case study of InfraFair?**  
A: Any asset through which energy flows and which connects two buses can be modelled in the given case study. These include electrical lines, two-winding transformers, three-winding transformers, shunt capacitors and reactors, phase shift transformers, and electrical breakers. Note that in the case of a three-winding transformer, since it connects three buses, it needs to be modelled as three lines connected to a virtual node.

**Q: Does InfraFair require a specific format of input data?**  
A: Yes. InfraFair requires the input data to be placed in two Excel files (.xlsx). The first file contains the network data and the second files contain some input variables required by the model. It is important that the names of the columns are the same for the code to process the files. An example of this template can be found here: [https://github.com/IITEnergySystemModels/InfraFair/blob/main/Examples/EU_ex](https://github.com/IITEnergySystemModels/InfraFair/blob/main/Examples/EU_ex).

**Q: On which networks can InfraFair be applied?**  
A: All energy networks involve moving energy from one point to another. This includes the electrical network, the gas network, the heat network, and potentially the hydrogen network. For any network, the flow in the line or the pipeline needs to be provided, as well as the sources/injections and the sinks/withdrawals corresponding to every point in the network.

**Q: What are the generation technologies that InfraFair accepts?**  
A: InfraFair accepts all kinds of generations. In fact, InfraFair is generation-technology-agnostic as it does not require any information about the type of generation in the network. It only requires the magnitude of power generated at each node.

**Q: How long does it take to run InfraFair and obtain results?**  
A: The runtime depends on many factors, including, among others, the capabilities of the operating machine, the size of the network, the number of snapshots and the user's choice of which results to export. You can find how long it takes to run the provided examples in InfraFair’s journal paper: [https://doi.org/10.1016/j.softx.2025.102069](https://doi.org/10.1016/j.softx.2025.102069).

**Q: If the input data is incomplete in practical project applications, how will InfraFair deal with it?**  
A: Dealing with incomplete data is beyond the scope of the software. All the mandatory data must be completely provided to execute InfraFair successfully.

**Q: What kind of technology is used to group data?**  
A: The grouping of the data in InfraFair is a simple process that does not involve technical details. Simply, all the agents (horizontal result) or assets (vertical result) belonging to a certain group (for instance, a country group) are summed up together.

**Q: What kind of user community can use the InfraFair?**  
A: The software is designed primarily as a decision support tool for the energy regulator community and can be used by researchers, policymakers, and the broader community of energy modelers and stakeholders.

**Q: How can the table in the output file SO joint overall network usage cost per SO.xlsx be read?**  
A: The rows represent the grouping of network assets belonging to the different system operators, while the columns represent the grouping of network users belonging to the different system operators. For each row, the amount indicated per column represents the cost that the agents within the network of each system operator (indicated by the column) should pay for the use of the network assets of the system operator (indicated by the row). The diagonal values, which have the same system operator indicated in the row and the column, represent how much each system operator’s agents should pay to their system operator for the use of assets within their own network.

**Q: Can InfraFair provide a solution for cost allocation?**  
A: InfraFair is a tool for cost allocation of networks, both national and regional (among different countries). It allocates the costs of the different assets in the network to the users based on their expected usage. Thus, the answer is yes, it can provide a solution for cost allocation.

**Q: Does the processing of data in InfraFair involve data normalisation?**  
A: InfraFair does not involve data normalisation. The underlying mathematical operations do not require any kind of normalization. Normalization can be performed externally after obtaining the results for the sake of, for instance, comparing the different results of countries. However, since the main purpose of InfraFair is to allocate the cost, this is not embedded currently within it.

**Q: What is the range of input data that InfraFair accepts?**  
A: InfraFair intrinsically does not have a limitation on the range of input data. The wider the range, the more processing time it will take to run the software. However, one should be aware of the practical limitations of the data format. Because InfraFair inputs are provided as .xlsx files, such files have a limited number of rows and columns to be entered. Namely, the range of the number of columns is from 1 to 16384, while the range of the number of rows is from 1 to 1048576.

**Q: What is the clustering method for the input data in InfraFair?**  
A: InfraFair does not perform clustering of input data. Clustering is used to identify groups of similar attributes in large datasets. If a large dataset of snapshots is to be considered and it is deemed to be more practical to reduce the number of snapshots, clustering of these snapshots is to be performed entirely outside this tool. Then, data for the set of representative/clustered snapshots is fed into the model, assigning different weights to them according to the group size they represent or any other appropriate measure.

**Q: How does InfraFair cluster input data of different magnitudes?**  
A: Clustering and normalization are not part of the software functionalities. Note that, in tracing the flows in the grid to determine the usage of grid elements by generators and loads, only the power flows on these elements, power injections by generators and power withdrawals by loads are considered. These are all parameters expressing power amounts and all of them must be expressed in the same units (typically MW, or, instead, GW). Parameters for flows, losses, generation, demand and rated capacity should all be expressed in the same units, for instance, in MW. The model does not deal with possible inconsistencies in the units used to express different input parameters of the same type. The fact that some power amounts to be considered are significantly larger than others should not be taken into account in computing the allocation of the cost of each network element to its users. It is not acceptable to have a flow in MW in one asset and a flow in KW in another asset. Of course, different types of parameters could be expressed in different units, like those referring to power amounts and those referring to lengths or voltages, which could be expressed in km, kV, or others. But all the entries for each parameter should have the same unit.

**Q: What kind of solver does InfraFair require?**  
A: InfraFair is not an optimization solver and does not require any specific solver to run. The model is based on specific operations that are performed using the Numerical Python library, Numpy.

**Q: Does InfraFair require any specific operating system characteristics?**  
A: InfraFair does not require any specific operating system characteristics. It can run on any operating system that has Python 3.8 or above. Note that the model could run on a lower version of Python (although we do not recommend it and we have not tested it) but in this case, the user has to install it manually and not with pip install command. The same procedure for installing and running InfraFair can be used across the different operating systems (Windows, Linux, and Mac), using the specific operating system syntax.

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
