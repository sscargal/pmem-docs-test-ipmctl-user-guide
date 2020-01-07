# NAME

ipmctl-show-goal - Shows the memory allocation goal on one or more DCPMM

# SYNOPSIS

> 
> 
>     ipmctl show [OPTIONS] -goal [TARGETS] [PROPERTIES]

# DESCRIPTION

Shows the memory allocation goal on one or more DCPMMs. Once the goal is
successfully applied by the BIOS, it is no longer displayed. Use the
command Section [???](#Show%20Memory%20Resources) to view the
system-wide memory resources or the command ***Show Persistent Memory***
for detailed persistent memory information.

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

  - \-u (B|MB|MiB|GB|GiB|TB| TiB); -units (B|MB|MiB|GB|GiB|TB| TiB)  
    Changes the units that capacities are displayed in for this command.
    One of: bytes (B), megabytes (MB), mebibytes (MiB), gigabytes (GB),
    gibibytes (GiB), terabytes (TB) or tebibytes (TiB).

# TARGETS

  - \-dimm \[DimmIDs\]  
    Restricts output to specific DCPMMs by supplying one or more comma
    separated DCPMM identifiers. The default is to display all
    manageable DCPMMs with memory allocation goals.

  - \-socket \[SocketIds\]  
    Restricts output to the DCPMMs on specific sockets by supplying the
    socket target and one or more comma-separated socket identifiers.
    The default is to display all manageable DCPMMs on all sockets with
    memory allocation goals.

# EXAMPLES

Shows the default memory allocation goal attributes for each DCPMM.

> 
> 
>     ipmctl show -goal

Shows all the memory allocation goal attributes for the DCPMMs on socket
1.

> 
> 
>     ipmctl show -a -goal -socket 1

# LIMITATIONS

The specified DCPMMs must be manageable by the host software.

# RETURN DATA

The default behavior is to display a table with the default attributes
for each DCPMM; applying options changes the output to a more detailed
format.

  - SocketID  
    (Default) The processor socket identifier where the DCPMM is
    installed.

  - DimmID  
    (Default) The DCPMM identifier

  - MemorySize  
    (Default) The DCPMM capacity that will be configured in Memory Mode.

  - AppDirect1Size  
    (Default) The DCPMM capacity that will be configured as the first
    App Direct interleave set if applicable.

  - AppDirect1Index  
    Unique identifier of the first App Direct interleave set.
    
      - N/A: If no App Direct interleave set
    
      - Numeric value if App Direct interleave set is present.

  - AppDirect1Settings  
    The settings for the first App Direct interleave set in the format:
    x(Way) \[- (Size) iMC\] \[x (Size) Channel\]

  - AppDirect2Size  
    (Default) The DCPMM capacity that will be configured as the second
    App Direct interleave set if applicable.

  - AppDirect2Index  
    Unique identifier of the second App Direct interleave set.
    
      - N/A: If no App Direct interleave set
    
      - Numeric value if App Direct interleave set is present.

  - AppDirect2Settings  
    The settings for the second App Direct interleave set in the format:
    x(Way) \[- (Size) iMC\] \[x (Size) Channel\]

  - Status  
    The status of the memory allocation goal. One of:
    
      - Unknown: The status cannot be determined.
    
      - New: A reboot is required for the memory allocation goal to be
        processed by the BIOS.
    
      - Failed - Bad request: The BIOS failed to process the memory
        allocation goal because it was invalid.
    
      - Failed - Not enough resources: There were not enough resources
        for the BIOS to process the memory allocation goal.
    
      - Failed - Firmware error: The BIOS failed to process the memory
        allocation goal due to a firmware error.
    
      - Failed - Unknown: The BIOS failed to process the memory
        allocation goal due to an unknown error.

# SAMPLE OUTPUT

If a new memory allocation goal has been created, a prompt to reboot
will be presented.

> 
> 
>     A reboot is required to process new memory allocation goals.
