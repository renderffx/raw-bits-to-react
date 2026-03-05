# From CPU to the Browser

We live in the era of AI slop.  
Tools like Claude, Cursor, and friends generate React components faster than you can read them — but 90% of it is bloated, unoptimized garbage full of unnecessary useEffect chains that turn smooth UIs into slideshows imo many websites today wont run at 60 fps 

that show how engineers serious about engineering this is what makes you different from the , and this course helps engineers learn real engineering learn keep screaming “React is slow” while they accidentally DDoS their own event loop with re-renders and state thrashing.

The only real moat left? **Craft**.

> “In the age of slop, craft is the differentiator.”  
> — Benji Taylor  
> https://x.com/benjitaylor/status/2008251867546218983

I can’t say these things will directly get you a job, but learning this stuff makes you a world-class engineer, no doubt in that tbh hahah.

**CPU instruction fetch → cache misses → virtual memory page faults → TCP packets → HTTP parsing → HTML/CSS tokenization → layout thrashing → JS bytecode execution → GC pauses → Fiber reconciliation → paint chunks → GPU compositing.**

When you finish, you won’t whine about frameworks and not participate in framework wars

You’ll know precisely why your LCP is 4 seconds, which inline cache is polymorphic and exploding, why your 10k-item list janks on scroll, or how a single compositor layer promotion saves 15 ms per frame you become more then what i describing lol

---

### What You Build From Scratch

- Toy RV32I CPU simulator + realistic 2-level cache (feel branch mispredicts & L1/L2 thrashing)
- Clean networking layer: raw TCP sockets → persistent HTTP/1.1 with chunked encoding → TLS handshake intuition → WebSocket framing
- Mini browser rendering engine: full HTML tokenizer + tree construction → CSS cascade/specificity/layers → complete Flexbox + Grid layout → paint order + basic software rasterizer → layer promotion & compositing
- Bytecode JavaScript engine: hand-written parser → AST → stack-based VM → closures/prototypes/inline caches → generational garbage collector → complete event loop (microtasks, macrotasks, rAF, rIC)
- High-performance Virtual DOM: naive diff → keyed O(n) heuristics → Fiber-style architecture (units of work, yielding, time-slicing)
- Mini React clone: Fiber reconciler + full hooks system + concurrent features (Suspense, transitions, deferred values) + streaming SSR + selective/progressive hydration
- Next.js-inspired production app: file-based routing, SSG/ISR, API routes, code-splitting — all running on your own stack
- End-to-end optimized application: sub-second loads, stable 60 fps, handles 10,000+ DOM mutations gracefully, survives extreme hardware/network constraints

---

### Who This Is Really For

**You, if:**

- You’re a senior frontend engineer tired of surface-level “perf tips” and ready to go god-tier
- You’re a backend/systems dev who wants to master high-performance UIs from first principles
- You’re done blaming React and want to understand the real reasons (caches, GC, layout, compositing, event loop)
- You crave hard, proud-of-it-forever projects

**Not for you, if:**

- You want fast dopamine hits or copy-paste code
- Low-level words like “mark-compact”, “TLB miss”, “bailout”, “paint chunk” scare you
- You’re not ready to wrestle C++/Rust for months

---

### Prerequisites (You Need These FR)

- Write fluent C++ or Rust (templates, lifetimes, unsafe blocks — most heavy lifting is here)
- Understand CPU pipelines, branch prediction, cache associativity, virtual memory & TLB
- Know OS basics: processes, syscalls, memory layout, scheduling
- Deep data structures & algorithms comfort
- Real experience with GDB/LLDB, Valgrind, perf, strace

---

### Realistic Commitment

**12 core weeks of deep focus**  
→ Usually stretches to 4–6 months part-time

---

## Detailed Weekly Breakdown

### Week 0.5 – Hardware & Memory Reality

Grasp how your code actually executes on real metal.

- CPU pipeline (fetch → decode → execute → writeback)
- Registers, ILP basics, instruction scheduling
- Branch prediction (static/dynamic), mispredict penalties, pipeline stalls
- Cache hierarchy (L1i/d, L2, L3), lines, associativity, write policies
- Virtual memory: paging, TLB, page faults, huge pages
- Process layout: text, rodata, data, bss, stack, heap
- Pointers: alignment, padding, strict aliasing, unaligned access cost

**Project**  
RV32I CPU simulator + 2-level cache in Rust/C++. Measure branch vs cache miss penalties on small loops.

---

### Week 1 – Networking From First Principles

Packets, not abstractions.

- TCP/UDP sockets (bind/listen/accept, connect/send/recv)
- 3-way handshake, sequence/ack, sliding window, flow/congestion basics
- HTTP/1.1: headers, chunked, keep-alive, pipelining
- HTTP/2 intro (multiplexing, HPACK)
- TLS 1.3 handshake overview (no crypto deep dive)
- WebSocket: upgrade, framing, masking, ping/pong
- Debugging: Wireshark filters, tcpdump, tc/netem latency/loss simulation

**Project**  
Persistent HTTP/1.1 client + server with chunked support. Test under high latency / packet loss.

---

### Weeks 2–3 – Browser Rendering Engine

From markup to pixels, no black boxes.

#### HTML Parsing
- WHATWG tokenizer (13 states, 67 transitions)
- Tree construction, error recovery, quirks mode
- Script execution timing (blocking/async/defer)

#### CSS Engine
- Tokenizer/parser for selectors, properties, at-rules
- Specificity + cascade (including layers)
- Computed styles, inheritance, media queries

#### Layout Engine
- Box model, margin collapse, formatting contexts
- Floats, positioning, full Flexbox algorithm, full Grid algorithm
- Inline layout, line breaking, text shaping

#### Paint & Composite
- Stacking contexts, layer promotion, paint order
- Display lists / paint chunks
- Basic scanline rasterizer + GPU texture/compositing hints

**Project**  
Browser that renders real Wikipedia pages (text, images, fonts, simple animations). Log timings: parse → style → layout → paint → composite.

---

### Weeks 4–5 – JavaScript Engine

Turn source code into running behavior.

#### Parsing & AST
- Lexer + recursive descent parser
- AST construction, scope analysis, hoisting, TDZ

#### Execution
- Bytecode design, stack VM, opcode dispatch
- Closures (environment chains), prototypes, inline caches

#### Memory Management
- Mark-sweep GC → generational (semi-space nursery + mark-compact)
- Incremental GC basics, WeakMap/WeakSet
- Memory profiling & leak detection

#### Event Loop
- Microtask/macrotask queues, requestAnimationFrame, requestIdleCallback
- Task prioritization

**Stretch**  
Polymorphic inline cache + basic speculative JIT

**Project**  
Run real JS (classes, closures, async/await, Promises). Integrate with DOM. Optimize GC pauses on hot paths.

---

### Week 6 – Virtual DOM & Reconciliation

Understand why React feels fast (when done right).

- Naive O(n³) diff → keyed O(n) + component/element/list heuristics
- Fiber: unit of work, yielding, work-in-progress tree
- Scheduling: rAF batching, time slicing, priority lanes
- Jank prevention: read/write batching, CSS containment, transform-only animations

**Project**  
VDOM library. Stress-test 10,000+ node updates. Compare perf with/without keys.

---

### Week 7 – React & Next.js Internals

Rebuild the core machinery.

- Fiber reconciler: render/commit phases, effect lists, lanes
- Hooks: queue, cursor, memoization, cleanups
- Concurrent mode: Suspense, transitions, deferred values, auto-batching
- SSR: renderToPipeableStream, selective hydration, double-pass fixes
- Next.js layer: file-based routing, SSG/ISR, API routes, code splitting

**Project**  
Mini React + streaming SSR server + hydration + simple file router.

---

### Week 8 – Performance Engineering Mastery

Real tools & patterns that ship results.

- Profiling: Chrome Perf panel, React Profiler, Lighthouse (LCP/INP/CLS)
- Optimizations: memoization, virtualization, AVIF/WebP + srcset, font subset/preload
- Critical path: critical CSS, render-blocking elimination, preload/preconnect
- Bundle discipline: tree shaking, route-based splitting

**Project**  
Optimize a real slow SPA → <1s LCP + stable 60 fps. Full metrics + trace documentation.

---

### Week 9 – Engine Hacking & Advanced Debugging

Touch the real code.

- Build V8 from source → custom bytecode/tracing
- Build Chromium/Servo → instrument layout/compositor
- WASM: linear memory, JS interop, SIMD basics

**Project**  
Add custom profiling to your engine. Accelerate compute-heavy task with WASM (e.g. image filter/physics).

---

### Week 10 – Extreme Constraints

Survive when everything is taken away.

- 64 KB RAM simulation, 10–20 MHz CPU
- Tiny JS subset, manual memory management
- 2G network, high packet loss, long RTT
- Small-screen rendering optimizations

**Project**  
Port mini-browser + UI framework to constrained environment. Document the ruthless cuts needed.

---

### Weeks 11–12 – Capstone Project

Build your own coherent web platform.

- Custom browser engine (HTML/CSS/JS subset)
- Fiber + hooks + concurrent React-like framework
- Streaming SSR + progressive/selective hydration
- Next.js-style app (routing, SSG/ISR, API endpoints)
- Comprehensive performance tracing suite
- WASM acceleration for critical paths
- Full constraint/stress testing

---

### What Success Looks Like

- Complex UIs rendering at stable 60 fps
- Smooth handling of 10,000+ concurrent DOM updates
- Sub-second initial page loads (real numbers)
- Graceful degradation & progressive enhancement
- Complete documentation: diagrams, architecture, traces, metrics

---

You’ll walk away with something rare:

**Deep intuition across the entire stack — CPU → memory → network → rendering → JS → React.**  
**The confidence to debug and optimize at any layer.**  
**The ability to read/contribute to V8, Chromium, or similar codebases.**

---

this path is hard ik everything in this world hard at start soon you gonna suffer and it will break you a little but at end winning only matters

But if you finish it, you’ll have built something most engineers never even attempt — and you’ll never see web perf the same way again

**thank me later :)**
