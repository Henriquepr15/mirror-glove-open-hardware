# Gerber fabrication files

This folder contains the Gerber and drill files exported from the Mirror Glove ESP32-C6 Super Mini PCB design.

These files correspond to the prototype version used for experimental validation and open hardware documentation.

## Important note

The current PCB design is provided as an experimental/as-built prototype version. The KiCad Design Rule Checker reported violations mainly related to custom footprints, courtyard definitions, library matching, and layout details.

The board files are shared to support transparency, review, modification, and replication of the prototype. Before manufacturing a new batch, users should open the project in KiCad, run ERC/DRC checks, review the reported violations, and adjust the design according to the fabrication requirements of the selected PCB manufacturer.

This project is not a certified medical device and the PCB files should not be used for clinical or safety-critical applications without additional validation.
