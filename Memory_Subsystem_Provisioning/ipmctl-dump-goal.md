# NAME

ipmctl-dump-goal - Stores the current system configuration in a file

# SYNOPSIS

> 
> 
>     ipmctl dump [OPTIONS] -destination (path) -system -config

# DESCRIPTION

Store the currently configured memory allocation settings for all DCPMMs
in the system to a file in order to replicate the configuration
elsewhere. Apply the stored memory allocation settings using the command
Section [???](#Load%20Memory%20Allocation%20Goal).

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

# EXAMPLES

Stores the memory allocation settings from all the DCPMMs into the file
"config.txt".

> 
> 
>     ipmctl dump -destination config.txt -system -config

# LIMITATIONS

Only memory allocation settings for manageable DCPMMs that have been
successfully applied by the BIOS are stored in the file. Unconfigured
DCPMMs are not included, nor are memory allocation goals that have not
been applied.

# RETURN DATA

The CLI will indicate the overall status of the operation when complete.
If a failure occurs when dumping the memory allocation from multiple
DCPMMs, the process will stop and the output file will be removed.

The output file is formatted as an ASCII file with one row per DCPMM
containing the following comma-separated values.

  - SocketID  
    unsigned short int Identifier for the socket the DCPMM is associated
    with.

  - DimmHandle  
    unsigned int DCPMM device handle.

  - Capacity  
    unsigned long long int Total capacity of the DCPMM in GiB.

  - MemorySize  
    unsigned long long int Capacity of the DCPMM allocated as Memory
    Mode in GiB.

  - AppDirect1Size  
    unsigned long long int Capacity of the DCPMM allocated for the first
    App Direct interleave set in GiB.

  - AppDirect1Format  
    unsigned short int Bit mask representing the interleave format of
    the first App Direct interleave set.

  - AppDirect1Mirrored  
    unsigned char 1 if the first App Direct interleave set is mirrored,
    0 otherwise.

  - AppDirect1Index  
    unsigned short int Unique index of the first App Direct interleave
    set.

  - AppDirect2Size  
    unsigned long long int Capacity of the DCPMM allocated for the
    second App Direct interleave set in GiB.

  - AppDirect2Format  
    unsigned short int Bit mask representing the interleave format of
    the second App Direct interleave set.

  - AppDirect2Mirrored  
    unsigned char 1 if the second App Direct interleave set is mirrored,
    0 otherwise.

  - AppDirect2Index  
    unsigned short int Unique index of the second App Direct interleave
    set.

# SAMPLE OUTPUT

> 
> 
>     Successfully dumped system configuration to file: config.csv

config.csv contents:

> 
> 
>     #SocketID,DimmHandle,Capacity,MemorySize,AppDirect1Size,AppDirect
>     1Format,AppDirect
>     1Mirrored,AppDirect1Index,AppDirect2Size,AppDirect2Format,AppDire
>     ct2Mirrored,AppDirect2Index
>     1,4385,64,64,0,0,0,0,0,0,0,0
>     1,4401,64,64,0,0,0,0,0,0,0,0
>     1,4417,64,64,0,0,0,0,0,0,0,0
>     1,4433,64,64,0,0,0,0,0,0,0,0
>     1,4449,64,64,0,0,0,0,0,0,0,0
