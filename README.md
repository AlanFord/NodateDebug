# NodateDebug
Building an STM32CubeIDE debug environment for a NoDate project

I've been fascinated by small, low-overhead libraries for developing software on STM32 platforms.  Lately I've been working with Maya Posch's NoDate library.  Unfortunately, I'm not very good at using gdb and really like graphical IDEs for debugging.  So these are my ideas for integrating a NoDate makefile project into a STM32Cube IDE debug environment.  Props to https://github.com/ethanhuanginst/STM32CubeIDE-Workshop-2019 for the crucial basic steps.  Note that the instructions that follow were developed for use on Linux.  Some modification may be required for use with Windows or MacOS.

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
   * Drag all "stm32_hp141_lcd" file (except out.elf) and folders into "stm32_hp141_lcd" in Project Exploere of STM32CubeIDE:  
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
