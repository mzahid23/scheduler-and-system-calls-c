# xv6 Priority Scheduler and System Calls

A modified version of the xv6 operating system implementing a custom priority-based CPU scheduler, kernel-level system calls, process priority management, and a userspace `ps` utility.

This project focused on operating systems concepts including process scheduling, kernel development, process control blocks, starvation prevention, and user/kernel communication.

---

## Features

- Custom priority scheduler implementation
- Dynamic process priority management
- Aging mechanism to reduce starvation
- Kernel-level system calls
- Userspace `ps` utility
- Process statistics tracking
- Effective vs. real process priorities
- CPU time slice management

---

## Technologies Used

- C
- xv6 Operating System
- QEMU
- Linux
- Git/GitHub

---

## System Calls Implemented

### `setPriority(int pid, int priority)`

Sets the real priority of a process.

- Priority range: `-20` to `20`
- Higher priority processes receive more CPU time
- Invalid priorities return an error

---

### `setEffectivePriority(int pid, int priority)`

Updates the effective runtime priority of a process used by the scheduler.

This allowed dynamic scheduling behavior and starvation prevention.

---

### `getpinfo(struct pstat *)`

Transfers process information from kernel space to userspace.

Tracked information includes:
- process name
- process state
- PID
- real priority
- effective priority
- CPU ticks accumulated

---

## Priority Scheduler

The default xv6 round-robin scheduler was replaced with a priority-based scheduler.

### Scheduler Behavior

- Processes with higher priorities are selected first
- Tied priorities rotate fairly between runnable processes
- Processes exceeding their time quantum yield the CPU
- Effective priorities are dynamically adjusted

---

## Aging Mechanism

To prevent starvation:

- Processes waiting too long without CPU access receive a priority boost
- After 10 scheduler ticks without running:
  - effective priority increases by 1
- Once scheduled:
  - effective priority resets to real priority

This improved fairness while still prioritizing important processes.

---

## Userspace `ps` Utility

A custom `ps` command was implemented to display runtime process information.

Example output:

```text
NAME    PID     STATUS      PRIORITY
init    1       SLEEPING    1
sh      2       SLEEPING    1
test    4       SLEEPING    -10
ps      6       RUNNING     20
```

---

## Concepts Learned

This project strengthened understanding of:

- CPU scheduling algorithms
- Kernel development
- Process control blocks (PCB)
- Starvation and aging
- System calls
- User/kernel memory transfer
- Synchronization and locking
- Operating system internals

---

## Building the Kernel

```bash
make
```

---

## Running xv6

```bash
make qemu
```

---

## Exiting xv6

```bash
ctrl-a x
```

---

## Future Improvements

- Multi-level feedback queue scheduler
- Priority inheritance
- Scheduler benchmarking tools
- Real-time scheduling support
- Improved process monitoring utilities

---

## Author

Muhammad Zahid
