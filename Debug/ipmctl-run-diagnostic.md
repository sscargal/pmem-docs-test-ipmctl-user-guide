# NAME

ipmctl-run-diagnostic - Runs a diagnostic test

# SYNOPSIS

> 
> 
>     ipmctl start [OPTIONS] -diagnostic [TARGETS]

# DESCRIPTION

Runs a diagnostic test.

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

# TARGETS

  - \-diagnostic \[Quick|Config|Security|FW\]  
    Run a specific test by supplying its name. By default all tests are
    run. One of:
    
      - "Quick" - This test verifies that the DCPMM host mailbox is
        accessible and that basic health indicators can be read and are
        currently reporting acceptable values.
    
      - "Config" - This test verifies that the BIOS platform
        configuration matches the installed hardware and the platform
        configuration conforms to best known practices.
    
      - "Security" - This test verifies that all DCPMMs have a
        consistent security state. It’s a best practice to enable
        security on all DCPMMs rather than just some.
    
      - "FW" - This test verifies that all DCPMMs of a given model have
        consistent FW installed and other FW modifiable attributes are
        set in accordance with best practices.  
        Note that the test does not have a means of verifying that the
        installed FW is the optimal version for a given DCPMM model just
        that it’s been consistently applied across the system.

  - \-dimm \[DimmIDS\]  
    Runs a diagnostic test on specific DCPMMs by optionally supplying
    one or more comma-separated DCPMM identifiers. The default is to run
    the specified tests on all manageable DCPMMs. Only valid for the
    Quick diagnostic test.

# EXAMPLES

Runs all diagnostics.

> 
> 
>     ipmctl start -diagnostic

Runs the quick check diagnostic on DCPMM 0x0001

> 
> 
>     ipmctl start -diagnostic Quick -dimm 0x0001

# LIMITATIONS

If a DCPMM is unmanageable, then Quick test will report the reason,
while Config, Security and FW tests will skip unmanageable DCPMMs.

# RETURN DATA

Each diagnostic generates one or more log messages. A successful test
generates a single log message per DCPMM indicating that no errors were
found. A failed test might generate multiple log messages each
highlighting a specific error with all the relevant details. Each log
contains the following information.

  - TestName  
    The test name. One of:
    
      - "Quick"
    
      - "Config"
    
      - "Security"
    
      - "FW"

  - State  
    The severity of the error. One
            of:
    
      - "Ok"
    
      - "Warning"
    
      - "Failed"
    
      - "Aborted"
        
            NOTE: State is promoted to the highest severity result from the test group.

  - Message  
    A free form textual description of the error.