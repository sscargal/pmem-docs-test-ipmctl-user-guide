# NAME

ipmctl-show-socket - Shows basic information about the physical
processors

# SYNOPSIS

> 
> 
>     ipmctl show [OPTIONS] -socket [TARGETS]

# DESCRIPTION

Shows basic information about the physical processors in the host
server.

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

  - \-socket \[SocketIDs\]  
    Restricts output to the DIMMs installed on specific sockets by
    supplying the socket target and one or more comma-separated socket
    identifiers. The default is to display all sockets.

# EXAMPLES

Displays information about all the processors.

> 
> 
>     ipmctl show -socket

Lists all properties for socket 1.

> 
> 
>     ipmctl show -socket 1

Retrieves specific properties for each processor.

> 
> 
>     ipmctl show -d MappedMemoryLimit -socket

# RETURN DATA

Displays a table with the attributes listed below for each physical
processor installed in the host server.

  - SocketID  
    (Default) The processor socket identifier.

  - MappedMemoryLimit  
    (Default) The maximum amount of memory that is allowed to be mapped
    into the system physical address space for this processor based on
    its SKU.

  - TotalMappedMemory  
    (Default) The total amount of memory that is currently mapped into
    the system physical address space for this processor.
