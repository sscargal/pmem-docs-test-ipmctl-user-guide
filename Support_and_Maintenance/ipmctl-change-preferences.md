# NAME

ipmctl-change-preferences - Modifies one or more user preferences

# SYNOPSIS

> 
> 
>     ipmctl set [OPTIONS] -preferences [PROPERTIES]

# DESCRIPTION

Modifies one or more user preferences in the DCPMM software.

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

# PROPERTIES

  - CLI\_DEFAULT\_DIMM\_ID  
    The default display of DCPMM identifiers. One of:
    
      - "UID": Use the DimmUID attribute as defined in the section
        ***Show Device***.
    
      - "HANDLE": Use the DimmHandle attribute as defined in section
        ***Show Device***. This is the default

  - CLI\_DEFAULT\_SIZE  
    The default display of capacities in the CLI. One of:
    
      - "AUTO": Automatically choose the best format for each capacity
        in binary multiples of bytes (i.e., B, MiB, GiB or TiB). This is
        the default.
    
      - "AUTO\_10": Automatically choose the best format for each
        capacity in decimal multiples of bytes (i.e., B, MB, GB or TB).
    
      - "B": Displays all capacities in bytes.
    
      - "MB": Displays all capacities in megabytes.
    
      - "MiB": Displays all capacities in mebibytes.
    
      - "GB": Displays all capacities in gigabytes.
    
      - "GiB": Displays all capacities in gibibytes.
    
      - "TB": Displays all capacities in terabytes.
    
      - "TiB": Displays all capacities in tebibytes.

  - APPDIRECT\_SETTINGS  
    The interleave settings to use when creating App Direct capacity in
    the format: (IMCSize\_ChannelSize). Must be one of the BIOS
    supported App Direct settings returned by the command ***Show System
    Capabilities***.

> **Note**
> 
> ByOne is not a valid setting for this preference. The default is
> "RECOMMENDED" which uses the BIOS recommended App Direct settings.

> **Note**
> 
> The same interleave settings are used for all the App Direct capacity
> in the system. Therefore, if any App Direct capacity already exists,
> this preference cannot be changed.

  - APPDIRECT\_GRANULARITY  
    The minimum App Direct granularity per DCPMM supported by the
    command ***Create Memory Allocation Goal***. One of:
    
      - "1": Allows 1 GiB App Direct granularity.
    
      - "32": Allows 32 GiB App Direct granularity.

# EXAMPLES

Use DimmUID as the default DCPMM identifier, and display all capacities
in bytes.

> 
> 
>     ipmctl set -preferences CLI_DEFAULT_DIMM_ID=UID CLI_DEFAULT_SIZE=B

# RETURN DATA

Returns the status of the operation.

# SAMPLE OUTPUT

> 
> 
>     Set (Property)=(Value): Success|Error (Code)-(Description)
