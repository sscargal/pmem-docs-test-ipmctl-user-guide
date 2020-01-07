# NAME

ipmctl-start-session - Starts a recording or playback
>     session.

# SYNOPSIS

> 
> 
>     ipmctl start [OPTIONS] -session -mode (record|playback|playback_manual)

# DESCRIPTION

Starts a recording or playback session. The recording session records
the platform’s ACPI NFIT, PCAT, PMTT tables, SMBIOS tables, and FIS
mailbox transactions that occur during the recording session. The normal
use-case would be to start a recording session, execute commands (i.e.
create -goal, show -sensors, etc.) to be recorded, dump the recorded
session using the [???](#Dump%20Session) command, followed by stopping
the session using the [???](#Stop%20Session) command. The "dumped"
session can then be loaded and "played" back on any platform that can
execute the ipmctl tool.

The playback session has two modes, 'playback' and 'playback\_manual'.
The 'playback' mode will automatically execute all commands that were
previously recorded. The 'playback\_manual' mode allows commands to be
executed one at a time in a manual fashion. Note, the
[???](#Show%20Session) command displays the order and commands to
execute, where the '\*' denotes which command to execute next.

# OPTIONS

  - \-f; -force  
    Do not warn the user that starting a new session terminates an
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
    Specifies to start a session.

  - \-mode (record|playback|playback\_manual)  
    The session modes supported. One of:
    
      - "record" - records data associated with command execution
    
      - "playback" - automatically executes commands previously recorded
    
      - "playback\_manual" - enables manual execution of commands
        previously recorded

# EXAMPLES

Start a recording session.

> 
> 
>     ipmctl start -session -mode record

Automatically execute commands in a session.

> 
> 
>     ipmctl start -session -mode playback

Allow for manual execution of commands in playback mode

> 
> 
>     ipmctl start -session -mode playback_manual

# LIMITATIONS

Recordings should be played back on the same IPMCTL version that created
the recording. Recordings taken in UEFI should be played back in the
UEFI environment (simulated or real). Recordings taken in an OS are
binary compatible with other OS versions of IPMCTL, i.e. recording taken
in Linux can be played back in Windows.

# RETURN DATA

In 'playback' mode the output will be a concatination of the output from
each played back command.

# SAMPLE OUTPUT