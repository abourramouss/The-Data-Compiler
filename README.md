# 📦 The Data Compiler

> **Not a parser. Not a loader. A compiler for raw data.**

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Status: Prototype](https://img.shields.io/badge/status-prototype-orange)]()
[![Made with ❤️](https://img.shields.io/badge/built_with-love-red)]()

---

## 🚀 What is this?

**The Data Compiler** is a system that **compiles declarative descriptions of binary/textual data formats** into optimized, backend-aware, representation-flexible access plans.

It treats data formats like source code.  
It emits IRs. It generates execution strategies.  
It validates, optimizes, and transforms how raw data is read — from byte streams to structured, memory-safe views.

We don’t load data. We **compile access to it**.

---

## ⚡ Why?

Because:
- Raw data lives in undocumented, weird formats
- Most tools decode eagerly or require full loads
- There was no compiler for data

Until now.

---

## 🔧 Core Concepts

- **Format as Code** – describe formats in a high-level DSL
- **IR as Schema** – internal representation captures field layout + dependencies
- **Index as Metadata** – skip reads, enable chunk access
- **Codegen as Execution** – emit code or plans based on runtime context
- **Runtime as Decision Layer** – chooses paths like `mmap`, `io_uring`, `buffer`, etc.

---

## 🧱 Compiler Pipeline

```
User Spec
   ⬇️
Format IR
   ⬇️
Validation & Offset Planning
   ⬇️
Index Generation
   ⬇️
Access Plan IR
   ⬇️
Execution Planner
   ⬇️
Backend Codegen
```

---

## ✨ Example

```python
@format
class LogEntry:
    ts: UInt64
    level: UInt8
    message: Bytes(128)

reader = compile_pkg("logs.bin")
reader.read().filter(lambda r: r.level > 3).to_numpy()
```

Behind the scenes:
- Only needed fields are accessed
- Data may never be copied
- I/O path is optimized based on traits + storage

---

## ✅ Goals

- Transparent: Feels like querying a database
- Format-aware: Knows bytes, layouts, field relationships
- Backend-agnostic: Files, blobs, RDMA, HTTP, etc.
- Efficient: Lazy, parallel, zero-copy where possible
- Composable: Meant to plug into compute frameworks

---

## 🔭 Future

- [ ] Write pipelines (format spec → file writer)
- [ ] Distributed execution support
- [ ] MLIR-style IR dialects
- [ ] Codegen to Python/C/LLVM
- [ ] Format fusion (multi-version packages)
- [ ] Fully self-contained `.pkg` data bundles

---

## 📘 TL;DR

> **Data is code.**  
> The format is the function. The compiler emits the access logic.  
> This is not a parser. This is not a loader.  
> **This is a compiler for raw data.**

---

## 📂 License

MIT © 2025
