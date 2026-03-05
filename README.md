**From CPU to the Browser**

I can’t say these things will directly get you a job, but learning this stuff makes you a world-class engineer, no doubt in that tbh hahah  

In the age of ai slop where Claude and friends can generate React components in seconds which is pretty useless and lot of useffect devs complaining about react and ddos themselves by react ,  so here **low-level craft** is the only real differentiator  
(https://x.com/benjitaylor/status/2008251867546218983)

You will **build from scratch**:
- A simplified CPU simulator with cache model
- A from-scratch networking stack
- A complete (subset) browser rendering engine (HTML/CSS/layout/paint)
- A bytecode JavaScript engine with GC and event loop
- A high-performance Virtual DOM + Fiber-style reconciler
- A React/Next.js-inspired framework with hooks, concurrent mode, and SSR
- An end-to-end optimized web application

**Who this course is for**
- Senior frontend engineers who want to become systems-level frontend gods
- Backend/systems engineers moving into high-performance UI
- Anyone tired of “it’s slow because React” and ready to understand *why* at the instruction level

**Prerequisites** (must-have — this is intense)
- Strong C++ **or** Rust (you’ll implement most of the heavy parts in one of these)
- Solid computer architecture (pipelines, caches, virtual memory)
- Operating systems basics (processes, syscalls, virtual memory, scheduling)
- Deep data structures & algorithms knowledge
- Experience with low-level debugging (GDB, Valgrind, perf, strace, etc.)

**Course duration**  
12 focused weeks (realistically 4–6 months part-time with life)

### Detailed Weekly Breakdown

**Week 0.5 – CPU & Memory Architecture Fundamentals**  
Build intuition for how hardware actually executes code.

- CPU basics: fetch, decode, execute, writeback (sometimes memory stage)
- Registers & instructions: basic register usage, simple instruction scheduling, ILP basics
- Branching & pipelines: branch prediction (static/dynamic), mispredict cost, pipeline bubbles/stails
- Cache basics: L1i/L1d, L2, L3; cache lines, associativity, write-back vs write-through
- Memory: virtual memory (paging, TLB, page faults, huge pages), stack vs heap
- Process / low-level execution: text, rodata, data, bss, stack, heap layout
- System calls overview
- Pointers and simple memory alignment: alignment, padding, strict aliasing, unaligned access penalties

**Project**  
Implement a toy RV32I CPU simulator + simple 2-level cache in Rust/C++.  
Run small assembly loops and measure branch mispredict vs L1/L2 miss penalties.

**Week 1 – Networking from First Principles / from Scratch**

- Socket programming: TCP & UDP sockets, bind/listen/accept, connect/send/recv
- TCP basics: three-way handshake, sequence/ack, sliding window, flow control, congestion avoidance basics
- HTTP basics: request line, headers, body, chunked encoding, keep-alive, pipelining
- HTTP/2 intro: multiplexing, header compression
- TLS basics: handshake overview (TLS 1.3), certificate check (no deep crypto math)
- WebSocket basics: HTTP upgrade handshake, framing, masking, ping/pong
- Network debugging: tcpdump / Wireshark basics & filters, tc/netem to simulate latency and packet loss

**Project**  
Build a minimal persistent HTTP/1.1 client + server with chunked support.  
Simulate high-latency / packet-loss networks and observe behavior.

**Weeks 2–3 – Browser Engine Implementation / Rendering Engine**

**HTML parsing**
- Tokenization state machine (13 states, 67 transitions / WHATWG subset)
- Tree construction algorithm
- Error recovery and quirks mode
- Parser-blocking scripts and async/defer, script insertion & execution timing

**CSS engine**
- Tokenizer and parser (grammar implementation) for selectors, properties, at-rules
- Selector matching with specificity calculation
- Cascade resolution algorithm (including layers)
- Style computation and inheritance
- Media query evaluation

**Layout engine**
- Box model calculation, margin collapse, block/formatting contexts
- Normal flow, floats & clearing, positioning schemes
- Flexbox algorithm: main/cross axis, flex basis, grow, shrink (full)
- Grid algorithm: track sizing, placement, spanning (full)
- Line breaking and text shaping / inline layout & text wrapping

**Paint and composite**
- Layer tree construction, paint order, stacking contexts, layer promotion
- Paint recording and display lists / paint chunk recording
- Rasterization strategies (basic software scanline rasterizer + GPU texture hints)
- GPU compositing and texture management

**Project**  
Build a browser engine in C++ or Rust that renders real Wikipedia pages (text, images, basic styling, simple CSS animations).  
Handle fonts, images. Measure and log every phase: parse → style → layout → paint → composite.

**Weeks 4–5 – JavaScript Engine**

**Parsing and AST**
- Lexical analysis and tokenization / Lexer
- Hand-written recursive descent parser
- AST construction and validation
- Scope analysis, hoisting, TDZ, symbol resolution

**Interpreter implementation**
- Bytecode design and instruction set
- Stack-based VM execution, opcode table, dispatch
- Closure implementation with environment chains
- Prototype chain traversal
- Property lookup optimization (hidden classes / inline caches)

**Memory management**
- Mark-and-sweep garbage collection (stop-the-world)
- Generational collection (young/old generations, semi-space nursery + mark-compact old gen)
- Incremental and concurrent GC basics
- WeakMap and WeakSet implementation
- Memory profiling and leak detection

**Event loop mechanics**
- Microtask queue (Promise.then)
- Macrotask queue (setTimeout, I/O)
- Animation frame callbacks (requestAnimationFrame)
- Idle callbacks (requestIdleCallback) and scheduling
- Task prioritization

**Optional / Stretch**
- JIT compilation: inline caching and polymorphic inline caching, type feedback, speculative optimization, deoptimization and bailout, register allocation

**Project**  
JS engine executing real programs. Implement closures, prototypes, async/await, Promises, event loop.  
Integrate with your DOM for interactive apps. Profile GC pauses and optimize hot paths.

**Week 6 – Virtual DOM & Reconciliation**

- Diffing algorithms: naive O(n³) → keyed O(n) heuristics
- Key-based reconciliation
- Heuristics: component type, element type, lists
- Fiber architecture preparation: unit of work, work-in-progress tree, yielding
- Batching and scheduling: requestAnimationFrame-based updates, double buffering, priority queues, time slicing for interruptibility
- Repaint/reflow optimization: layout thrashing detection, read/write batching (FastDOM), CSS containment, layer creation, composite-only animations

**Project**  
Virtual DOM library with optimized reconciliation. Stress test with 10,000+ dynamic nodes. Profile layout/paint timings.

**Week 7 – React/Next.js Internals**

**Fiber reconciler**
- Work loop and unit of work
- Reconciliation phases: render and commit
- Effect list construction
- Priority levels and lane model

**Hooks implementation**
- Hooks queue and cursor
- useEffect cleanup and dependency checking
- useRef mutable container
- useCallback/useMemo memoization
- Custom hook composition

**Concurrent features**
- Time slicing and work interruption
- Suspense and lazy loading
- useTransition and useDeferredValue
- Automatic batching

**Server-side rendering**
- renderToString vs renderToPipeableStream
- Progressive hydration and selective hydration
- Double pass problem and solutions
- Edge rendering vs Node rendering

**Next.js architecture**
- File-based routing implementation
- SSG: getStaticProps build-time execution
- ISR: revalidation and stale-while-revalidate
- API routes and middleware
- Module bundling and code splitting

**Project**  
Clone React's core reconciler with Fiber and hooks. Build SSR framework with streaming and hydration. Implement file-based routing.

**Week 8 – Performance Engineering**

**Profiling tools**
- Chrome DevTools: Performance tab deep dive
- React DevTools Profiler
- Lighthouse metrics: FCP, LCP, TTI, CLS, FID (now INP)
- Custom performance marks and measures
- Heap snapshots and allocation timelines

**Optimization techniques**
- Component memoization strategies
- Virtualized lists and windowing
- Image optimization: formats (AVIF/WebP), lazy loading, responsive images (srcset)
- Font optimization: subsetting, preloading, display strategies
- Bundle analysis and tree shaking
- Code splitting strategies: route-based, component-based

**Critical rendering path**
- Eliminate render-blocking resources
- Minimize critical CSS
- Defer non-critical JavaScript
- Preload/prefetch/preconnect strategies

**Project**  
Optimize real-world app from 3s to <1s LCP. Achieve stable 60fps animations with heavy DOM updates. Document every optimization with before/after metrics.

**Week 9 – Engine Modification & Debugging**

**JavaScript engine hacking**
- Build V8 from source with custom patches
- Add custom bytecode instructions
- Instrument GC for detailed metrics
- Profile JIT compilation decisions

**Browser engine debugging**
- Build Chromium/WebKit/Servo from source
- Add custom tracing to layout engine
- Modify rendering pipeline for instrumentation
- Debug compositor thread interactions

**WebAssembly integration**
- Compile C/C++/Rust to WASM
- Linear memory management
- JS ↔ WASM interop optimization
- SIMD and threads basics

**Project**  
Add custom profiling to browser engine. Build WASM module for computationally intensive task (image processing, physics simulation). Optimize JS/WASM boundary.

**Week 10 – Hardware Simulation & Constraints / Extreme Constraints**

- Embedded systems: run minimal browser on microcontroller simulation
- Memory-constrained rendering (64 KB RAM)
- CPU-constrained JavaScript (10–20 MHz effective)
- Display optimization for small screens
- Stress testing: memory pressure, CPU throttling, network constraint (2G, 3G, high loss, long RTT), GPU bottleneck analysis

**Project**  
Port mini-browser + UI framework to constrained env. Document brutal but necessary optimizations.

**Weeks 11–12 – Capstone Project**  
Build a complete system:

1. Custom browser engine with HTML/CSS/JS support (subset)
2. React-like framework with Fiber and concurrent features
3. SSR framework with streaming and progressive/selective hydration
4. Production-optimized Next.js-style application (file-based routing, SSG/ISR, API routes)
5. Full performance profiling suite
6. WebAssembly acceleration for critical paths
7. Hardware constraint testing and optimization

**Requirements / Success criteria**
- Render complex UIs at stable 60 fps
- Handle 10,000+ concurrent DOM updates smoothly
- Sub-second initial page load
- Progressive enhancement and graceful degradation
- Comprehensive error handling and edge cases
- Full performance documentation: diagrams, architecture, traces, metrics


**What you’ll walk away with**
- deep intuition for CPU → memory → execution → network → rendering → JS → React
- ability to debug and fix performance at any layer of the stack
-  you can read V8/Chromium source, optimize production apps, and contribute to engine/framework codebases

This is one of the most rewarding (and hardest :)) learning paths you can take in frontend/systems engineering :)

