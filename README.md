# OPERATING SYSTEMS HW2 : Reader-Writer Problem Solution
## Students:
-- Ebru İl
-- Şeyma Göçmez
## Objective

This project implements a solution to the *Reader-Writer Problem* using semaphores. The goal is to simulate a system where multiple readers and writers access shared resources (tables/files) concurrently, adhering to the following rules:

1. Multiple readers can read a file simultaneously.
2. Writers get exclusive access to a file while writing—no readers or writers can access the file during this time.
3. If a writer is waiting, no new readers may start until the writer finishes its operation.

The *Reader-Writer Problem Solution* project is a simulation designed to demonstrate controlled concurrent access to shared resources (files) using semaphores. It is implemented in C and adheres to key rules for managing readers and writers. Multiple readers can access the same file simultaneously, while writers require exclusive access. If a writer is waiting, no new readers are allowed until the writer finishes. 

Key features include multithreaded execution with `pthread`, efficient use of semaphores for critical section management, and dynamic parsing of operations from an input activity file. Each thread operates as a reader or writer based on the input schedule. Writers append data to files, while readers access shared resources concurrently.

The program reads an activity file detailing operations and logs the execution order and outcomes to `logfile.txt`. It also creates and updates the shared files dynamically during the simulation. The implementation provides synchronization and prevents race conditions and maintains data integrity.

The implementation is useful for understanding concurrency control, semaphore implementation, and real-world scenarios where multiple processes interact with shared resources. Its modular design makes it adaptable to various thread and resource counts, as specified by the user at runtime.
## Features

- *Concurrency*: Ensures safe, simultaneous access to shared resources using semaphores.
- *Simulation*: Reads input from a provided activity file and simulates reader and writer operations.
- *Logging*: Generates a log file (logfile.txt) detailing the sequence of operations and their completion status.

## File Descriptions

1. *databaseSim.c*: The main source code implementing the solution.
2. *logfile.txt*: Example output log showing the execution of reader and writer operations.
3. *Sample Activity File*: Defines the sequence of operations for simulation.

## How to Compile and Run

### Prerequisites
- *GCC Compiler*: Ensure gcc is installed on your system.
- *POSIX Threads*: Required for multithreading support.

### Compilation
Use the following command to compile the program:
bash
gcc databaseSim.c -o databaseSim -lpthread


### Running the Program
To run the program, use the following syntax:
bash
./databaseSim <number_of_threads> <number_of_tables> <activity_file>


*Example*:
bash
./databaseSim 10 2 activity.txt


Here:
- 10: Number of threads (representing readers and writers).
- 2: Number of tables (files) to be created and accessed.
- activity.txt: The input file containing operations.

### Input File Format
The input file (e.g., activity.txt) specifies operations in the following format:

<operation_time> <thread_id> <table_id> <operation_type> <operation_duration> "<written_value>"


*Example*:

5 1 1 read 3 ""
6 2 1 read 2 ""
7 3 1 write 10 "INFORMATION 1"
9 4 1 read 2 ""


### Output
The program generates:
1. *Log file (logfile.txt)*: Logs each activity in order of execution.
2. *Updated table files*: Reflects write operations performed by the threads.

### Example Log Output

Reader 1 started reading tbl1.txt
Reader 2 started reading tbl1.txt
Writer 3 is waiting to write to tbl1.txt
Reader 1 finished reading tbl1.txt
Reader 2 finished reading tbl1.txt
Writer 3 started writing to tbl1.txt
Writer 3 finished writing to tbl1.txt
Reader 4 started reading tbl1.txt


## Implementation Notes

- *Semaphores*: Used to manage reader and writer access to shared resources.
- *Threads*: Each thread simulates a reader or writer.
- *Dynamic Input Handling*: Parses operations from the given activity file.
- *Safety*: Prevents race conditions using semaphore-controlled critical sections.

## Sample Execution
1. Compile the program:
   bash
   gcc databaseSim.c -o databaseSim -lpthread
   
2. Run the program with an activity file:
   bash
   ./databaseSim 10 3 activity.txt
   
3. Check logfile.txt for the operation log.
