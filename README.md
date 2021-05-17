# Operating Systems Concepts
----------------------------
## Course Information

This repository contains a summary of my learnings in concepts of operating systems with resourses available online and assignments that I have done as part of learning.

Operating system is the core part for managing software and hardware resources in a computer system. And the below resources were helpful in covering the basic concepts, principles and implementation techniques of operating systems.

### Topics covered

    Process Management : process, thread, scheduling.
    Concurrency        : mutual exclusion,synchronization, semaphores, deadlocks.
    Memory Management  : allocation, protection, hardware support, paging, segmentation.
    Virtual Memory     : demand paging, allocation, replacement, swapping, segmentation, TLBs.
    File Management    : naming, file operations and their implementation.
    File Systems       : allocation, free space management, directory management, mounting I/O.
    Management         : device drivers, disk scheduling.
    
### Resources

- lecture notes : [stanford's CS140: Operating Systems](https://web.stanford.edu/~ouster/cgi-bin/cs140-spring20/lectures.php)  and course syllabus.
- [Video lectures on "Operating Systems"](https://www.youtube.com/playlist?list=PLLDC70psjvq5hIT0kfr1sirNuees0NIbG) by Prof. P.K. Biswas sir, Ph.D(IIT Kharagpur).
- TextBook : [Silberschatz, A. and Galvin, P. B. Operating System Concepts. 8/e. Wiley, 2008.](https://books.google.co.in/books/about/Operating_System_Concepts.html?id=9_-oQgAACAAJ&hl=en)


## PintOS

Pintos is a simple operating system developed at Stanford for the cs140 class as a teaching operating system for 80x86, and has achieved widespread usage in undergraduate OS classes. It is simple and small (compared to Linux). On the other hand, it is realistic enough to help you understand core OS concepts in depth. It supports kernel threads, virtual memory, user programs, and file system. But its original implementations are premature or incomplete. Through the projects, we will be strengthening all of these areas of Pintos to make it complete.

Intro to Pintos - [Video](https://www.youtube.com/playlist?list=PLOZTHmYuABf0rONeeOdvTnFDKF_7DDByy)

The complete Pintos documentation - [HTML](https://web.stanford.edu/~ouster/cgi-bin/cs140-spring20/pintos/pintos.html)

### Dependencies

We'll be using Docker to run Pintos in an x86 emulator running inside a container.
- Install Docker on your machine - [installer link](https://docs.docker.com/engine/install/)

Also, make sure you are using an operating system with the following software:
* git
* Bash
* text editor of your choice

### Getting Started

Fetch the latest Pintos version [pintos.tar.gz](http://www.stanford.edu/class/cs140/projects/pintos/pintos.tar.gz) from stanford and extract it.
```
$ zcat $(path_to_file):/pintos.tar.gz | tar x
```
Or clone the git repo of customized Pintos distribution by Prof. Thierry Sans
```
$ git clone https://github.com/ThierrySans/CSCC69-Pintos
```

Once, you have the source code ready we can test the Pintos docker image.
```
$ docker run --rm --name pintos -w /pintos/src/threads/build thierrysans/pintos pintos --qemu -- -q run alarm-zero
```
It should run Pintos and execute the command alarm-zero before quitting (option -q). The output should look like this:

    qemu-system-i386 -device isa-debug-exit -drive file=/tmp/4VOGYdFrP1.dsk,index=0,media=disk,format=raw 
    -m 4 -net none -nographic -monitor null
    PiLo hda1
    Loading............
    Kernel command line: -q run alarm-zero
    Pintos booting with 3,968 kB RAM...
    367 pages available in kernel pool.
    367 pages available in user pool.
    Calibrating timer...  417,792,000 loops/s.
    Boot complete.
    Executing 'alarm-zero':
    (alarm-zero) begin
    (alarm-zero) PASS
    (alarm-zero) end
    Execution of 'alarm-zero' complete.
    Timer: 24 ticks
    Thread: 0 idle ticks, 25 kernel ticks, 0 user ticks
    Console: 385 characters output
    Keyboard: 0 keys pressed
    Powering off...

The Docker image thierrysans/pintos contains a modified version of the original Pintos source code. However you are not going to modify this code directly in the container, otherwise all of your changes will be lost as soon as the container shuts down.

### Building Pintos

As the next step, build the source code supplied for the first project. First, run the docker container with a mount of your source:

```
$ docker run --rm --name pintos -it -v "$(pwd):/pintos" thierrysans/pintos bash
```

Once in the Docker container, you should build the utils directory (first time only):
```
<Docker>$ cd /pintos/src/utils
<Docker>$ make
```

Now, each of the projects has seperate folder i.e file needed for project 1: Threads are under Pintos/src/thread/. so, while working on the projects build the corresponding directory.
```
<Docker>$ cd /pintos/src/threads
<Docker>$ make
```
### Running Pintos
you can invoke pintos as `$ pintos args` .Each argument is passed to the Pintos kernel for it to act on. The command pintos should be run in the directory where the kernel was built.

```
<Docker>$ cd /pintos/src/threads/build
<Docker>$ pintos -q run alarm-multiple
```
In these arguments, run instructs the kernel to run a test and alarm-multiple is the test to run.

By default, pintos runs the Bochs simulator but you can also run the same command with the QEMU simulator:

```
<Docker>$ pintos --qemu -- -q run alarm-multiple
```
For project 1, the tests will probably run faster in Bochs. For the rest of the projects, they will run much faster in QEMU. make check will select the faster simulator by default, but you can override its choice by specifying SIMULATOR=--bochs or SIMULATOR=--qemu on the make command line.

### Projects
------------

**Project 1: Threads**
- [x] Wait Queue
- [x] Basic Priority Scheduling

**Project 2: User Programs**
- [x] User Program Exeuction
- [x] Process Management
- [x] System Calls

**Project 3: Virtual Memory**
- [ ] Stack Growth
- [ ] Virtual Memory (Paging)
- [ ] Memory-Mapped Files

**Project 4: File Systems**
- [ ] Buffer Cache
- [ ] Extensible Files
- [ ] Filesystem and Subdirectories

### Grading
 Each project has several tests, each of which has a name beginning with tests. To completely test your submission, invoke make check from the project build directory. This will build and run each test and print a "pass" or "fail" message for each one. When a test fails, make check also prints some details of the reason for failure. After running all the tests, make check also prints a summary of the test results.

 Once, the testing is done you can call 
 ```
 <Docker>$ make grade
 ```
This command grade your work and you check it in the file created under build/grade.


> **DISCLAIMER: DO NOT EVER USE the above code for your coursework.