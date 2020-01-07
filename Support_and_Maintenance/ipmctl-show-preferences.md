# NAME

ipmctl-show-preferences - Displays a list of the DCPMM software user
preferences

# SYNOPSIS

> 
> 
>     ipmctl show [OPTIONS] -preferences

# DESCRIPTION

Displays a list of the DCPMM software user preferences and their current
values.

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

# EXAMPLES

Displays the current values for all the user preferences

> 
> 
>     ipmctl show -preferences

# RETURN DATA

  - CLI\_DEFAULT\_DIMM\_ID  
    The default display of DCPMM identifiers. One of:
    
      - UID: Use the DimmUID attribute as defined in the command Show
        Device.
    
      - HANDLE: Use the DimmHandle attribute as defined in the command
        Show Device. This is the default.

  - CLI\_DEFAULT\_SIZE  
    The default display of capacities in the CLI. One of:
    
      - AUTO: Automatically choose the best format for each capacity in
        binary multiples of bytes (i.e., B, MiB, GiB or TiB). This is
        the default.
    
      - AUTO\_10: AUTO\_10: Automatically choose the best format for
        each capacity in decimal multiples of bytes (i.e., B, MB, GB or
        TB).
    
      - B: Displays all capacities in bytes.
    
      - MB: Displays all capacities in megabytes.
    
      - MiB: Displays all capacities in mebibytes.
    
      - GB: Displays all capacities in gigabytes.
    
      - GiB: Displays all capacities in gibibytes.
    
      - TB: Displays all capacities in terabytes.
    
      - TiB: Displays all capacities in tebibytes.

  - APPDIRECT\_SETTINGS  
    The interleave settings to use when creating App Direct capacity in
    the format: (IMCSize\_ChannelSize). The default is "RECOMMENDED"
    which uses the BIOS recommended App Direct settings returned by the
    command Show System Capabilities.

  - APPDIRECT\_GRANULARITY  
    The minimum App Direct granularity per DCPMM supported by the
    command Create Memory Allocation Goal. One of:
    
      - 1: Allows 1 GiB App Direct granularity.
    
      - 32: Allows 32 GiB App Direct granularity.

  - DBG\_LOG\_LEVEL  
    Whether debug logging is enabled in the DCPMM host software. These
    logs pertain to the operation of the command-line tool only and do
    not reflect any logging functionality of the DCPMM. One of:
    
      - 0: Logging is disabled. This is the default.
    
      - 1: Log Errors.
    
      - 2: Log Warnings, Errors.
    
      - 3: Log Informational, Warnings, Errors.
    
      - 4: Log Verbose, Informational, Warnings, Errors.
