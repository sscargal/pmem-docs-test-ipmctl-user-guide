# NAME

ipmctl-show-acpi - Shows the system ACPI tables related to the DCPMMs

# SYNOPSIS

> 
> 
>     ipmctl show [OPTIONS] -system

# DESCRIPTION

Shows the system ACPI tables related to the DCPMMs in the system.

# OPTIONS

  - \-h; -help  
    Displays help for the command.

  - \-ddrt  
    Used to specify DDRT as the desired transport protocol for the
    current invocation of ipmctl.

  - \-smbus  
    Used to specify SMBUS as the desired transport protocol for the
    current invocation of ipmctl.

> **Note**
> 
> The -ddrt and -smbus options are mutually exclusive and may not be
> used together.

# TARGETS

  - \-system \[NFIT|PCAT|PMTT\]  
    The system ACPI table(s) to display. By default both the NFIT and
    PCAT tables are displayed. One of:
    
      - "NFIT" - The NVDIMM Firmware Interface Table
    
      - "PCAT" - The Platform Capabilities Table
    
      - "PMTT" - The Platform Memory Topology Table

Refer to the ACPI specification for detailed information about the ACPI
tables.

# EXAMPLES

Show the ACPI NFIT

> 
> 
>     ipmctl show -system NFIT

# RETURN DATA

Returns the formatted data from the requested ACPI tables and their
sub-tables. Refer to the ACPI specification for detailed information
about the format of the ACPI tables.

> **Note**
> 
> All data is presented in ACPI little endian format.