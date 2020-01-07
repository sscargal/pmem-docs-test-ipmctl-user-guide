# NAME

ipmctl-load-goal - Load a memory allocation goal from a file onto DCPMMs

# SYNOPSIS

> 
> 
>     ipmctl load [OPTIONS] -source (path) -goal [TARGETS]

# DESCRIPTION

Load a memory allocation goal from a file onto one or more DCPMMs.

> **Warning**
> 
> **This command may result in data loss. Data should be backed up to
> other storage before executing this command**.

> **Note**
> 
> Changing a memory allocation goal modifies how the platform firmware
> maps persistent memory in the system address space (SPA) which may
> result in data loss or inaccessible data, but does not explicitly
> delete or modify user data found in persistent memory.

# OPTIONS

  - \-f; -force  
    Reconfiguring DCPMMs is a destructive operation which requires
    confirmation from the user. This option suppresses the confirmation.

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

  - \-u (B|MB|MiB|GB|GiB|TB| TiB); -units (B|MB|MiB|GB|GiB|TB| TiB)  
    Changes the units that capacities are displayed in for this command.
    One of: bytes (B), megabytes (MB), mebibytes (MiB), gigabytes (GB),
    gibibytes (GiB), terabytes (TB) or tebibytes (TiB).

# TARGETS

  - \-dimm \[DimmIDs\]  
    Loads the memory allocation goal onto specific DCPMMs by supplying
    one or more comma separated DCPMM identifiers. The default is to
    load the memory allocation goal onto all manageable DCPMMs.

  - \-socket \[SocketIds\]  
    Loads the memory allocation goal onto all manageable DCPMMs on
    specific sockets by supplying the socket target and one or more
    comma-separated socket identifiers. The default is to load the
    memory allocation goal onto all manageable DCPMMs on all sockets.

# EXAMPLES

Loads the configuration settings stored in "config.txt" onto all the
DCPMMs in the system as a memory allocation goal to be applied by the
BIOS on the next reboot.

> 
> 
>     ipmctl load -source config.txt -goal

Loads the configuration settings stored in "config.txt" onto a specified
set of DCPMMs as a memory allocation goal to be applied by the BIOS on
the next reboot.

> 
> 
>     ipmctl load -source config.txt -goal -dimm 1,2,3

Loads the configuration settings stored in "config.txt" onto all
manageable DCPMMs on sockets 1 and 2 as a memory allocation goal to be
applied by the BIOS on the next reboot.

> 
> 
>     ipmctl load -source config.txt -goal -socket 1,2

# LIMITATIONS

In order to successfully execute this command:

  - The caller must have the appropriate privileges.

  - The specified DCPMM(s) must be manageable by the host software and
    must all have the same SKU.

  - Existing memory allocation goals that have not been applied and any
    namespaces associated with the requested DCPMM(s) must be deleted
    before running this command.

  - Security state must be disabled. Changing the memory configuration
    is a destructive operation which results in loss of data stored in
    the persistent memory region. Therefore, data should be backed up to
    other storage before executing this command. Targets may be limited
    to individual DCPMMs or sockets, but all DCPMMs on affected sockets
    must be configured when the command finishes. If the selected
    targets make this impossible, the command will be rejected. Refer to
    ***Show System Capabilities*** for a list of BIOS supported modes.

  - Some requests are dependent on BIOS and/or platform configuration.
    For details, refer to the *Intel® Optane™ DC Persistent Memory
    Software Memory Allocation Rules*, document number 564194. For
    example:

  - Provisioning DCPMMs for Memory Mode while BIOS is configured for 1LM
    only will result in unused capacity.

  - Provisioning DCPMMs for Memory Mode while not all iMCs have at least
    one DCPMM will result in unused capacity.

# RETURN DATA

If successful, the CLI will display the memory allocation goal stored on
each DCPMM as documented in the command Section
[???](#Show%20Memory%20Allocation%20Goal). If a failure occurs, an error
code and message will be displayed. If a failure occurs when configuring
multiple DCPMMs, the process will exit and remove the memory allocation
goal from any DCPMMs that succeeded prior to the failure.
