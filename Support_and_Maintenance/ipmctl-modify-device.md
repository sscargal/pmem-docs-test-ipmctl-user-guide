# NAME

ipmctl-modify-device - Changes the configurable setting(s) on one or
more DCPMMs

# SYNOPSIS

> 
> 
>     ipmctl set [OPTIONS] -dimm (DimmIDs) FirstFastRefresh=(0|1)

# DESCRIPTION

Changes the configurable setting(s) on one or more DCPMMs.

# OPTIONS

  - \-f; -force  
    Changing DCPMM setting(s) is a potentially destructive operation
    which requires confirmation from the user for each DCPMM. This
    option suppresses the confirmation.

  - \-h; -help  
    Displays help for the command.

# TARGETS

  - \-dimm (DimmIDs)  
    Modifies specific DCPMMs by supplying one or more comma-separated
    DCPMM identifiers. However, this is not recommended as it may put
    the system in an undesirable state. The default is to modify all
    manageable DCPMMs.

# PROPERTIES

  - FirstFastRefresh  
    Whether acceleration of the first refresh cycle is enabled. One of:
    
      - "0": Disable - This is the default.
    
      - "1": Enable - Customers will have to wait a pre-determined time
        (5-6 minutes) before starting benchmark tests.

# EXAMPLES

Enables acceleration of the first fast refresh cycle on all manageable
DCPMMs

> 
> 
>     set -dimm FirstFastRefresh=1

# LIMITATIONS

The specified DCPMM(s) must be manageable by the host software.

# RETURN DATA

For each DCPMM, the CLI will indicate the status of the operation. If a
failure occurs when modifying multiple DCPMMs, the process will exit and
not continue modifying the remaining DCPMMs.

# SAMPLE OUTPUT

> 
> 
>     Modify DIMM (DimmID): Success
>     Modify DIMM (DimmID): Error (Code)-(Description)
