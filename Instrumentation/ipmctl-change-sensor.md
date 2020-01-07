# NAME

ipmctl-change-sensor - Changes the threshold or enabled state for DCPMMs
sensors

# SYNOPSIS

> 
> 
>     ipmctl set [OPTIONS] -sensor (SENSORS) [TARGETS]
>     AlarmThreshold=(temperature) EnabledState=(0|1)

# DESCRIPTION

Changes the non-critical alarm threshold or enabled state for one or
more DCPMMs sensors. Use the command Show Sensor to view the current
settings.

# OPTIONS

  - \-f; -force  
    Changing the sensor settings is a potentially destructive operation
    which requires confirmation from the user for each DCPMM. This
    option suppresses the confirmation.

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

# SENSORS

  - MediaTemperature  
    The current DCPMM media temperature in Celsius.  
    Valid values: 0-2047

  - ControllerTemperature  
    The current DCPMM controller temperature in Celsius.  
    Valid values 0-2047

  - PercentageRemaining  
    Remaining DCPMM’s life as a percentage value of factory expected
    life span.  
    Valid values: 1-99

# TARGETS

  - \-dimm \[DimmIDs\]  
    Restricts output to the sensors on specific DCPMMs by optionally
    supplying the DIMM target and one or more comma-separated DCPMM
    identifiers. The default is to display sensors for all manageable
    DCPMMs.

# PROPERTIES

  - AlarmThreshold  
    The upper (for temperatures) or lower (for spare capacity)
    non-critical alarm threshold of the sensor. If the current value of
    the sensor is at or above for thermal, or below for capacity, the
    theshold value, then the sensor will indicate a "NonCritical" state.
    Temperatures may be specified in degrees Celsius to a precision of
    1/16 a degree.

  - EnabledState  
    Enable or disable the non-critical alarm threshold. One of:
    
      - "0": Disable
    
      - "1": Enable

# EXAMPLES

Changes the media temperature threshold to 51 on the specified DCPMM and
enable the alarm.

> 
> 
>     ipmctl set -sensor MediaTemperature –dimm 0x0001 AlarmThreshold=51
>     EnabledState=1

# LIMITATIONS

The specified DCPMM(s) must be manageable by the host software.

# RETURN DATA

For each DCPMM, the CLI will indicate the status of the operation. If a
failure occurs when modifying multiple DCPMMs, the process will exit and
not continue modifying the remaining DCPMMs.

# SAMPLE OUTPUT

> 
> 
>     Modify (Sensor) settings on DIMM (DimmID): Success

> 
> 
>     Modify (Sensor) settings on DIMM (DimmID): Error (Code) -
>     (Description)