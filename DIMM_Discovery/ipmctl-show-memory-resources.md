# NAME

ipmctl-show-memory-resources - Shows the total DCPMM memory resource
allocation

# SYNOPSIS

> 
> 
>     ipmctl show [OPTIONS] -memoryresources

# DESCRIPTION

Shows the total DCPMM memory resource allocation across the host server.

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

  - \-u (B|MB|MiB|GB|GiB|TB| TiB); -units (B|MB|MiB|GB|GiB|TB| TiB)  
    Changes the units that capacities are displayed in for this command.
    One of: bytes (B), megabytes (MB), mebibytes (MiB), gigabytes (GB),
    gibibytes (GiB), terabytes (TB) or tebibytes (TiB).

# EXAMPLES

Shows the DCPMM memory resource allocation.

> 
> 
>     ipmctl show -memoryresources

# RETURN DATA

Returns the default attributes listed below.

> **Note**
> 
> Capacities from unmanageable DCPMMs are not included in the following
> aggregated totals.

  - Capacity  
    Total system DCPMM capacity.

  - MemoryCapacity  
    Total usable system DCPMM Memory Mode capacity.

  - AppDirectCapacity  
    Total usable system DCPMM App Direct capacity.

  - UnconfiguredCapacity  
    Total system DCPMM capacity that is unusable because it has not been
    configured.

  - ReservedCapacity  
    Total system DCPMM persistent memory capacity that is reserved. This
    capacity is the persistent memory partition capacity (rounded down
    for alignment) less any App Direct capacity. Reserved capacity
    typically results from a Memory Allocation Goal request that
    specified the Reserved property. This capacity is not mapped to
    system physical address (SPA) space.

  - InaccessibleCapacity  
    Total system DCPMM capacity that is inaccessible due any of:
    
      - Platform configuration prevents accessing this capacity. e.g.
        MemoryCapacity is configured but MemoryMode is not enabled by
        platform FW (current Memory Mode is 1LM).
    
      - Capacity is inaccessible because it is not mapped into the
        system physical address space (SPA). This is usually due to
        platform firmware memory alignment requirements.
    
      - DCPMM configured capacity but SKU prevents usage. e.g.
        AppDirectCapcity but DCPMM SKU is MemoryMode only.

# DETAILS

DCPMMs are partitioned into Memory and Persistent partitions. ipmctl
will align the Memory partition on a 1 GiB boundary with the Persistent
partition consuming the remaining capacity. An exception: if DCPMM is
configured for 100% Memory Mode then Memory partition will consume 100%
of the capacity, while Persistent partition will be 0 length. Any
capacity that falls outside the Memory and Persistent partitions is
InaccessibleCapacity and is not useable.

Platform firmware alignment restrictions may result in some capacity
from the Memory and Persistent partitions not mapped to system physical
address (SPA) space. This memory is considered InaccessibleCapacity and
is not usable.

Definitions:

  - Total Capacity (TC)  
    Raw Capacity (total usable) reported by DCPMM DIMM Partition Info

  - Memory Partition Capacity (MPC)  
    Volatile Capacity reported by DCPMM DIMM Partition Info

  - Persistent Partition Capacity (PPC)  
    Persistent Capacity reported by DCPMM DIMM Partition Info

  - Volatile Memory Size (VMS)  
    Usable voliatile memory capacity as reported by platform FW via
    *Intel NVDIMM Current Config→Volatile Memory Size Mapped into SPA*
    field

  - Persistent Memory Size (PMS)  
    Usable persistent memory capacity as reported by platform FW via
    *Intel NVDIMM Current Config→Persistent Memory Size Mapped into SPA*
    field

  - DCPMM DIMM Partition Info  
    DIMM Partition Info provided by DCPMM firmware. See *Intel® Optane™
    DC Persistent Memory Module Firmware Interface Specification* for
    details.

  - Intel NVDIMM Current Config  
    See *Intel® NVM Dimm Management Software-Firmware Interface
    Specification* for details.

**Calculations:**

> 
> 
>     MemoryCapacity = Volatile Memory Size

> 
> 
>     AppDirectCapacity = Persistent Memory Size

> 
> 
>     ReservedCapacity = PPC (rounded down for PM alignment) - PMS

> 
> 
>     InaccessibleCapacity =
>       + TC - VMS - PMS - ReservedCapacity
>      if (CurrentMode == 1LM) then
>       + VMS (rounded down for alignment)
