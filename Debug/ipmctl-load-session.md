# NAME

ipmctl-load-session - Loads content captured during a recording session
into internal memory buffers. Captured content includes ACPI, SMBIOS
tables, and FIS requests and responses.

# SYNOPSIS

> 
> 
>     ipmctl load [OPTIONS] -source (path) -session

# DESCRIPTION

Loads content captured during a recording session into internal memory
buffers. Captured content includes ACPI, SMBIOS tables, and FIS requests
and responses. A loaded session can be executed using the 'start
-session' command.

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

  - \-source (path)  
    An absolute or relative path including the filename.

  - \-session  
    Specifies that the source file contains recording data.

# EXAMPLES

Load the contents of a previously recorded session from
/tmp/session.pbr.

> 
> 
>     ipmctl load -source /tmp/session.pbr -session

# LIMITATIONS

# RETURN DATA

# SAMPLE OUTPUT

> 
> 
>     Successfully loaded 1060619 bytes to session buffer.
