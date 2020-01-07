# NAME

ipmctl-dump-support-data - Dumps a support snapshot to a
>     file

# SYNOPSIS

> 
> 
>     ipmctl dump [OPTIONS] -destination (file_prefix) [-dict (file)] -support

# DESCRIPTION

Creates a support snapshot and dump support data to a file for off-line
analysis by support personnel. Support data may include system log(s),
error log(s), trace log(s), platform configuration, sensor information
and diagnostic results.

Commands executed: \* version \* show -memoryresources \* show -a
-system -capabilities \* show -a -topology \* start -diagnostic \* show
-system

Commands executed per DCPMM: \* show -a -dimm \* show -a -sensor -dimm
\* show -pcd -dimm \* show -error media -dimm \* show -error thermal
-dimm

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

  - \-destination (file\_prefix)  
    This command creates a text file with a name starting with the given
    file\_prefix option and dumps the platform support information into
    it. In addition, this command also outputs the debug log information
    in separate files. Refer to ***Dump Debug Log*** for more details.

  - \-dict (path)  
    Optional file path to the dictionary file. If supplied, the command
    will create both the binary debug log and a text file with decoded
    log data with the file prefix specified by -destination. This option
    is used only to dump the debug log information.

# EXAMPLES

Creates a text file named dumpfile\_platform\_support\_info.txt and
stores the platform supported data in that file. Also, dumps the debug
log info in the related files that start with the file name
dumpfile\_\*. Refer to ***Dump Debug Log*** for more info on the output
files.

> 
> 
>     ipmctl dump -destination dumpfile_ -dict nlog_dict.1.1.0.0000.txt -support

# RETURN DATA

Simply returns the status of the operation.

# SAMPLE OUTPUT

Dump support data succesfully written to
dumpfile\_platform\_support\_info.txt
