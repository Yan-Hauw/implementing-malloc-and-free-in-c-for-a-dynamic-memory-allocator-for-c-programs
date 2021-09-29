# implementing-malloc-and-free-in-c-for-a-dynamic-allocator-for-c-programs
Wrote the malloc and free routines of a dynamic memory allocator for C programs using both the explicit free list allocator and segregated free list allocator approaches.

<br/>

**Project context:** <br/>

This was a school project in which I wrote my own version of the malloc and free routines of a dynamic memory allocator for C programs.

See section titled **Code in mm.c :** for how the allocator implementation was improved from the starter code that was provided by the school instructor at the start of the project.

<br/>

**Folder and file structure in repository:** <br/>

At the root of this repository, there are 3 folders whose contents are very similar. 
Each folder is dedicated to one type of implementation of the dynamic memory allocator and each folder is named accordingly. <br/>

The 3 allocator implementations encountered in this project are: <br/>
1. Segregated list dynamic memory allocator <br/>
2. Explicit free list dynamic memory allocator <br/>
3. Implicit list dynamic memory allocator <br/>

The only file that is different across the 3 folders is mm.c . <br/>

Each folder contains:<br/>
1. Its own implementation of the malloc and free routines belonging to its parent folder, contained in the file mm.c . <br/>
2. A driver program that allows the programmer to evaluate the performance of the implementation of the malloc and free routines contained in that folder. <br/>

<br/>

**Folders and files in each allocator implementation :** <br/>
Folders
1. traces (contains trace files (.rep files) and files to manipulate the trace files (.pl files and a Makefile)) <br/>

I do not understand the files in the traces folder well as these were not written by me. These files were provided by the instructor of the course. 
To further understand the trace files that are used by the driver program, look at the README file in the traces folder. <br/>
<br/>

Note: The {realloc,realloc2}-bal.rep trace files were not used because the mm.c program was not evaluated for its realloc routines. These trace files were left there in case removing them would affect the functioning of the driver program. 


Files <br/>

1. mm.c (Description given above)

2. mdriver.c (Contains the code for the driver program)

3. The 10+ remaining files in the same directory as mm.c are used by the driver program for configuration and to measure the speed of the malloc and free routines in mm.c .
    - I do not understand these remaining files well as these were not written by me. They were provided by the instructor of the course. To further understand these files, look at the README file in the same directory as mm.c.

<br/>


**Code in mm.c :** <br/>

The progression from implicit list to explicit list to segregated list allocator from project start to project end:

  - At the start of the project, all files in the **Implicit list dynamic memory allocator** folder were provided by the instructor in the above described file/folder structure.

  - The malloc and free routines of the implicit allocator were not written by me.

  - The code in mm.c was then changed to improve the malloc and free routines to those of an **Explicit free list dynamic memory allocator**.

  - After the malloc and free routines of the explicit free list allocator were implemented, the malloc and free routines in mm.c were further improved to those of a **Segregated list dynamic memory allocator**.

  - Throughout the project, the only file that was modified was mm.c . The reason that each folder in the GitHub repository has its own driver program is to allow people who are not familiar with the project to easily test the mm.c files for the different allocator implementations.


Notes: <br/>
1. The code is not well refactored. I aim to write more concise and readable code if I was to write more future projects in C.
2. Since the mm.c program was not evaluated for its realloc routine, this routine was not modified from the naive mm_realloc function that was provided in the starter code. The starter code was left there in case removing it would affect the functioning of the driver program. 
3. The heap consistency checker **mm_checkheap() method** in mm.c: 
    - The mm_checkheap() method was not modified from what was initially provided by the instructor in the mm.c start code. Hence, in all 3 allocators it does not have a purpose. This method was an option provided by the course instructor to scan the heap and check it for consistency to help with debugging the code. 
    - I decided to only use The GNU Debugger (GDB) to detect bugs and to not write a heap checker. In hindsight, it may have helped to write a good heap checker in addition to using GDB.

<br/>


**How the driver program evaluates the mm.c code :** <br/>

The malloc and free routines in mm.c were evaluated by the driver program according to the following metrics:
1. Correctness of malloc and free routines
    - To check whether the malloc and free routines are incorrectly implemented and contain bugs.
2. Space utilization
    - The peak ratio between the aggregate amount of memory used by the driver (i.e. allocated via the malloc routine but not yet freed by the free routine) and the size of the heap used by the allocator, where the optimal ratio is 1.
3. Throughput
    - The average number of operations completed per second

The driver program summarizes the performance of the allocator by computing a performance index, P, which is a score out of 100. The performance index is based on 2 factors:
1. Scaled Utilization - U<sub>s</sub>: This is calculated by first calculating the weighted average of the utilizations (U<sub>avg</sub>) across traces. Some traces are worth more than others. The formula for scaling is: 

<br/>

![equation](http://latex2png.com/pngs/5a8c907f126b4ce93a4fd680488d7ddd.png) 

<br/>

2. Weighted harmonic mean of throughput - T: The harmonic mean is used to understand averages for rates. Throughput is a rate. The driver program uses weighted harmonic mean to emphasize some traces.



<br/>

**How to test the program :** <br/>

git clone the project repository to a local folder of your choice. Once cloned, navigate to local folder that contains the root folder of the repository, and go into whichever allocator implementation you would like to test.<br/>

The following commands should only be run in the same directory where the mm.c file is found:

1. Build the project (i.e. the driver program and mm.c)

    - To build a fully optimized excutable file for the driver program, type "make" into the command line.

    - Run the driver to test for correctness and print the performance index:

        - To only test mm.c for correctness and print the performance index, type "./mdriver" into the command line.

        - To do the above AND print a performance breakdown for each trace file, type "./mdriver -v" into the command line.

        - To print a performance breakdown for each trace file and additional diagnostic information, type "./mdriver -V" into the command line.

        - To run the driver for only one specific trace file in the traces folder, type the following command into the command line:
```console
            ./mdriver -f traces/<insert name of trace file here>
```



2. If you would like to change the mm.c code and do debugging using gdb

    - Instead of following the above commands, build an optimized excutable file for the driver program. Type "make debug" into the command line


    - Then start running the driver program with GDB using the command "gdb ./mdriver"


    - Continue debugging based on your own knowledge of GDB commands. I cannot anticipate how this program will be used by other people.

<br/>



The above commands should remain the same regardless of which of the 3 allocator implementations you are testing. To ensure smooth testing of the 3 mm.c files, do not reorganise any of the files or folders.


If the malloc and free routines are incorrectly implemented and contain bugs, the driver program will crash and print a segmentation fault error message or get stuck in the process of running and never print the performance index.











