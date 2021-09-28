# implementing-malloc-and-free-in-c-for-a-dynamic-allocator-for-c-programs
Wrote the malloc and free routines of a dynamic memory allocator for C programs using both the explicit free list allocator and segregated free list allocator approaches.

<br/>

**Project context:** <br/>

This was a school project in which I wrote my own version of the malloc and free routines of a dynamic memory allocator for C programs.



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

**Folders and files used by the driver program (same for each folder in project root) :** <br/>
Folders
1. traces ()

Files









