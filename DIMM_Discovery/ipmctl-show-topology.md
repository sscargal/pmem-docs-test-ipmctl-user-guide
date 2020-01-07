# NAME

ipmctl-show-topology - Shows the topology of the memory installed

# SYNOPSIS

> 
> 
>     ipmctl show [OPTIONS] -topology [TARGETS]

# DESCRIPTION

Shows the topology of the memory installed in the host server. Use the
command ipmctl-show-device to view more detailed information about a
DCPMM.

# OPTIONS

  - \-a; -all  
    Shows all attributes.

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
    Restricts output to specific DIMMs by optionally supplying the DIMM
    target and one or more comma-separated DIMM identifiers. The default
    is to display all DIMMs.

  - \-socket \[SocketIDs\]  
    Restricts output to the DIMMs installed on specific sockets by
    supplying the socket target and one or more comma-separated socket
    identifiers. The default is to display all sockets.

> **Note**
> 
> If ACPI PMTT table is not present, then DDR4 memory will not be
> displayed in the filtered socket list.

# EXAMPLES

Displays the system memory topology.

> 
> 
>     ipmctl show -topology

# RETURN DATA

Displays a table with the attributes listed below for each memory DIMM
installed in the host server.

  - MemoryType  
    (Default) The DIMM type. One of:
    
      - Unknown
    
      - DDR4
    
      - Logical Non-volatile Device

  - Capacity  
    (Default) The raw capacity of the DIMM as reported in the SMBIOS
    Type 17 table.

  - DimmID  
    (Default) The DIMM identifier. For DRAM DIMMs, the DimmID is "N/A".

  - PhysicalID  
    (Default) The DIMM physical identifier (i.e., SMBIOS Type 17
    handle).

  - DeviceLocator  
    (Default) The string that identifies the physically-labeled socket
    or board position where the DIMM is located.

  - SocketID  
    The processor socket identifier (i.e., NUMA node) where the DIMM is
    installed. For DRAM DIMMs, the socket identifier is "N/A".

  - MemControllerID  
    The associated memory controller identifier. For DRAM DIMMs, the
    memory controller identifier is "N/A".

  - ChannelID  
    The associated channel. For DRAM DIMMs, the channel identifier is
    "N/A".

  - ChannelPos  
    The DIMM position in the channel. For DRAM DIMMs, the channel
    position identifier is "N/A".

  - NodeControllerID  
    The node controller identifier. For DRAM DIMMs, the node controller
    identifier is "N/A".

  - BankLabel  
    The string that identifies the physically-labeled bank where the
    DIMM is located.