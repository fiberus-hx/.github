# Project Overview

Fiberus is a project to build a new Haxe compiler target with a fiber-based runtime for multiprocessing. The goal is to create a runtime where all concurrency is handled via fibers/coroutines, with integrated garbage collection. Lockfreeness is paramount.

Fiberus is designed specifically for workloads that can benefit from **lightweight, cooperative concurrency** using fibers (user-mode coroutines) combined with a **work-stealing scheduler** and tight GC integration.

### Target Use Cases

1. **High-concurrency task-parallel applications** - Breaking work into thousands of small, independent jobs (e.g., ray tracing, physics simulation, build pipelines, data processing)
2. **Game engines and real-time systems** - Directly inspired by the Naughty Dog fiber model (GDC 2015 talk)
3. **Server-side applications with massive concurrency** - Web servers, game servers, chat systems
4. **Embarrassingly parallel compute workloads** - Raytracers, video encoders, scientific simulations
5. **Scenarios where preemptive threads are problematic** - Avoiding priority inversion, thread starvation, or complex mutex hierarchies
