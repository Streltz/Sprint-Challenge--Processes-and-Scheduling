# Sprint Challenge: Processes and Scheduling

1. List all of the main states a process may be in at any point in time on a standard Unix system. Briefly explain what each of these states mean.

On a standard UNIX system, the main states of a process are:

Start: When a process is first created, it occupies the "created" or "new" state. In this state, the process awaits admission to the "ready" state. Admission will be approved or delayed by a long-term, or admission, scheduler.

Ready: A "ready" or "waiting" process has been loaded into main memory and is awaiting execution on a CPU.

Running: A process moves into the running state when it is chosen for execution. A process can run in either the kernel mode or user mode.

Blocked: A process transitions to a blocked state when it cannot carry on without an external change in state or event occurring like user input or access to a critical section which must be executed atomically.

Terminated: A process may be terminated, either from the "running" state by completing its execution or by explicitly being killed. In either of these cases, the process moves to the "terminated" state. The underlying program is no longer executing but the process remains in the process table as a zombie process until its parent process calls the wait system call to read its exit status, at which point the process is removed from the process table, finally ending the process's lifetime. If the parent fails to call wait, this continues to consume the process table entry (concretely the process identifier or PID), and causes a resource leak.

2. What is a Zombie Process? How does it get created? How does it get destroyed?

When a process finishes execution, it will have an exit status to report to its parent process. Because of this last little bit of information, the process will remain in the operating system’s process table as a zombie process, indicating that it is not to be scheduled for further execution, but that it cannot be completely removed (and its process ID cannot be reused) until it has been determined that the exit status is no longer needed.
You can kill the parent process of the zombie and at that point, all of the parent’s children will be adopted by the init process (pid 1), which periodically runs wait() to reap any zombie children.

3. Describe the job of the Scheduler in the OS in general.The process scheduling is the activity of the process manager that handles the removal of the running process from the CPU and the selection of another process on the basis of a particular strategy.

Process scheduling is an essential part of a Multiprogramming operating systems. Such operating systems allow more than one process to be loaded into the executable memory at a time and the loaded process shares the CPU using time multiplexing.

4. Describe the benefits of the MLFQ over a plain Round-Robin scheduler.

MLFQ minimizes response time while algorithms like Round Robin reduce response time but are terrible for turnaround time. 