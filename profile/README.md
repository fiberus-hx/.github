## Project Overview

Fiberus is an experimental project to build a new **native** [Haxe](https://haxe.org) compiler target with a fiber-based runtime for multiprocessing. It is designed specifically for workloads that can benefit from **native, lightweight, cooperative concurrency** using [fibers/coroutines](https://graphitemaster.github.io/fibers/#what-are-fibers) combined with a **work-stealing scheduler** and tight GC integration.

Fiberus exists to let you write clean, idiomatic [Haxe code](https://haxe.org/documentation/introduction/language-introduction.html) while enjoying cooperative concurrency that feels like a natural part of the language and runtime - without the friction of high-level async/await constructs that always seemed like an afterthought layered on top in other languages and runtimes.

### Target Use Cases

1. **High-concurrency task-parallel applications** - Breaking work into thousands of small, independent jobs (e.g., ray tracing, physics simulation, build pipelines, data processing)
2. **Game engines and real-time systems** - Inspired by the [Naughty Dog fiber model (GDC 2015 talk)](https://gdcvault.com/play/1022186/Parallelizing-the-Naughty-Dog-Engine)
3. **Server-side applications with massive concurrency** - Web servers, game servers, chat systems
4. **Embarrassingly parallel compute workloads** - Raytracers, video encoders, scientific simulations
5. **Scenarios where preemptive threads are problematic** - Avoiding priority inversion, thread starvation, or complex mutex hierarchies


### Contact
[Get in touch on Discord](https://discord.com/channels/162395145352904705/1475242607910195270)

---

## Project Status

- **Current Maturity:** ~97-99% Haxe standard library parity with hxcpp
- **Haxe Unit Tests:** 11,693 assertions — 0 failures (same test suite as hxcpp, HashLink, JVM)
- **Fiberus Native Tests:** ~1,669 assertions — all passing (2 pre-existing WeakMap failures)
- **Combined Test Coverage:** ~13,362 assertions
- **Platform:** Linux x86_64 only

### What Works

**Core Language:**
- Fiber spawn/yield/context switching (hand-written x86_64 assembly)
- Work-stealing multi-threaded scheduler (Chase-Lev deque)
- MaPLe-inspired Hierarchical Heap GC (per-fiber heaps, depth-based write barriers, Cheney copying collector)
- Closures with capture
- Exception handling with typed catch (Int, Float, Bool, String, Object instanceof, Dynamic catch-all)
- Pattern matching, enums with parameters, generic classes

**Standard Library:**
- Collections: IntMap, StringMap, Int64Map, ObjectMap (full iteration support)
- Reflect, Type (full runtime reflection and type introspection — all methods implemented)
- EReg (pcre2-backed regular expressions)
- haxe.Json (simdjson parser, custom printer)
- haxe.zip.Compress/Uncompress (miniz)
- haxe.crypto: Md5, Sha1, Sha256, Base64, Crc32, Adler32
- haxe.Utf8 (simdutf-backed)
- haxe.Resource (embedded binary resources)
- haxe.Serializer / haxe.Unserializer (full serialization/deserialization)
- haxe.Http (HTTP/HTTPS client)
- Xml (full DOM parser/builder)
- StringBuf (C-backed growable buffer)
- Std.parseInt, Std.parseFloat, Std.isOfType
- haxe.Exception (native exception integration)

**I/O and Networking:**
- io_uring async I/O (fibers yield instead of blocking threads)
- File/Socket I/O via io_uring
- sys.ssl.Socket, Key, Certificate, Digest (mbedTLS, io_uring-integrated)
- sys.io.Process (subprocess.h, pidfd + io_uring for fiber-friendly waiting)
- sys.net.Socket, UdpSocket

**Threading and Concurrency:**
- sys.thread.Tls (real slot-based thread-local storage)
- sys.thread.Thread.create maps to Fiber.spawn
- haxe.atomic: AtomicInt, AtomicBool, AtomicObject (GCC builtins, SEQ_CST, value-based CAS)
- Mutex/Lock/Condition/Semaphore/Deque stubs (throw directing to fiber API)



**Native Types:**
- Int8-Int64, UInt8-UInt64, Float32/64, SizeT, Char

**Fiberus Repositories**
- [Haxe Compiler](https://github.com/fiberus-hx/haxe/tree/fiberus) - Compiler Fork containing the fiberus codegenerator
- [Fiberus Runtime](https://github.com/fiberus-hx/fiberus) - Fiberus C-Runtime
- [Filewatch Fiberus Externs](https://github.com/fiberus-hx/fib_filewatch) - Filewatching externs
- [Meow Fiberus Externs](https://github.com/fiberus-hx/fib_meow) - Meow Hashing
- [RGFW Fiberus Externs](https://github.com/fiberus-hx/fib_rgfw) - Riley's General Framework for Windowing externs
- [Yoga Fiberus Externs](https://github.com/fiberus-hx/fib_yoga) - Meta's Yoga Layout externs
- [Sqlite3 Fiberus Externs](https://github.com/fiberus-hx/fib_sqlite3) - SQLite3 database library + Custom non-blocking SQLite VFS for the Fiberus runtime.
- [Warp10 HTTP Framework](https://github.com/fiberus-hx/warp10) - High-performance HTTP framework designed for fiberus

---

### Fiberus in action
A [simple webserver written in Haxe running fiberus](https://github.com/fiberus-hx/fiberus/blob/main/benchs/http/SimpleWebServer.hx), spawning a fiber for every request ([Loadtest Results](https://gist.github.com/dazKind/2483162f05da0194fceaac6d73537bd7)).

Our MaPLe-inspired Hierarchical Heap GC (per-fiber heaps, depth-based write barriers, Cheney copying collector) in action:

<img width="1039" height="590" alt="image" src="https://github.com/user-attachments/assets/f3af30f1-e45b-4679-a090-2d9c0ad9552d" />




