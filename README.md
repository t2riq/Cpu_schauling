# CPU Scheduler Simulator

## Overview

This is a C++ command-line simulator for CPU scheduling algorithms. It supports several scheduling methods (FCFS, SJF, Priority, Round Robin) and allows basic interaction via terminal prompts. Processes can be loaded from a file (`input.txt`) or entered manually.

---

## Supported Scheduling Algorithms

- **First Come First Served (FCFS)**
- **Shortest Job First (SJF)** – Non-preemptive only
- **Priority Scheduling** – Non-preemptive only
- **Round Robin** – Time Quantum = 2

> ⚠️ Preemptive variants are mostly not implemented or marked as “not yet”.

---

## Input Format

The simulator reads processes from a file called `input.txt`. Each line should contain one process in the format:
<burst_time>:<arrival_time>:<priority>

Example:
```
5:0:2
3:1:1
8:2:3
```
Alternatively, you can manually add processes during runtime.

---

## How to Build

Compile with `g++`:

```bash
g++ -o scheduler scheduler.cpp
```
Run the executable:
```
./scheduler
```

---

## Menu Options

When you run the program, you're presented with a main menu:

1. **Scheduling Method** – Pick one of the available algorithms:
   - FCFS (First Come First Served)
   - SJF (Shortest Job First)
   - Priority Scheduling
   - Round Robin

2. **Preemptive Mode** – **Not implemented** (just prints "not yet")

3. **Non-preemptive Mode** – Shortcut to run SJF Non-Preemptive directly

4. **End Program** – Exits the application

For each algorithm, the simulator:
- Loads processes from `input.txt`
- Optionally allows you to add more via the terminal
- Runs the selected scheduling logic
- Prints process order, individual waiting times, and average waiting time

---

## Output

Each algorithm generates output in this format:

- **Process List (Ordered by Scheduling Policy)**
- **Waiting Time per Process**
- **Average Waiting Time**
- For **Round Robin**, the time quantum is fixed at **2 units**, and process output reflects the context switching logic.


---

## Limitations

- ⚠️ **No Preemptive Scheduling** — Options are there, but not functional.
- ❌ **No Gantt Chart** or visual timeline.
- 📎 Uses **raw pointers** and basic linked list logic (no smart pointers or STL).
- 🧨 **No input validation** — malformed input can crash the program.
- 🗃️ Only accepts input from `input.txt` or manual terminal entry.
- 🧹 Needs refactoring for modularity, maintainability, and real scalability.

---

## File Structure

The logic is packed into a single C++ file with the following key parts:

### Main Flow
- `main()` – CLI menu and control logic

### Process Management
- `read_from_File()` – Reads `input.txt`
- `add_new_process()` – Adds more processes via user input
- `createNode()`, `insertBack()`, `insertFront()` – Linked list ops
- `display()` – Shows current process list

### Scheduling Algorithms
- `fcfs()` – First Come First Served
- `ShortestJobFirst_NP()` – Shortest Job First (Non-preemptive)
- `proirity()` – Priority Scheduling (Non-preemptive) *(typo in function name)*
- `round_Robin()` – Round Robin (Quantum = 2)

### Sorting Utilities
- `sortFCFS()`, `sortSJF()`, `sortproirty()` – Linked list sorting by arrival, burst, and priority *(another typo)*

### Timing
- `calwaiting_time()` – Calculates waiting times (non-RR)
- `calwaiting_time_rRobin()` – Specialized logic for Round Robin timing

---

## Final Notes

This is a working, bare-bones CPU scheduler simulation meant for educational/demo purposes. If you're expecting polished design, modular code, or full algorithm coverage—this isn't it.

But it's a solid base.
