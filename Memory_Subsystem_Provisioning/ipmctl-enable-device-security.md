# NAME

ipmctl-enable-device-security - Enable data-at-rest security on DCPMM

# SYNOPSIS

> 
> 
>     ipmctl set [OPTIONS] -dimm [TARGETS] NewPassphrase=(string)
>     ConfirmPassphrase=(string)

# DESCRIPTION

Enable data-at-rest security for the persistent memory on one or more
DCPMMs by setting a passphrase.

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

> **Note**
> 
> The file does not need to contain the ConfirmPassphrase property

# TARGETS

  - \-dimm \[DimmIDs\]  
    Set the passphrase on specific DCPMMs by supplying one or more comma
    separated DCPMM identifiers. However, this is not recommended as it
    may put the system in an undesirable state. The default is to set
    the passphrase on all manageable DCPMMs.

# PROPERTIES

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

Set a passphrase on DIMM 0x0001.

> 
> 
>     ipmctl set -dimm 0x0001 NewPassphrase=123 ConfirmPassphrase=123

Sets a passphrase on DCPMM 0x0001 by supplying the passphrase in the
file mypassphrase.file. In this example, the format of the file would
be:

\#ascii  
NewPassphrase=myNewPassphrase

> 
> 
>     ipmctl set -source mypassphrase.file -dimm 0x0001 NewPassphrase="" ConfirmPassphrase=""

# LIMITATIONS

In order to successfully execute this command:

The caller must have the appropriate privileges. The specified DCPMM
must have security disabled and be manageable by the host software.

There must not be any goal creation pending.

# RETURN DATA

If empty strings are provided for the passphrase properties and the
source option is not included, the user will be prompted (once for all
DCPMMs) to enter the new passphrase and then again to confirm the new
passphrase as described below. The passphrase characters will be hidden.

New passphrase: \*\*\*\*  
Confirm new passphrase: \*\*\*\*

For each DCPMM, the CLI will indicate the status of the set passphrase
operation. If a failure occurs when setting the passphrase on multiple
DCPMMs, the process will exit and not continue updating the remaining
DCPMMs.

# SAMPLE OUTPUT

> 
> 
>     Set passphrase on DIMM (DimmID): Success

> 
> 
>     Set passphrase on DIMM (DimmID): Error (Code) - (Description)
