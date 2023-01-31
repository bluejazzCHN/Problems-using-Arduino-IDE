# Compilation related problems 

## 1. cc1.exe: some warnings being treated as errors

+ Due to the application of a large number of packages, warning information appeared during the compilation process, causing the compiler to upgrade the warning to error. 

For example, if you compile M5Stack AtomS3 demo Multitask, you will see below warning info.

```
In file included from c:\Users\songj\Documents\Arduino\libraries\FastLED\src/FastLED.h:67,
                 from c:\Users\songj\Documents\Arduino\libraries\M5AtomS3\src\utility\LED_DisPlay.h:4,
                 from c:\Users\songj\Documents\Arduino\libraries\M5AtomS3\src\utility\LED_DisPlay.cpp:1:
c:\Users\songj\Documents\Arduino\libraries\FastLED\src/fastspi.h:145:23: note: #pragma message: No hardware SPI pins defined.  All SPI access will default to bitbanged output
 #      pragma message "No hardware SPI pins defined.  All SPI access will default to bitbanged output"
c:\Users\songj\Documents\Arduino\libraries\M5AtomS3\src\utility\In_eSPI.cpp:870:29: warning: missing initializer for member 'spi_bus_config_t::data5_io_num' [-Wmissing-field-initializers]
c:\Users\songj\Documents\Arduino\libraries\M5AtomS3\src\utility\In_eSPI.cpp:870:29: warning: missing initializer for member 'spi_bus_config_t::data6_io_num' [-Wmissing-field-initializers]
c:\Users\songj\Documents\Arduino\libraries\M5AtomS3\src\utility\In_eSPI.cpp:870:29: warning: missing initializer for member 'spi_bus_config_t::data7_io_num' [-Wmissing-field-initializers]
```
+ Solution

1. find platform.txt file in C:\Users\songj\AppData\Local\Arduino15\packages\m5stack\hardware\esp32\2.0.6\ (You need to adjust the directory based on the arduino ide version information and hardware vendor information)
2.  find the below code segment

```
# Arduino Compile Warning Levels
compiler.warning_flags=-w
compiler.warning_flags.none=-w
compiler.warning_flags.default=
compiler.warning_flags.more=-Wall -Werror=all
compiler.warning_flags.all=-Wall -Werror=all -Wextra
```
change to

```
# Arduino Compile Warning Levels
#compiler.warning_flags=-w
#compiler.warning_flags.none=-w
compiler.warning_flags.default=-Wno-error
#compiler.warning_flags.more=-Wall -Werror=all
#compiler.warning_flags.all=-Wall -Werror=all -Wextra
```

$ -Wno-error tells the compiler to ignore warning information $ 
