# NodateDebug
Building an STM32CubeIDE debug environment for a NoDate project

I've been fascinated by small, low-overhead libraries for developing software on STM32 platforms.  Lately I've been working with Maya Posch's [NoDate](https://github.com/MayaPosch/Nodate) library.  Unfortunately, I'm not very good at using gdb and really like graphical IDEs for debugging.  So these are my ideas for integrating a NoDate makefile project into a STM32Cube IDE debug environment.  Props to https://github.com/ethanhuanginst/STM32CubeIDE-Workshop-2019 for the crucial basic steps that I built upon.  Note that the instructions that follow were developed for use on Linux.  Some modification may be required for use with Windows or MacOS.

## Steps

0. Preparations
   * Install the NoDate library and set the required environment variables.  Test the installation by compiling one of the included examples.
   * Install the STM32CubeIDE environment.

1. Start a new STM32 project
   
   * Select "Help -->Information Center":  
     ![](images/stm32_hp141_lcd-start-new-project-0.png)
   
     
   
   * Press "Start new STM32 project":
     ![](images/stm32_hp141_lcd-start-new-project-1.png)
   * Select "32F746DISCOVERY" board from "Board Selector" and press "Next" button:  
     ![](images/stm32_hp141_lcd-start-new-project-2.png)
   * Assign "Project Name" and "Location", and make sure "Targeted Project Type" is "Empty". Press "Finish" button when all is set.  
     ![](images/stm32_hp141_lcd-start-new-project-3.png)
   
5. Prepare for compiling   
   * Delete all folders and files:  
![](images/stm32_hp141_lcd-start-new-project-5.png)
   * Drag all the contents of your NoDate project into the project folder in Project Exploere of STM32CubeIDE:  
     ![](images/stm32_hp141_lcd-start-new-project-6.png)
   * Select "Copy files and folders" and then press "OK":
![](images/stm32_hp141_lcd-start-new-project-7.png)
   
8. Compile the code
   
   * Select "Properties":  
![](images/stm32_hp141_lcd-start-new-project-9.png)
   
   * Modify "Builder Settings" (uncheck "Generate Makefiles automatically" and delete string "Debug" in Build directory) as shown below:  
![](images/stm32_hp141_lcd-start-new-project-10.png)
     
   * Select "Build Project":  
![](images/stm32_hp141_lcd-start-new-project-8.png)
     
     

11. Start debug

    * Select "Debug As --> STM32 MCU C/C++ Application"  
    ![](images/stm32_hp141_lcd-start-new-project-11.png)
    * Press "OK" button in "Edit Configuration":  
    ![](images/stm32_hp141_lcd-start-new-project-13.png)
    * Press "Resume" button to run the code:  
    ![](images/stm32_hp141_lcd-start-new-project-12.png)


12. (Optional) Adjust the compiler optimization settings
You may find that, when stepping the debugger through your source code, the debugger begins jumping around in an unnatural manner.  This isn't a show-stopper, but may be a little disconcerting.  The behavior is caused by NoDate's default compiler optimization level.  A more sedate behavior can be induced by adding the following line to the Project makefile:\
	APP_FLAGS = -O0\
Be warned, however, that this change will result in a larger compiled program.  If you have a microcontroller with a small amount of flash storage, changing the optimization settings may result in a compiled program too large for your microcontroller.  If so, remove the APP_FLAGS line from the makefile.

   
That's all it takes to debug an application that uses the NoDate library!  If, however, you wish to contribute to the development of the NoDate library you may want to have the debugger step through the library code.  That requires a few more configuration steps.
   
1. Add the NoDate libraries to the Project   
    * Drag the following folders from the NoDate library into "stm32_hp141_lcd" in Project Exploere of STM32CubeIDE:  
        * arch/stm32/cpp/boards
        * arch/stm32/cpp/core
        * arch/stm32/cpp/libs
        * arch/stm32/cpp/peripherals
    * Select "Link to files and folders" and then press "OK":
     
2. (Optional) Add "defines" from the Makefile to the Project
   The IDE will work at this point, but some of the NoDate source code may be marked as unused code in the display because the IDE doesn't know the values of numerouse preprocessor defines.  These can be added to the Project settings to improve the IDE display.
      * Rebuild the project and examine the Console window.  Find a compile command (beginning with "arm-none-eabi-g++") and search for command options that begin with "-D".  Enter these option (without the -D) in the 
    * Select "Link to files and folders" and then press "OK":


