---
author: "@h3ndrk"
date: "-- vRoHOW 2022"
paging: "%d / %d"
---

```
 ██      ██  ██      ██  ██         ██   🭊🭁🭝🭚
 ██      ██  ██      ██  ██         ██ 🭇🭄█🭠🭗
 ██████████  ██      ██  ██         ██🭊🭁█🭪     🬹🬹🬹🬹🬹
 ██      ██  ██      ██  ██         ███🭝🭒█🭏🬼   █🬺🬹🬹🬹
 ██      ██  🭓████████🭞  🭓████████  ██🭠🭗🭢🭕█🭌🬿  🬹🬹🬹🬻█
```

# HULKs Framework

The new framework that powers our HULKs, written in Rust.

---

# Topics For Today

- **Motivation:** Why? How?
- **Main concepts:** Modules, Cyclers
- **Building blocks:** Filtering, Buffering, Communication
- **Experience:** Modules, Contexts
- **Code Generation**

---

# Motivation

**Why rewrite our framework and robotics code?**

- Decrease technical debt, rethink main concepts
- Knowledge transfer, newbie motivation
- Learn a new language (Rust)
- Fun ;)

---

# Motivation

**Why Rust?**

- Blazingly fast
- Strongly typed
- Safe by default
- Intelligent compiler
- Rich ecosystem

---

# Timeline

- **November 2021:** Start of concept and design
- **January 2022:** Working framework prototype
- **April 2022:** Technical demonstration at GORE 2022
  - Scored 3 goals!
- **July 2022:** Quarter finals reached at RoboCup 2022
  - Scored 17 goals!
- **November 2022:** Working framework prototype for version 2

---

# Concepts: Module

```
                     ┏Module━━━━━┓
             Inputs ─╂→ cycle() ─╂→ Outputs
                     ┃     ↕     ┃
                     ┃   State   ┃
                     ┗━━━━━━━━━━━┛
```

- **Inputs:** From preceeding modules, configuration, hardware, ...
- **Outputs:** For succeeding modules, additional introspection, ...

---

# Concepts: Cycler

```
            ┏Cycler━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
Databases ↔ ┃  Module A  →  Module B  →  Module C  ┃
            ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

- Executes topologically sorted modules
- Each cycle fills a database, shared with other cyclers afterwards
- Time and input data is fixed within a cycle
- First module synchronizes with environment (LoLA, camera, ...)

---

# Concepts: Realtime & Perception Cyclers

```
━━Perception Cycler━━━━━━ ↘
↑             ━━Realtime Cycler━━━━━━━━━━━━━━━━━━━━━ ↘
Environment ↗                                         Actuators
```

- Cyclers are executed in parallel
- **Realtime cyclers** percept environment, control actuators
- **Perception cylers** percept environment, integrate into realtime
- Multiple realtime and perception cyclers may exist

---

# Concepts: Cycler Integration

- Cyclers may run at different speeds (LoLA, cameras, complex NNs)
- Integration interface: Filters (e.g. Kalman, state machine)
- Problem: Synchronized time and asynchronous processing

```
VisionTop:   ┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
VisionBottom: ┣━━━━━━━          ┣━━━━━━━          ┣━━━━━━━
Network:        ┣━━━ ┣━━━┣━━━             ┣━━━ ┣━━━┣━━━┣━━━
Realtime:    ┣━━━━━━━   ┣━━━━━━━━━ ┣━━━       ┣━━━━━     ┣━━━━━━━
```

---

# Concepts: Cycler Integration

```
VisionTop:   ┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
VisionBottom: ┣━━━━━━━          ┣━━━━━━━          ┣━━━━━━━
Network:        ┣━━━ ┣━━━┣━━━             ┣━━━ ┣━━━┣━━━┣━━━
Realtime:    ┣━━━━━━━   ┣━━━━━━━━━ ┣━━━       ┣━━━━━     ┣━━━━━━━
```

- Some filters need data in correct order → need to wait for all data
- Filters would lag but there is already finished data
- **Future Queue** and rollback in filters (persistent/temporary)

---

# Concepts: Database Access Across Cyclers

- Concurrent read/write access from different cyclers
- Readers should not block writers, but get latest data
- **Multiple buffering** between cyclers and communication

```
Slot 0: W━━   W━━ R╴╴╴╴╴╴╴╴     W━━   W━━
Slot 1:    W━━   W━━   W━━   W━━   W━━   W━━    #Slots = 2*#W + #R
Slot 2:             W━━  R╴╴╴╴╴╴╴                      = 2*1  + 2
Slot 3:                   W━━ R╴╴╴╴╴╴╴╴                = 4
```

---

# Communication

```
        ┏Framework━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓  File System
Hardware Interface ↔ Cyclers ↔ Communication ─╂─ Network Clients
        ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛  ...
                             • Databases
                             • Configuration Parameters
                             • Additional Outputs
                             • Data Injection
                             • Remote Procedure Calls, ...
```

---

# Developer Experience: Writing Modules

```rust
struct MyModule { /* module's state */ }
struct NewContext { /* inputs for new() */ }
struct CycleContext { /* inputs for cycle() */ }
struct MainOutputs { /* outputs from cycle() */ }
impl MyModule {
    fn new(context: NewContext) -> Self
    fn cycle(&mut self, context: CycleContext) -> MainOutputs
}
```

---

# Developer Experience: Writing Contexts

```rust
struct CycleContext {
    joint_angle: RequiredInput<Option<Joint>, "joint/angle?">,
    ball_radius: Parameter<f32, "field_dimensions/ball/radius">,
    ball: PerceptionInput<Option<Ball>, "VisionTop", "ball?">,
    hardware_interface: HardwareInterface,
    debug_lines: AdditionalOutput<Vec<Line>, "debug/lines">,
    // ... Input, HistoricInput, PersistantState
}
```

---

# Code Generation

- Cycler constructs contexts, executes module, stores outputs
- v1 needed manual boilerplate code, v2 generates everything
  - Structs, cyclers, runtime are generated from context fields
  - Developers only write modules and hardware interfaces
- Rules on how to write cyclers are now expressed as code
- Zero overhead at runtime, checks at compile-time
- Source code analysis enables many more future use-cases

---

# Conclusion

- 5 cyclers at HULKs: Audio, Control, SplNetwork, VisionTop/-Bottom
- Long running cyclers may be implemented in the future
- Framework is very flexible and robust
- Concepts from last year still hold up
- Only minor changes needed in framework since early prototype
- Version 2 makes the framework more generic, increases separation
- Rust language is a huge win in many ways
- WebSocket interface ensures tooling flexibility
