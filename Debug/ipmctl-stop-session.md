# NAME

ipmctl-stop-session - Stops the active playback or recording session.

# SYNOPSIS

> 
> 
>     ipmctl stop [OPTIONS] -session

# DESCRIPTION

Stops the active playback or recording session.

# OPTIONS

  - \-f; -force  
    Do not warn the user that stopping a new session terminates an
    active recording session resulting in deleting recorded content.

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

  - \-session  
    Specifies to stop a session.

# EXAMPLES

Stop the current session.

> 
> 
>     ipmctl stop -session

# LIMITATIONS

# RETURN DATA

# SAMPLE OUTPUT

> 
> 
>     Successfully dumped 1060619 bytes to file.

Warning - Executing in playback mode\!

Stopping a session will free all recording content. Do you want to
continue? \[y/n\] y Stopped PBR session.
