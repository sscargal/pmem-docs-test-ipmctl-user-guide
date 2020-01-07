# NAME

ipmctl-create-goal - Creates a memory allocation goal on one or more
DCPMM

# SYNOPSIS

> 
> 
>     ipmctl create [OPTIONS] -goal [TARGETS] [PROPERTIES]

# DESCRIPTION

Creates a memory allocation goal on one or more for the BIOS to read on
the next reboot in order to map the DCPMM capacity into the system
address space. Persistent memory can then be utilized by creating a
namespace.

> **Note**
> 
> The capacity values presented by this command are a target goal or
> request to platform firmware. The actual capacity values are subject
> to change due to rounding and alignment requirements. If the goal
> request is invalid or not possible it may be rejected by platform
> firmware.

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
    This option can also be used to recover/override corrupted Platform
    Configuration Data (PCD).

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
    Creates a memory allocation goal on specific DCPMMs by optionally
    supplying one or more comma-separated DCPMM identifiers. This list
    must include all unconfigured DCPMMs on the affected socket(s). The
    default is to configure all manageable DCPMMs on all sockets.

  - \-socket \[SocketIds\]  
    Creates a memory allocation goal on specific DCPMMs by supplying one
    or more comma-separated DCPMM identifiers. This list must include
    all unconfigured DCPMMs on the affected socket(s). The default is to
    configure all manageable DCPMMs on all sockets.

# PROPERTIES

  - MemoryMode  
    Percentage of the total capacity to use in Memory Mode (0-100).
    Default = 0.

  - PersistentMemoryType  
    If MemoryMode is not 100%, the type of persistent memory to create.
    
      - "AppDirect": (Default) Create App Direct capacity utilizing
        hardware interleaving across the requested DCPMMs if applicable
        given the specified target.
    
      - "AppDirectNotInterleaved": Create App Direct capacity that is
        not interleaved any other DCPMMs.

  - NamespaceLabelVersion  
    The version of the namespace label storage area (LSA) index block
    
      - "1.2": (Default) Defined in UEFI 2.7a - sections 13.19
    
      - "1.1": Legacy 1.1 namespace label support

  - Reserved  
    Reserve a percentage (0-100) of the requested DCPMM App Direct
    capacity that will not be mapped into the system physical address
    space and will be presented as Reserved Capacity with Show Device
    and Show Memory Resources Commands.

# EXAMPLES

Configures all the DCPMM capacity in Memory Mode.

> 
> 
>     ipmctl create -goal MemoryMode=100

Configures all the DCPMM capacity as App Direct.

> 
> 
>     ipmctl create -goal PersistentMemoryType=AppDirect

Configures the capacity on each DCPMM with 20% of the capacity in Memory
Mode and the remaining as App Direct capacity that does not use hardware
interleaving.

> 
> 
>     ipmctl create -goal MemoryMode=20 PersistentMemoryType=AppDirectNotInterleaved

Configures the DCPMM capacity across the entire system with 25% of the
capacity in Memory Mode, 25% reserved and the remaining 50% as App
Direct. Configures the DCPMM capacity across the entire system with 25%
of the capacity in Memory Mode and the remaining 75% as App
>     Direct.

> 
> 
>     ipmctl create -goal MemoryMode=25 PersistentMemoryType=AppDirect Reserved=25

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

Minor adjustments (up to 10%) in the requested capacities are sometimes
necessary to align properly according to the platform rules. There are
also some situations that require additional confirmation from the user
because they may result in a non- optimal configuration (i.e., reduced
performance). These are described below.:

**The requested goal may result in a non-optimal configuration due to
the population of DIMMs in the system**  

Memory Mode capacity requested but the population of DRAM DIMMs and
DCPMMs in the system may result in reduced performance (i.e., the ratio
of DRAM and DCPMMs is not balanced, DRAM and DCPMMs are not on the same
channel or not all the same size).

**The requested goal may result in a non-optimal configuration due to
the population of DIMMs in the system.**  
App Direct capacity requested but the population of DCPMMs in the system
may result in reduced performance (i.e., DCPMMs are not the same size or
populated asymmetrically across the socket).

**The requested goal will result in App Direct capacity which is not
supported by the host software.**  
App Direct capacity requested but App Direct is not supported by the
currently installed host software.

**The requested goal will result in Memory Mode capacity that is
unusable with the currently selected platform BIOS volatile mode.**  
Memory Mode capacity requested by the platform BIOS is currently set to
1LM Mode.

**The requested goal was adjusted more than 10% to find a valid
configuration.**  
\> 10% adjustment from the requested goal

**The amount of mapped memory was limited based on the SKU resulting in
un-mapped capacity.**  
Mapped memory was limited based on the CPU SKU.

Therefore, before making any changes to the configuration, a prompt is
displayed showing the memory allocation goals that will be created on
each DCPMM as documented in the command Section
[???](#Show%20Memory%20Allocation%20Goal), along with any additional
confirmation messages. The force option can be used to override this
confirmation and proceed directly with creating the goals.

> 
> 
>     The following configuration will be applied:
>     SocketID DimmID MemorySize AppDirect1Size AppDirect2Size (Refer to
>     the command Section )
>     [Additional Confirmation Messages (see above)] Do you want to
>     continue?