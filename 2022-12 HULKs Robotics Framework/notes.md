# HULKs Framework

# Topics For Today

# Motivation

- Why not ...?
  - No knowledge transfer of framework
  - No newbie motivation
  - Most often limited to one programming language or configuration file hell
  - Not as fun as rewriting

# Timeline

# Concepts: Module

# Concepts: Cycler

- Cyclers are emptied before cycles begin
- One cycle works on one set of input data, which cannot change, only the own module-generated data changes
- Databases are structs (blackboards), but not a database server

# Concepts: Realtime & Perception Cyclers

- Realtime has realtime constraints, e.g. actuator output via LoLA
- Perception does not but needs to wait for new percepts

# Concepts: Cycler Integration

- 'predefined, fixed speeds' vs 'undetermined variable speed'

# Concepts: Database Access Across Cyclers

# Communication

- It is not SPL networking
- It is not the hardware interface
- It is a framework component, that has nothing to do with the robotics domain
- Communication bridges the cyclers with the outside world
- No SPL network messaging, but everything else
- WebSocket interface for our tools
- Cyclers share databases with communication
- Configuration parameters, with change notifications
- Additional outputs subscribable by clients
- Data injection between modules
- Remote procedure calls, and more...

# Developer Experience: Writing Modules

# Developer Experience: Writing Contexts

# Code Generation

# Conclusion

- CodeRelease contains framework version 1
