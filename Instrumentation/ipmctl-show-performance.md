# NAME

ipmctl-show-performance - Shows performance metrics for one or more
DCPMMs

# SYNOPSIS

> 
> 
>     ipmctl show [OPTIONS] -performance [METRICS] [TARGETS]

# DESCRIPTION

Shows performance metrics for one or more DCPMMs.

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

# METRICS

Restricts output to a specific performance metric by supplying the
metric name. See RETURN DATA for more information. One of:

  - MediaReads

  - MediaWrites

  - ReadRequests

  - WriteRequests

  - TotalMediaReads

  - TotalMediaWrites

  - TotalReadRequests

  - TotalWriteRequests

The default is to display all performance metrics.

# TARGETS

  - \-dimm \[DimmIDs\]  
    Restricts output to the performance metrics for specific DCPMM by
    supplying one or more comma separated DCPMM identifiers. The default
    is to display performance metrics for all manageable DCPMM.

# EXAMPLES

Shows all performance metrics for all DCPMMs in the server.

> 
> 
>     ipmctl show -dimm -performance

Shows the number of 64 byte reads since last AC cycle for all DCPMMs in
the server.

> 
> 
>     ipmctl show -dimm -performance MediaReads

# RETURN DATA

This command displays a table of the specified metrics for each
specified DCPMM. Applying a specific DCPMM target limits the rows in the
table. Applying a specific metric name target limits the columns in the
table.

  - DimmID  
    The DCPMM identifier

  - MediaReads  
    Number of 64 byte reads from media on the DCPMM since last AC cycle.

  - MediaWrites  
    Number of 64 byte writes to media on the DCPMM since last AC cycle.

  - ReadRequests  
    Number of DDRT read transactions the DCPMM has serviced since last
    AC cycle.

  - WriteRequests  
    Number of DDRT write transactions the DCPMM has serviced since last
    AC cycle.

  - TotalMediaReads  
    Number of 64 byte reads from media on the DCPMM over its lifetime.

  - TotalMediaWrites  
    Number of 64 byte writes to media on the DCPMM over its lifetime.

  - TotalReadRequest  
    Number of DDRT read transactions the DCPMM has serviced over its
    lifetime.

  - TotalWriteRequest  
    Number of DDRT write transactions the DCPMM has serviced over its
    lifetime.
