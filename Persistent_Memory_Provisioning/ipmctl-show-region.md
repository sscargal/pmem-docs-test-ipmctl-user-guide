# NAME

ipmctl-show-region - Retrieves a list of persistent memory regions

# SYNOPSIS

> 
> 
>     ipmctl show [OPTIONS] -region [TARGETS]

# DESCRIPTION

Retrieves a list of persistent memory regions of DCPMM capacity

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

  - \-lpmb  
    Used to specify large transport payload size for the current
    invocation of ipmctl.

  - \-spmb  
    Used to specify small transport payload size for the current
    invocation of ipmctl.

> **Note**
> 
> The -lpmb and -spmb options are mutually exclusive and may not be used
> together.

  - \-nfit  
    Used to specify NFIT table as the source instead of PCD(default) for
    the current invocation of ipmctl.

  - \-u (B|MB|MiB|GB|GiB|TB| TiB); -units (B|MB|MiB|GB|GiB|TB| TiB)  
    Changes the units that capacities are displayed in for this command.
    One of: bytes (B), megabytes (MB), mebibytes (MiB), gigabytes (GB),
    gibibytes (GiB), terabytes (TB) or tebibytes (TiB).

# TARGETS

  - \-region \[RegionIDs\]  
    Restricts output to specific persistent memory regions by providing
    one or more comma separated region identifiers. The default is to
    display the persistent memory regions across all manageable DCPMMs.

  - \-socket \[SocketIDs\]  
    Restricts output to the persistent memory regions on specific
    sockets by supplying the socket target and one or more
    comma-separated socket identifiers. The default is to display all
    sockets.

# EXAMPLES

Shows all attributes of all persistent memory regions in the server.

> 
> 
>     ipmctl show -a -region

Shows all attributes for the specified persistent memory region.

> 
> 
>     ipmctl show -a -region 1

# LIMITATIONS

All the underlying DCPMMs should be unlocked to accurately reflect the
available capacities. The specified DCPMM(s) must be manageable by the
host software.

# RETURN DATA

The default behavior is to display a table with the default attributes
listed below; applying options changes the output to a more detailed
format.

  - RegionID  
    (Default) The unique region identifier

  - PersistentMemoryType  
    (Default) A comma-separated list of the underlying type(s) of
    persistent memory capacity in the region. One or more of:
    
      - AppDirect: App Direct capacity interleaved across two or more
        DCPMMs that is fully mapped into the system physical address
        space.
    
      - AppDirectNotInterleaved: App Direct capacity wholly contained on
        a single DCPMMs that is fully mapped into the system physical
        address space.

  - Capacity  
    (Default) Total usable capacity, both allocated and unallocated

  - FreeCapacity  
    (Default) Remaining usable capacity

  - SocketID  
    (Default) Socket ID to which the region belongs

  - HealthState  
    The rolled up health of the underlying DCPMMs. One of:
    
      - Unknown: The region health cannot be determined.
    
      - Healthy: All underlying DCPMM persistent memory capacity is
        available.
    
      - Pending: A new memory allocation goal has been created but not
        applied. Reboot or delete any existing memory allocation goals
        before creating namespaces on the region.
    
      - Error: There is an issue with some or all of the underlying
        DCPMM capacity because the interleave set has failed.
    
      - Locked: One or more of the of the underlying DCPMMs are locked.

  - ISetID  
    The region unique identifier. Also known as interleave set cookie.

  - DimmID  
    A list of all the DIMMs that are part of this reg.
