# NAME

ipmctl-version - Shows the DCPMM host software versions

# SYNOPSIS

> 
> 
>     ipmctl version [OPTIONS]

# DESCRIPTION

Shows the DCPMM host software versions.

# OPTIONS

  - \-h; -help  
    Displays help for the command.

# EXAMPLES

Displays the available version information for the DCPMM software
components.

> 
> 
>     ipmctl version

# RETURN DATA

By default returns the following inventory information.

  - Component  
    The name of the software component. One of:
    
      - \[Product Name\] Software Version: The DCPMM management software
        version
    
      - \[Product Name\] Driver Version: The vendor specific DCPMM
        driver version

  - Version  
    The current version of the software component if found or an error
    if not.

> **Note**
> 
> If the software version is incompatible, the version will be followed
> by an error message indicating such. If DCPMMs are found with a FIS
> implementation higher than supported by the SW version, this command
> will print a warning.
