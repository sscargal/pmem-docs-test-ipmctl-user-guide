# NAME

ipmctl-dump-session - Dumps content captured during a recording session.
Captured content includes ACPI, SMBIOS tables, and FIS requests and
responses. The resulting session file that is generated can be used to
playback commands recorded on a real platform in a simulated
environment, making it possible to debug issues offline.

# SYNOPSIS

> 
> 
>     ipmctl dump [OPTIONS] -destination (path) -session

# DESCRIPTION

Dumps content captured during a recording session. Captured content
includes ACPI, SMBIOS tables, and FIS requests and responses. The
resulting session file that is generated can be used to playback
commands recorded on a real platform in a simulated environment, making
it possible to debug issues offline.

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

# TARGET

  - \-destination (path)  
    An absolute or relative path including the filename, where the
    contents of the active session will be copied to.

  - \-session  
    Specifies to dump the contents associated with an active recording
    session.

# EXAMPLES

Dump the contents associated with the current active recording session
to /tmp/session.pbr.

> 
> 
>     ipmctl dump -destination /tmp/session.pbr -session

# LIMITATIONS

To successfully execute this command, there must be an active recording
session.

# RETURN DATA

The resulting file includes, NFIT, PCAT, PMTT and SMBIOS tables that are
used by IPMCTL to determine the DCPMM topology. DCPMM data that is
transfered to/from DCPMM(s) over the mailbox interface.

# SAMPLE OUTPUT

> 
> 
>     Successfully dumped 1060619 bytes to file.
