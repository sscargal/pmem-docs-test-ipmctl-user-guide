# NAME

ipmctl-change-device-passphrase - Changes the security passphrase on
DCPMM

# SYNOPSIS

> 
> 
>     ipmctl set [OPTIONS] -dimm [TARGETS] Passphrase=(string) NewPassphrase=(string)
>     ConfirmPassphrase=(string)

# DESCRIPTION

Changes the security passphrase on one or more DCPMMs.

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

  - \-master  
    Changes the master passphrase. Valid only if master passphrase is
    enabled on specified DCPMMs (see MasterPassphraseEnabled attribute
    in section [???](#Show%20Device)).

  - \-default  
    Use this option when the current master passphrase is set to the
    default value. Valid only if used along with the '-master' option.
    May not be combined with the Passphrase property.

  - \-source (path)  
    File path to a local file containing the new passphrase (1-32
    characters).

> **Note**
> 
> The file does not need to contain the ConfirmPassphrase property

# TARGETS

  - \-dimm \[DimmIDs\]  
    Changes the passphrase on specific DCPMMs by supplying one or more
    comma separated DCPMM identifiers. However, this is not recommended
    as it may put the system in an undesirable state. The default is to
    change the passphrase on all manageable DCPMMs.

# PROPERTIES

  - Passphrase  
    The current passphrase (1-32 characters). For better passphrase
    protection, specify an empty string (e.g., Passphrase="") to be
    prompted for the current passphrase or to use a file containing the
    passphrases with the source option.

  - NewPassphrase  
    The new passphrase (1-32 characters). For better passphrase
    protection, specify an empty string (e.g., NewPassphrase="") to be
    prompted for the passphrase or to use a file containing the
    passphrase with the source option.

  - ConfirmPassphrase  
    Confirmation of the new passphrase (1-32 character and must match
    NewPassphrase). For better passphrase protection, specify an empty
    string (e.g., ConfirmPassphrase="") to be prompted for the
    passphrase or to use a file containing the passphrase with the
    source option.

# EXAMPLES

Changes the passphrase from mypassphrase to mynewpassphrase on all
DCPMMs.

> 
> 
>     ipmctl set -dimm Passphrase=mypassphrase NewPassphrase=mynewpassphrase
>      ConfirmPassphrase=mynewpassphrase

Changes the passphrase on all DCPMMs by having the CLI prompt for the
current and new
>     passphrases.

> 
> 
>     ipmctl set -dimm Passphrase="" NewPassphrase="" ConfirmPassphrase=""

Changes the passphrase on all DCPMMs by supplying the current and new
passphrases from the specified file. In this example, the format of the
file would
>     be:

\#ascii  
Passphrase=myOldPassphrase  
NewPassphrase=myNewPassphrase

> 
> 
>     ipmctl set -source passphrase.file -dimm Passphrase="" NewPassphrase=""
>     ConfirmPassphrase=""

Changes the default master passphrase to masterpassphrase on all
>     DCPMMs.

> 
> 
>     ipmctl set -master -default NewPassphrase=masterpassphrase ConfirmPassphrase=
>     masterpassphrase

Changes the master passphrase from masterpassphrase to
newmasterpassphrase on all
>     DCPMMs.

> 
> 
>     ipmctl set -master -dimm Passphrase=masterpassphrase NewPassphrase=newmasterpassphrase
>     ConfirmPassphrase=newmasterpassphrase

# LIMITATIONS

The specified DCPMM must be manageable by the host software, have
security enabled and not be in the "Frozen" or "Exceeded" lock states.

# RETURN DATA

If empty strings are provided for the passphrase properties and the
source option is not included, the user will be prompted (once for all
DCPMM) to enter the current passphrase, then again for the new
passphrase and then again to confirm the new passphrase as described
below. The passphrase characters are hidden.

Current passphrase: \*\*\*\*

For each DIMM, the CLI will indicate the status of the passphrase change
operation. If a failure occurs when updating the passphrase on multiple
DCPMMs, the process will exit and not continue updating the remaining
DCPMMs.

# SAMPLE OUTPUT

> 
> 
>     Change passphrase on DIMM (DimmID): Success

> 
> 
>     Change passphrase on DIMM (DimmID): Error (Code)-(Description)
