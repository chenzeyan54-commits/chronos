# <img src="./assets/logo.svg" alt="Chronos Logo" width="32" height="32" align="absmiddle" style="vertical-align: middle; margin-right: 8px;" /> Chronos

**The Deterministic Simulation Testing (DST) Framework for Node.js & TypeScript**

[![npm version](https://img.shields.io/npm/v/@sx4im/chronos-core.svg?color=indigo)](https://www.npmjs.com/package/@sx4im/chronos-core)
[![npm downloads](https://img.shields.io/npm/dm/@sx4im/chronos-vitest.svg?color=blue)](https://www.npmjs.com/package/@sx4im/chronos-vitest)
[![CI status](https://github.com/sx4im/chronos/actions/workflows/ci.yml/badge.svg)](https://github.com/sx4im/chronos/actions/workflows/ci.yml)
[![determinism guard](https://img.shields.io/badge/determinism%20guard-passing-brightgreen)](./packages/core/test/determinism.test.ts)
[![good first issues](https://img.shields.io/github/issues/sx4im/chronos/good%20first%20issue?color=7057ff&label=good%20first%20issues)](https://github.com/sx4im/chronos/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)
[![license: MIT](https://img.shields.io/badge/license-MIT-blue)](./LICENSE)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Vitest](https://img.shields.io/badge/Vitest-native-FCC72B?logo=vitest&logoColor=black)](https://vitest.dev/)

> **Find 1-in-a-million race conditions in concurrent & distributed systems and replay them bit-for-bit from a single integer seed.** Inspired by FoundationDB & TigerBeetle, built natively for TypeScript & Node.js.

---

## Explainer Video

[![Watch the Explainer Video](./assets/video-thumbnail.jpg)](https://www.youtube.com/watch?v=7d9_jUrygKM)

---

## Table of Contents

- [Why Chronos?](#why-chronos)
- [The Magic Moment](#the-magic-moment)
- [Key Features](#key-features)
- [Quickstart & Installation](#quickstart--installation)
- [Architecture & System Flow](#architecture--system-flow)
- [How Deterministic Simulation Testing (DST) Works](#how-deterministic-simulation-testing-dst-works)
- [Simulated Environment vs Real Environment](#simulated-environment-vs-real-environment)
- [Packages Overview](#packages-overview)
- [CLI Reference](#cli-reference)
- [Examples & Reference Implementations](#examples--reference-implementations)
- [Comparison: Chronos vs Traditional Testing vs Madsim / Turmoil](#comparison-chronos-vs-traditional-testing-vs-madsim--turmoil)
- [Security](#security)
- [Contributing](#contributing)
- [License](#license)

---

## Why Chronos?

Async bugs, heisenbugs, and network race conditions in Node.js microservices, Raft consensus nodes, CRDTs, and distributed databases are notoriously hard to debug. They manifest once in CI, log an intermittent timeout, and disappear when you try to attach a debugger.

**Chronos solves this by replacing real-world entropy with deterministic virtual primitives.** It executes your concurrent code on a **single controlled thread** using:

* **Virtual Clock**: Fast-forwards time instantly (milliseconds or hours in fractions of a second).
* **Seeded PRNG**: `xoshiro256**` generator for 100% reproducible random choices.
* **Simulated Network**: Configurable latency, packet drops, duplication, network partitions, and node crash/restarts.
* **Entropy Safety Guards**: Fails fast if non-deterministic methods like `Date.now()`, `Math.random()`, or real `setTimeout` escape into your simulation.

If a failure occurs across 10,000 randomized simulation runs, Chronos outputs a **failure capsule** containing the exact seed. Running `chronos replay <capsule>` recreates the **exact execution path, bit-for-bit, every single time.**

---

## The Magic Moment