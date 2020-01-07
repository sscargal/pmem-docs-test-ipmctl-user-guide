# NAME

ipmctl-show-firmware - Shows detailed information about the firmware

# SYNOPSIS

> 
> 
>     ipmctl show [OPTIONS] -firmware [TARGETS]

# DESCRIPTION

Shows detailed information about the firmware on one or more DCPMMs.

# OPTIONS

  - \-a; -all  
    Shows all attributes.

> **Note**
> 
> The all and display options are exclusive and may not be used
> together.

  - \-d (attributes); -display (attributes)  
    Filters the returned attributes by explicitly specifying a
    comma-separated list of any of the attributes defined in the Return
    Data section.

> **Note**
> 
> The all and display options are exclusive and may not be used
> together.

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

  - \-dimm \[DimmIDs\]  
    Restricts output to the firmware information for specific DCPMMs by
    supplying one or more comma-separated DCPMM identifiers. The default
    is to display the firmware information for all manageable DCPMMs.

# EXAMPLES

Shows the firmware information for all DCPMMs in the server.

> 
> 
>     ipmctl show -dimm -firmware

# LIMITATIONS

The specified DCPMM(s) must be manageable by the host software.

# RETURN DATA

The default behavior is to display a table with the default attributes
listed below; the options can be used to expand or restrict the output.

  - DimmID  
    (Default) The DCPMM identifier

  - ActiveFWVersion  
    (Default) The BCD-formatted revision of the active firmware in the
    format PN.RN.SV.bbbb where:
    
      - PN = 2-digit product number
    
      - RN = 2-digit revision number
    
      - SV = 2-digit security version number
    
      - bbbb = 4-digit build version

  - StagedFWVersion  
    (Default) The BCD-formatted revision of the firmware staged for
    execution on the next power cycle in the format PN.RN.SV.bbbb where:
    
      - PN = 2-digit product number
    
      - RN = 2-digit revision number
    
      - SV = 2-digit security version number
    
      - bbbb = 4-digit build version

  - FWUpdateStatus  
    The status of the last firmware update operation. One of:
    
      - Unknown
    
      - Staged successfully
    
      - Update loaded successfully
    
      - Update failed to load, fell back to previous firmware

  - FWImageMaxSize  
    The maximum size of a firmware image
