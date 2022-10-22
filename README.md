# StripIRQFromCPULog
This is a dead simple command-line tool to strip interrupts from a 65816 CPU debugger transcript.

Usage:
```
    StripIRQFromCPULog.exe [inputLog] [outputLog]
```
For example,
```
    StripIRQFromCPULog.exe input.log output.log
```

In that case, if input.log contained
```
$80/BBF5 65 75       ADC $75    [$00:0075]   A:0008 X:000A Y:0002 P:envmXdizc
$80/BBF7 85 75       STA $75    [$00:0075]   A:0030 X:000A Y:0002 P:envmXdizc
*** IRQ
$00/84E5 5C E9 84 80 JMP $8084E9[$80:84E9]   A:0030 X:000A Y:0002 P:envmXdIzc
$80/84E9 C2 30       REP #$30                A:0030 X:000A Y:0002 P:envmXdIzc
$80/84EB 78          SEI                     A:0030 X:000A Y:0002 P:envmxdIzc
$80/84EC 8B          PHB                     A:0030 X:000A Y:0002 P:envmxdIzc
$80/84ED AB          PLB                     A:0030 X:000A Y:0002 P:envmxdIzc
$80/84EE 40          RTI                     A:0030 X:000A Y:0002 P:eNvmxdIzc
$80/BBF9 A5 6F       LDA $6F    [$00:006F]   A:0030 X:000A Y:0002 P:envmXdizc
$80/BBFB D0 05       BNE $05    [$BC02]      A:0008 X:000A Y:0002 P:envmXdizc
$80/BC02 A5 75       LDA $75    [$00:0075]   A:0008 X:000A Y:0002 P:envmXdizc
```
Then, output.log will be produced to contain
```
$80/BBF5 65 75       ADC $75    [$00:0075]   A:0008 X:000A Y:0002 P:envmXdizc
$80/BBF7 85 75       STA $75    [$00:0075]   A:0030 X:000A Y:0002 P:envmXdizc
$80/BBF9 A5 6F       LDA $6F    [$00:006F]   A:0030 X:000A Y:0002 P:envmXdizc
$80/BBFB D0 05       BNE $05    [$BC02]      A:0008 X:000A Y:0002 P:envmXdizc
$80/BC02 A5 75       LDA $75    [$00:0075]   A:0008 X:000A Y:0002 P:envmXdizc
```

giving a continuous transcript skipping over the interrupt. The program handles both IRQ and NMI, as well as the case where NMI overlaps with an IRQ.

When the program is built in Debug config, the arguments are hard-coded. When the program is built in Release config, it takes command line arguments. 

## Build
This program is in C++ built as a Visual Studio 2019 solution.

## Usage Environment
This program is for Windows 7/Windows 10+ x86-compatible environments.
