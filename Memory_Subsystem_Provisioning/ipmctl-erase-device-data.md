# NAME

ipmctl-erase-device-data - Erases the persistent data on one or more
DCPMMs

# SYNOPSIS

> 
> 
>     ipmctl delete [OPTIONS] -dimm [TARGETS] Passphrase=(string)

# DESCRIPTION

Erases the persistent data on one or more DCPMMs. This commands invokes
the DCPMM 'Secure Erase' command.

> **Note**
> 
> This command does not zero out the persistent data, but instead
> randomizes the data.

# OPTIONS

  - \-f; -force  
    Erasing DCPMM data is a destructive operation which requires
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

  - \-master  
    Erases DCPMMs using master passphrase. Valid only if master
    passphrase is enabled on specified DCPMMs (see
    MasterPassphraseEnabled attribute in section [???](#Show%20Device)).

  - \-default  
    Use this option when the current master passphrase is set to the
    default value. Valid only if used along with the '-master' option.
    May not be combined with the Passphrase property.

  - \-source (path)  
    File path to a local file containing the new passphrase (1-32
    characters).

# TARGETS

  - \-dimm \[DimmIDs\]  
    Erases specific DCPMMs by supplying one or more comma-separated
    DCPMM identifiers. However, this is not recommended as it may put
    the system in an undesirable state. The default is to erase all
    manageable DCPMMs.

# PROPERTIES

  - Passphrase  
    If security state is disabled, then passphrase is not required and
    will be ignored if supplied.  
    If security state is enabled, then a passphrase must be supplied.  
    The current passphrase (1-32 characters). For better passphrase
    protection, specify an empty string (e.g., Passphrase="") to be
    prompted for the passphrase or to use a file containing the
    passphrase with the source option.

# EXAMPLES

Security disabled DCPMMs: Erases all the persistent data on all DCPMMs
in the system.

> 
> 
>     ipmctl delete -dimm

Security enabled specifics: Erases all the persistent data on all DCPMMs
in the system.

> 
> 
>     ipmctl delete -dimm Passphrase=123

Security enabled specifics: Erases all the persistent data on all DCPMMs
in the system using the default master passphrase.

> 
> 
>     ipmctl delete -master -default -dimm

Security enabled specifics: Erases all the persistent data on all DCPMMs
in the system using the master passphrase.

> 
> 
>     ipmctl delete -master -dimm Passphrase=masterpassphrase

Erases all the persistent data on all DCPMMs by having the CLI prompt
for the current passphrase.

> 
> 
>     ipmctl delete -dimm Passphrase=""

# LIMITATIONS

To successfully execute this command, the caller must have the
appropriate privileges and the specified DCPMM(s) must be manageable by
the host software, not be in the "Frozen" or "Exceeded" lock states and
any namespaces associated with the requested DCPMM(s) must be deleted
before running this command.

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
>     Erase DIMM (DimmID): Success
>     Erase DIMM (DimmID): Error (Code) - (Description)
