# Deadlock-Free Resource Allocation Demo

A single-page, browser-based visualization of safe (sequential) resource allocation among multiple processors, inspired by concepts from the **Banker's Algorithm** and deadlock-avoidance theory in Operating Systems.

## Overview

This demo lets you define a pool of available system resources and a set of processors, each with its own resource needs. It validates every request against availability *before* allocation and then animates a safe execution sequence in which each processor acquires and releases its resources one at a time, guaranteeing no deadlock occurs.

## Files

- `index.html` — Self-contained HTML/CSS/JavaScript app (no external dependencies, no build step).

## How to Use

1. Open `index.html` in any modern web browser.
2. **Enter available resources** as a comma-separated list (e.g. `3,4`), representing the quantity of each resource type in the system.
3. **Add processors** one at a time by entering their resource needs (e.g. `3,2`) and clicking **Add Processor**. Each processor's need vector must:
   - Match the number of resource types defined for the system.
   - Not exceed the currently available quantity for any resource type.
   Invalid input is flagged inline with a warning message.
4. Once at least one processor has been added, click **Run Safe Allocation** to start the simulation.
5. Watch the animated panel and log:
   - Each processor "using" its allocated resources (highlighted green).
   - Resources being released back to the pool (highlighted blue).
   - A running log of available resources before/after each step.
6. When all processors have completed, a summary table lists each processor, its resource usage, and final status (`Executed`).
7. Click **Reset** to clear all state and start over.

## How It Works

- **Validation** (`addProcessor`): Before a processor is added, the app checks that its request vector is the correct length and that no individual resource request exceeds what's currently marked available, preventing unsafe/oversized requests up front.
- **Simulation** (`runSimulation` / `executeNext`): Processors are executed **sequentially**, not concurrently. Each processor:
  1. "Acquires" its resources (subtracted from `available`).
  2. Holds them briefly (simulated via `setTimeout`).
  3. Releases them back (added back to `available`).
  
  Because only one processor holds resources at a time and every processor eventually releases everything it holds, **no circular wait or hold-and-wait condition can arise** — the classic prerequisites for deadlock are structurally avoided.
- **Visualization** (`visualizeState`): Renders a processor/resource box layout and toggles CSS classes (`using`, `released`) to animate state transitions.
- **Result Table** (`buildTable`): Summarizes each processor's resource vector and final execution status after the simulation completes.

## Key Concepts Illustrated

| Concept | How it's shown |
|---|---|
| Resource request validation | Warnings when requests exceed availability or mismatch resource types |
| Safe allocation sequence | Processors run one-by-one, never holding resources simultaneously |
| Hold-and-wait avoidance | Each processor releases resources immediately after use |
| State visualization | Color-coded animation of acquiring/releasing resources |

## Limitations / Notes

- This is a **teaching visualization**, not a full implementation of the Banker's Algorithm (it does not compute a safe sequence among *concurrently competing* processors with maximum-claim matrices; it simply runs each added processor safely in sequence).
- All processors are guaranteed to "succeed" since the app never allows an oversized request to be added in the first place — so this demo shows *deadlock avoidance by design* rather than *deadlock detection* after the fact.
- No persistence: refreshing the page clears all data.

## Customization Ideas

- Extend to true Banker's Algorithm: add per-processor **maximum claim** vectors and compute a safe sequence via the standard safety algorithm.
- Allow concurrent (interleaved) processor execution to demonstrate actual deadlock scenarios for contrast.
- Add multiple resource instances with allocation matrices (Allocation, Max, Need) for a full OS-course-style demo.
