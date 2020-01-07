# NAME

ipmctl-delete-pcd - Clears select partition data from the PCD

# SYNOPSIS

> 
> 
>     ipmctl delete [OPTIONS] -pcd [TARGETS]

# DESCRIPTION

When LSA is specified, the namespace label storage area partition in the
platform configuration data from one or more DCPMMs is cleared. This is
a destructive operation which will clear the entire namespace label
storage area including all namespaces labels and the namespace label
index block in order to re-purpose the DCPMM(s) for use in a different
operating system. All data on any deleted namespace(s) becomes
inaccessible.

> **Note**
> 
> Deleting PCD LSA partition data removes any logical OS namespace
> mapping to the persistent memory data, but does not explicitly delete
> or modify user data found in persistent memory.

When Config is specified, the Current, Input, and Output Data Size and
Start Offset values in the Configuration header are set to zero, making
those tables invalid.

> **Note**
> 
> This action can be useful when moving DCPMMs from one system to
> another, as goal creation rules may restrict provisioning dimms with
> an existing configuration.

> **Note**
> 
> When Config is specified, only PCD partition 1 is modified. If the
> platform is rebooted prior to creating a new goal on any targeted
> DCPMMs, UEFI platform firmware will detect the missing tables and, if
> possible, restore previous config using the PCD partition 0 tables.

> **Warning**
> 
> **This command may result in data loss. Data should be backed up to
> other storage before executing this command. Because of data
> dependencies, other commands may be affected until the system has been
> rebooted**.

# OPTIONS

  - \-f; -force  
    Deleting the PCD data is a destructive operation which requires
    confirmation from the user for each DCPMM. This option suppresses
    the confirmation.

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
    Deletes the PCD data on specific DCPMMs by supplying one or more
    comma-separated DCPMM identifiers. The default is to delete the PCD
    data for all manageable DCPMMs.

  - \-pcd \[Config|LSA\]  
    Restricts clearing select partition data in the platform
    configuration data area. The default is to clear both. One of:
    
      - Config - Configuration management information
    
      - LSA - Namespace label storage area

# EXAMPLES

Clears the namespace label storage area from all manageable DCPMMs

> 
> 
>     delete -dimm -pcd LSA

Clears the Cin, Cout, Ccur tables from all manageable DCPMMs

> 
> 
>     delete -dimm -pcd Config

# LIMITATIONS

The specified DCPMM(s) must be manageable by the host software, and if
data-at-rest security is enabled, the DCPMMs must be unlocked. Any
existing namespaces associated with the requested DCPMM(s) should be
deleted before running this command.

# RETURN DATA

For each DCPMM, the CLI will indicate the status of the operation. If a
failure occurs when deleting the platform configuration data from
multiple DCPMMs, the process will continue deleting the remaining
DCPMMs.