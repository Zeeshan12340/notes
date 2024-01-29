# Theory
Supervisory Control and Data Acquisition (SCADA) systems are used to control and automate industrial processes. SCADA systems includes:

**Supervisory computers:** the servers used to manage the process gathering data on the process and communicating with filed devices (PLC/RTU). In smaller deployments HMI is embedded in a single computer, in larger deploy HMI is installed into a dedicated computer.

**Programmable Logic Controllers (PLC):** digital computers used mainly for automating industrial processes. They are used to continuously monitor sensors (input) and make decisions controlling devices (output).

Remote Terminal Units (RTU): nowadays RTUs and PLCs functionalities overlap with each other. RTUs are usually preferred for wider geographical telemetry whereas PLCs are better with local controls.

**Communication network:** the network connecting all SCADA components (Ethernet, Serial, telephones, radio, cellular...). Network failures do not necessarily impact negatively on the plant process.  Both RTU's and PLC's should be designed to operate autonomously, using the last instruction given from the supervisory system.

**Human Machine Interface (HMI):** displays a digitalized representation of the plant. Operators can interact with the plant issuing commands using mouse, keyboards or touch screens. **Operators can make supervisory decisions adjusting or overriding the normal plant behaviour.**

**Modbus RTU is usually used via RS-485 (serial network): one master is present with one or more slaves. Each slave has an unique 8-bit address.**