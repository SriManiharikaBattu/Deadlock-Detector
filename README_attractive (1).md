# 🔒 Deadlock-Free Resource Allocation Demo

![Status](https://img.shields.io/badge/status-active-brightgreen)
![Type](https://img.shields.io/badge/type-visualization-blue)
![Tech](https://img.shields.io/badge/built%20with-HTML%20%7C%20CSS%20%7C%20JS-orange)
![No Dependencies](https://img.shields.io/badge/dependencies-none-lightgrey)

> An interactive, browser-based visualization of **safe resource allocation** among competing processors — inspired by the **Banker's Algorithm** and deadlock-avoidance principles from Operating Systems.

---

## ✨ Overview

This demo lets you define a pool of **available system resources** and add **processors**, each with its own resource needs. Every request is validated *before* allocation, and the app then animates a safe execution sequence — showing each processor acquire and release its resources one at a time, so **deadlock never occurs**.

---

## 📂 Files

| File | Description |
|------|-------------|
| `index.html` | Self-contained HTML/CSS/JavaScript app — no build step, no dependencies |

---

## 🚀 How to Use

1. **Open** `index.html` in any modern browser.
2. **Enter available resources** as comma-separated values (e.g. `3,4`) — the total quantity of each resource type in the system.
3. **Add processors** one at a time by entering their resource needs (e.g. `3,2`) and clicking **➕ Add Processor**.
   - ⚠️ Need vector length must match the number of resource types.
   - ⚠️ No single request may exceed the currently available amount.
4. Click **▶️ Run Safe Allocation** once you've added at least one processor.
5. Watch the **animated visualization** and live log:
   - 🟢 Green = processor actively using resources
   - 🔵 Blue = resources just released
6. Review the **summary table** once every processor finishes.
7. Click **🔄 Reset** to clear everything and start fresh.

---

## ⚙️ How It Works

| Stage | Function | What Happens |
|-------|----------|---------------|
| ✅ Validation | `addProcessor()` | Checks request length & size against availability before adding |
| 🔁 Simulation | `runSimulation()` / `executeNext()` | Processors run **sequentially** — acquire → hold → release |
| 🎨 Visualization | `visualizeState()` | Animates processor/resource boxes with color-coded states |
| 📊 Summary | `buildTable()` | Displays a final table of each processor's usage & status |

Because only **one processor holds resources at a time**, and every processor **always releases what it holds**, the classic deadlock conditions — *hold-and-wait* and *circular wait* — are structurally impossible here.

---

## 🧠 Key Concepts Illustrated

- ✅ Resource request validation
- 🔒 Safe, sequential allocation
- ♻️ Hold-and-wait avoidance
- 🎞️ Real-time state animation

---

## ⚠️ Limitations

- This is a **teaching visualization**, not a full Banker's Algorithm implementation (no concurrent competing processors or max-claim safety matrix).
- Since oversized requests are rejected at input time, every added processor is guaranteed to succeed — this demonstrates **deadlock avoidance by design**, not detection after the fact.
- No data persistence — refreshing the page resets everything.

---

## 💡 Ideas for Extension

- [ ] Implement full **Banker's Algorithm** with Max, Allocation & Need matrices
- [ ] Allow **concurrent/interleaved** execution to show real deadlock scenarios
- [ ] Support **multiple instances per resource type**
- [ ] Add a **Safety Sequence** display for OS coursework demos

---

<p align="center">Made with 💙 for learning Operating Systems concepts</p>
