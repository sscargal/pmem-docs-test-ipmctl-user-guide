# NAME

ipmctl-delete-goal - Deletes the memory allocation goal from DCPMMs

# SYNOPSIS

> 
> 
>     ipmctl delete [OPTIONS] -goal [TARGETS]

# DESCRIPTION

Deletes the memory allocation goal from one or more DCPMMs. This command
only deletes a memory allocation goal request that has not been
processed by BIOS.

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

# TARGETS

  - \-dimm \[DimmIDs\]  
    Deletes the memory allocation goal from specific DCPMMs by
    optionally supplying one or more comma-separated DCPMM identifiers.
    The default is to delete the memory allocation goals from all
    manageable DCPMMs.

  - \-socket \[SocketIds\]  
    Deletes the memory allocation goal from the DCPMMs on specific
    sockets by supplying the socket target and one or more
    comma-separated socket identifiers. The default is to delete the
    memory allocation goals from manageable DCPMMs on all sockets.

# EXAMPLES

Deletes the memory allocation goal from all DCPMMs on all sockets.

> 
> 
>     ipmctl delete -goal

# LIMITATIONS

The appropriate privileges and the specified DCPMM(s) must be manageable
by the host software and unlocked if security is enabled. given socket
and all specified DCPMMs must contain a memory allocation goal.

# RETURN DATA

For each DCPMM, the CLI will indicate the status of the operation. If a
failure occurs when deleting the memory allocation goals from multiple
DCPMMs, the process will output a failure message for those DCPMMs that
did not succeed and a success message for those that did.

# SAMPLE OUTPUT

> 
> 
>     Delete memory allocation goal from DIMM (DimmID): Success

> 
> 
>     Delete memory allocation goal from DIMM (DimmID): Error:
>     (Description)
