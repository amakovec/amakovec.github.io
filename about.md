---
layout: page
title: About Me
permalink: /about/
---

<link rel="stylesheet" href="/about.css">

<div class="image-cropper">
    <img align="right" class="profile-pic" alt="Andy Makovec's profile picture" src="/assets/images/author.jpg">
</div>

Hi!  I'm a hardware engineer with extensive experience in designing development boards, writing scripts for test automation, and creating test cases for board bring-up, design verification, and EMC.

## Experience

### Senior Electrical Test Engineer at Tesla (January 2022 - Present)

* Internal test equipment hardware platform
  * Revised an internal backplane power and communications board. Major redesign to replace end-of-life components, complete tear-up+reroute to fix signal integrity issues, fixed Ethernet termination scheme
  * Designed a board to interface a major new vehicle body controller/ECU with internal test equipment. Designed a schematic with circuits to test all drivers and communication lines on the ECU. Performed layout (50+ connectors w/ 500+ pins).
  * Debugged existing test instrument PCBA designs. Identified issues on multiple test instrument boards resulting in false readings and/or instrument failures. Found issues including synchronous FET shoot-through, missing inductive flyback protection, and missing hysteresis.
* Internal test equipment firmware
  * Resolved several networking firmware issues that were leading to random, infrequent, and difficult to reproduce disconnects (lwIP memory configuration)
  * Ported a bootloader w/ network update capability to an STM32 microcontroller, and ported its build system from a bespoke Python build script to CMake.
  * Implemented a pulse width measurement feature on an existing test instrument PCBA via STM32’s input capture feature and IRQ handlers / callbacks
* Internal test software platform
  * Ported 70% of lab’s test computers from Windows -> Linux to simplify deployment and management. Set up Ansible server + playbook w/ nightly automation to ensure computers are up to date and retain identical configuration.
  * Consolidated body controller reliability testing software, reducing copy-pasted function usage. Led teammates in the consolidation, helping with git branching/merging.
  * Debugged an internal Rust library for interfacing with vehicle controllers over Ethernet, resolving packet loss.
  * Added support for several minor revisions of vehicle body controllers/ECUs
* Steering systems
  * Led in-house reliability testing for 3 steering control PCBAs
  * Wrote Python software to apply a motor speed and torque profile while monitoring for faults, including monitoring and interlock hardware/software for test setup safety.
  * Root-caused a steering PCBA design validation failure. Identified a way to reliably reproduce the issue via an HTHE reliability test. Identified the failure mode via DUT instrumentation with oscilloscope and Python script to monitor scope trigger and power supply currents. Worked with design team to implement a rework/retrofit.
  * Performed thermal characterization testing of FETs, diodes, and micros used in the assembly
* Braking systems
  * Led low voltage power consumption testing for 4 braking control PCBAs
  * Wrote embedded C firmware (extension of existing internal RTOS) to actuate brake cylinders. Wrote an arbitrary waveform generator in C, to reduce flash memory requirement and avoid latency over CAN.
  * Wrote Python scripts to send start/stop commands to firmware, control and capture power and temperature data from NI DAQs, control and capture data from oscilloscopes, and monitor for overtemperature events.
  * Designed and implemented a web dashboard (streamlit, plotly) to intuitively display collected results to a variety of stakeholders (hardware designers, project management, leadership, etc.)
* Mentored 10+ interns and junior engineers by directing design and review for ECU validation and reliability testing projects, and PCB design projects
* Onboarded office in Shanghai, China on using internal hardware and software for ECU validation and reliability testing.
* Collaborated with technician team to set up test hardware, debug tests, perform data collection, and update tickets

### Hardware Engineer at Rockwell Automation (May 2019 - December 2021)

* Designed several development boards to enable test automation in early prototype and final test stages for a series of new I/O products:
  * Designed for requirements such as multiple isolation zones, 12+ high-speed signals, and several power integrity requirements, resulting in designs of 200+ components per board.
  * Oversaw layout performed by a separate layout designer.  Facilitated resolution of placement conflicts.
  * Designed a quick-turn PCB to test a high-risk subcircuit. Created and executed test cases to verify the subcircuit.
  * Led DMI review and PCB DFM processes, and assisted in material ordering and organizing production runs.
  * Created test cases for board bring-up and design verification test, and oversaw execution of tests.
* Designed and implemented Python scripts for test automation and results analysis:
  * Designed a Python script to capture test results from multiple pieces of test equipment and generate a test report containing 3000+ data points.  Included a GUI for use by technicians.
  * Designed a Python script to visualize backplane communication failures with a heatmap.
* EMC test plan generation (IEC 61000), specifically with regards to ensuring hardware was exercised to functional requirements while under exposure to noise:
  * Designed and implemented Ladder Logic (Allen-Bradley) for test automation.
  * Coordinated flashing of firmware and installation of software to 8 early prototype test setups in order to enable preliminary EMC testing.
* Member of a cross-functional SAFe Agile team (hardware, firmware, and software), collaborating with other teams (~150 person project) to develop a series of 10+ products.
* Served as Scrum Master (50/50 time split with technical work above, Sept 2019 - Sept 2020):
  * Led sprint planning and daily stand-ups, assisted in backlog grooming, and prepared stories and metrics in Jira.
  * Delivered bi-weekly readout presentations to an audience of ~150 people, covering a mix of technical progress and agile metrics.

### Hardware Engineering Co-Op at Rockwell Automation (Jan 2018 - Aug 2018)

* Performed EMC Testing of Ethernet-enabled embedded systems products to qualify conformance to the IEC 61000-6-4 standard, including configuring PLCs to automate the testing process.
* Oversaw the hardware-related aspects of a quality control revision of a legacy embedded systems product including DMI review, PCB DFM process, prototype/pilot runs, and last-time buy considerations.
* Investigated viability of potential cost savings in new Ethernet PHYs by testing for conformance to IEEE 802.3.
* Designed and analyzed possible PCB layouts to solve space constraint issues in a new product under development.
* Mentored a team of 3 engineering interns on a long-term embedded systems design project.

## Skills

* **Hardware Design**: High speed (Ethernet 1000BASE-T, 100BASE-TX, and 1000BASE-T1), brushed and brushless/3-phase DC motor drivers, high-side FET drivers / eFuses, op-amp / in-amp based amplifiers, microcontrollers (pinout assignment, layout, and firmware), grounding analysis, power supply design (buck, boost, buck-boost, single and multiphase)
* **Embedded Firmware (C)**: Communication (Ethernet, USB, SPI, I2C, UART, CAN), interrupts (timers, inputs, input capture), RTOS (Mbed OS), STM32 HAL and LL, Makefile, CMake
* **Design Capture**: Altium Designer proficiency (schematic, layout, rules, constraint manager, DRC, part management, Draftsman, and Altium 365), Mentor Graphics proficiency (Xpedition design capture flow, HyperLynx SI/PI modeling, library management), KiCAD competency (design capture and library management), HFSS (EMag FEM) and FEKO (antenna design) familiarity.
* **Programming Languages**: Python proficiency, Embedded C competency, Rust familiarity.
* **Version Control**: Git, GitHub, GitLab, and SVN competency.
* **Reliability Testing**: LTOE, HTOE, HTHE, PTCE + related failure modes
* **Standards (familiarity, not certification)**: IEC 61000-6-4, ISO 26262, IEEE 802.3
* **Other Skills**: LTSpice, Linux, CATIA V5/V6, 3DExperience, MATLAB/Octave, SAP ECC, Rockwell Software (Studio 5000, RSLinx, FactoryTalk), CMake, Ansible, Mbed OS, Bash, Jira, GitHub Actions

## Education

Bachelor of Science in Electrical and Computer Engineering, Electrical Engineering Program of Study (The Ohio State University, Class of 2019)

## Interests

* Hardware Test Automation and Python evangelist
* High speed digital design
* Wireless design
    * Microwave and antenna design coursework
    * Amateur Radio Extra License (Callsign KE8KNA)

## Contact Me

* GitHub: [amakovec](https://github.com/amakovec)
* LinkedIn: [amakovec](https://www.linkedin.com/in/amakovec/)
* Twitter: [@andymakovec](https://twitter.com/andymakovec)
* Email: [andymakovec@gmail.com](mailto:andymakovec@gmail.com)
