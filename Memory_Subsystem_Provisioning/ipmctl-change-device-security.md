# NAME

ipmctl-change-device-security - Changes the DCPMM security lock
>     state

# SYNOPSIS

> 
> 
>     ipmctl set [OPTIONS] -dimm [TARGETS] Lockstate=(Unlocked|Disabled|Frozen)
>     Passphrase=(string)

# DESCRIPTION

Changes the data-at-rest security lock state for the persistent memory
on one or more DCPMMs.

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

  - \-source (path)  
    File path to a local file containing the new passphrase (1-32
    characters).

# TARGETS

  - \-dimm \[DimmIDs\]  
    Changes the lock state of a specific DCPMMs by supplying one or more
    comma separated DCPMM identifiers. However, this is not recommended
    as it may put the system in an undesirable state. The default is to
    modify all manageable DCPMMs.

# PROPERTIES

  - LockState  
    The desired lock state.
    
      - "Disabled": Removes the passphrase on an DCPMM to disable
        security. Permitted only when LockState is Unlocked.
    
      - "Unlocked": Unlocks the persistent memory on a locked DCPMM.
    
      - "Frozen": Prevents further lock state changes to the DCPMM until
        the next reboot.

  - Passphrase  
    The current passphrase (1-32 characters). For better passphrase
    protection, specify an empty string (e.g., Passphrase="") to be
    prompted for the current passphrase or to use a file containing the
    passphrases with the source option.

# EXAMPLES

Unlocks device 0x0001.

> 
> 
>     ipmctl set -dimm 0x0001 LockState=Unlocked Passphrase=""

Unlocks device 0x0001 by supplying the passphrase in the file
"mypassphrase.file". In this example, the format of the file would be:

\#ascii  
Passphrase=myPassphrase

> 
> 
>     ipmctl set -source myfile.file -dimm 0x0001 LockState=Unlocked
>     Passphrase=""

# LIMITATIONS

To successfully execute this command, the caller must have the
appropriate privileges and the specified DCPMMs must be manageable by
the host software, have security enabled, not be in the "Frozen" or
"Exceeded" lock states, and not executing a long operation (ARS,
Overwrite, FWUpdate).

# RETURN DATA

If an empty string is provided for the passphrase property and the
source option is not included, the user will be prompted (once for all
DCPMMs) to enter the current passphrase. The passphrase characters are
hidden.

Current passphrase: **\***\*

For each DCPMM, the CLI will indicate the status of the security state
change. If a failure occurs when changing multiple DCPMMs, the process
will exit and not continue updating the remaining DCPMMs.

# SAMPLE OUTPUT

> 
> 
>     Unlock DIMM (DimmID): Success
>     Unlock DIMM (DimmID): Error (Code) - (Description)
>     Remove passphrase from DIMM (DimmID): Success
>     Remove passphrase from DIMM (DimmID): Error (Code) - (Description)
