## Project Overview

Fiberus is a project to build a new [Haxe](https://haxe.org) compiler target with a fiber-based runtime for multiprocessing. It is designed specifically for workloads that can benefit from **lightweight, cooperative concurrency** using [fibers/coroutines](https://graphitemaster.github.io/fibers/#what-are-fibers) combined with a **work-stealing scheduler** and tight GC integration.

Fiberus exists to let you write clean, idiomatic Haxe code while enjoying cooperative concurrency that feels like a natural part of the language and runtime - without the friction of high-level async/await constructs that always seemed like an afterthought layered on top in other languages and runtimes.

Fiberus 

### Target Use Cases

1. **High-concurrency task-parallel applications** - Breaking work into thousands of small, independent jobs (e.g., ray tracing, physics simulation, build pipelines, data processing)
2. **Game engines and real-time systems** - Inspired by the Naughty Dog fiber model (GDC 2015 talk)
3. **Server-side applications with massive concurrency** - Web servers, game servers, chat systems
4. **Embarrassingly parallel compute workloads** - Raytracers, video encoders, scientific simulations
5. **Scenarios where preemptive threads are problematic** - Avoiding priority inversion, thread starvation, or complex mutex hierarchies

---
### Fiberus + Tracy-Profiler
A simple webserver written in Haxe running fiberus, spawning a fiber for every request.
<img width="1910" height="1071" alt="image" src="https://github.com/user-attachments/assets/d85eda62-0d13-47fe-b59c-39f5ad48d971" />

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
