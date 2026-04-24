# COMPX234 Lab 2 - Readers-Writers Monitor

This project implements the Readers-Writers problem in Python using a monitor-style class with `threading.Lock` and `threading.Condition`.

## Design

The program uses a `ReadersWritersMonitor` class to protect the shared state:

- `active_readers`: number of readers currently reading
- `active_writers`: number of writers currently writing, either 0 or 1
- `waiting_writers`: number of writers waiting to write

The solution uses a writer-preference design. A reader waits if a writer is currently writing or if a writer is already waiting. This prevents writers from being delayed forever by new readers. A writer waits while any reader is reading or another writer is writing.

All checks are done inside `while` loops around `condition.wait()` so that a thread re-checks the monitor state after it wakes up.

## How to run

```bash
python readers_writers.py
```

## Sample output

The exact order may change each time because the program uses multiple threads.

```text
Reader 2 wants to read
Reader 2 starts reading. Active readers = 1
Reader 2 is READING
Reader 3 wants to read
Reader 3 starts reading. Active readers = 2
Reader 3 is READING
Writer 1 wants to write
Writer 1 is waiting to write
Reader 2 stops reading. Active readers = 1
Reader 2 finished reading
Reader 3 stops reading. Active readers = 0
Reader 3 finished reading
Writer 1 starts writing
Writer 1 is WRITING
Writer 1 stops writing
Writer 1 finished writing
Readers-writers simulation completed.
```

## Notes

- Multiple readers may read together when no writer is active or waiting.
- Writers have exclusive access to the shared resource.
- The `Reader` and `Writer` thread classes from the starter code were not changed.

## AI assistance acknowledgement

AI assistance was used to help understand the assignment requirements, plan the monitor design, and review the synchronization logic. The final code should be reviewed and understood by the student before submission and demonstration.
