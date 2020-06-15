# **Processes and Threads**

- Using [Docs to Markdown](https://gsuite.google.com/marketplace/app/docs_to_markdown/700168918607) to convert my [Processes and Threads](https://docs.google.com/document/d/11cKERzGs-TxPfTIQHekgcrWdcK_2drzd8Op_knRVtKM/edit?usp=sharing) from google doc text to markdown 


# Process



*   **What is it?**
    *   Execution of a program (A running program) by the operating system.
    *   One process can be made up of multiple threads.
*   **Why we need a process?**
    *   Because a program itself is only multiple lines of code so it couldn’t do anything if we don’t execute it.


# Multiple Process



*   Normally, everyone needs to run more than one program at the same time (multiple processes) for example, Running music player, discord while doing work in Microsoft Word.
*   **Question:** But the computer only has a few physical CPU, so how did it run multiple processes at once?
*   **Answer:** By running one process and switching to another process, the OS can create an illusion that there are many CPUs running for each process.


# Virtualizing the CPU



*   Running one process and switching to another to make the user feel like there are multiple CPUs running but in reality, there are only a few. It’s possible because** a time-sharing OS **which its essential goal is to minimize response time.
*   **Time-sharing OS**
    *   Time-sharing is a technique that enables many users to share computer resources simultaneously by allocating computer resources in time slots to each program.


# Machine State



*   The machine state uses to identify which process can read or update when it’s running.
*   At any given time, what part of the computer need for the execution of this process.
*   Each process contains a machine state of that process which can divide into three-part:
    *   State of memory: Static data, stack, heap, and code
    *   State of registers: PC, stack pointer, and frame pointer
    *   Input/Output information: list of open programs etc.


# Process API



*   We don’t directly work with a process. We usually work with the process through the API that the operating system provides for us which allowing us to work with the process without knowing the implementation detail.
*   **Create**
    *   Use to create new processes, for example, executing a command in the shell or double-click on an application icon.
*   **Destroy**
    *   Destroying processes forcefully.
*   **Wait**
    *   Waiting for a process to stop running.
*   **Miscellaneous Control**
    *   Other than destroying or waiting for a process there are some other controls option that are possible.
        *   **Suspend** (Stop a process from running for a while)
        *   **Resume** (Continue the process)
*   **Status**
    *   Get some information about the process, for example how long this process has run or what state it is in.


# From Program to Process



*   As everyone knows a standalone program is just multiple lines of code, so we need a way to execute it to make a program become a process.
    *   First: Loading the code and static data into memory
    *   Second: Creating, initializing a stack, and allocating some memory in the heap.
    *   Third: Doing other work as related to Input/Output setup.
    *   Fourth: Start program from the entry point, normally** main() **after that the OS transfers control of the CPU to that process, hence the program begins it execution.


# Process State



*   Normally consist of five states.
    *   **Created**
        *   State for a process that just got created and awaits for OS to change its state to ready.
    *   **Ready**
        *   State for a process that is ready to run but the OS doesn’t run it at this moment. This state can occur at any point of time if the process didn’t terminate yet 
    *   **Running**
        *   State for a process that got chosen by OS and now running on a processor, executing instructions (Line of code).
    *   **Blocked**
        *   State for a process that needs to perform some operation that requires other processes or events to occur or finish first.
    *   **Terminated**
        *   State for a process that got terminated, either form running state when OS finishes its execution or the process got terminated.

<table>
  <tr>
   <td colspan="2" >

<h2>Program vs Process</h2>

Key difference.
   </td>
  </tr>
  <tr>
   <td><strong>Program</strong>
   </td>
   <td><strong>Process</strong>
   </td>
  </tr>
  <tr>
   <td>Program is just multiple lines of code
   </td>
   <td>Program in execution.
   </td>
  </tr>
  <tr>
   <td>Store on disk and doesn’t require any other resources
   </td>
   <td>Holds resources such as CPU, memory address, disk, I/O, etc.
   </td>
  </tr>
</table>



## Threads (Lightweight process)



*   Threads is a flow of execution within a process
*   Threads under a single process have the same address space, they share memory machine states of that process.
*   Multithread is an execution of multiple threads for either the same or different processes.


## Thread Machine State



*   Shared between thread from the same process.
*   **Private state**
    *   State for each thread (Different from each other even if they came from the same process).
        *   Registers including PC and stack pointer
        *   Execution stack of each thread
    *   Contained under **TCB (Thread Control Block)**
        *   A data structure in the operating system kernel which contains thread-specific needed for managing the thread.
            *   Example of information contained in **TCB (Thread Control Block)**:
                *   **Thread Identifier**
                    *   Unique id for each thread.
                *   **Stack pointer**
                    *   Points to thread’s stack during the process.
                *   **Program counter**
                    *   Points to current code line in the program for this thread
                *   **State of thread**
                    *   Running, ready, waiting, start, done.
                *   **Thread’s register values**
                    *   Values of a register that this thread associates with.
                *   **Pointer to the Process control block (PCB)**
                    *   Pointer to process that associates with this thread.


## Threads vs Processes


<table>
  <tr>
   <td colspan="2" >
<h2>Threads vs Processes</h2>

Key difference.
   </td>
  </tr>
  <tr>
   <td><strong>Threads</strong>
   </td>
   <td><strong>Processes</strong>
   </td>
  </tr>
  <tr>
   <td>Segments of a process
   </td>
   <td>Program in execution
   </td>
  </tr>
  <tr>
   <td>Lightweight
   </td>
   <td>Not lightweight
   </td>
  </tr>
  <tr>
   <td>Takes less time to terminate and create than a process.
   </td>
   <td>Takes more time to terminate and create than a thread.
   </td>
  </tr>
  <tr>
   <td>Communication time between threads is faster than processes
   </td>
   <td>Communication time between processes is slower than threads.
   </td>
  </tr>
  <tr>
   <td>A different process is tread separately by OS
   </td>
   <td>All level peer threads are treated as a single task by OS
   </td>
  </tr>
  <tr>
   <td>Share memory
   </td>
   <td>Mostly isolated
   </td>
  </tr>
  <tr>
   <td>Share data with each other thread
   </td>
   <td>Not share data
   </td>
  </tr>
</table>



## Threads operation



*   **thread_create(thread, function, args)**
    *   Create a new thread to run the given func.
*   **thread_yield()**
    *   Yield thread voluntarily (For another to use the resource etc.).
*   **thread_join(thread)**
    *   Wait for child forked thread to finish, then return. 
*   **thread_exit**
    *   Quit thread.


## Reference

	[Process vs Thread: What's the difference?](https://www.guru99.com/difference-between-process-and-thread.html#:~:text=Process%20means%20a%20program%20is%20in%20execution%2C%20whereas%20thread,a%20segment%20of%20a%20process.&text=A%20Process%20is%20mostly%20isolated,share%20data%20with%20each%20other.). guru99. Retrieved 9 June 2020.

	[Process (computing)](https://en.wikipedia.org/wiki/Process_(computing)). Wikipedia. Retrieved 12 June 2020.

[Process state](https://en.wikipedia.org/wiki/Process_state). Wikipedia. Retrieved 13 June 2020.

[Types of Operating System](https://www.tutorialspoint.com/operating_system/os_types.htm#:~:text=Time%2Dsharing%20is%20a%20technique,is%20termed%20as%20time%2Dsharing.). Tutorialspoint. Retrieved 13 June 2020.

[Difference Between Program and Process](https://techdifferences.com/difference-between-program-and-process.html#:~:text=A%20program%20and%20a%20process,to%20be%20a%20passive%20one.). TechDifferences. Retrieved 13 June 2020.

[Thread control block](https://en.wikipedia.org/wiki/Thread_control_block#:~:text=Thread%20Control%20Block%20(TCB)%20is,thread%20in%20an%20operating%20system.%22). Wikipedia. Retrieved 13 June 2020.

“Threads" by Paruj Ratanaworabhan.

“The Process” by Paruj Ratanaworabhan.
