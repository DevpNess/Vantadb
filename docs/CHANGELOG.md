# Changelog

All notable changes to the VantaDB engine will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.4.1](https://github.com/ness-e/Vantadb/compare/v0.4.0...v0.4.1) - 2026-08-01

### Added

- *(sdk,cli)* VantaDB Recovery Plan: filters, delete_by_filter, count, similar_to_key, multi-namespace search, backup manifest
- *(server)* run flush and ingestion processing async in spawn_blocking
- *(hardware)* improve Windows RAM detection without sysinfo dependency
- *(bench)* param_sweep over SIFT-128 with auto_tune bypass
- Propuesta 3 — layer-wise bulk insert con pre-computo de niveles
- Propuesta 4 — flatten + RWLock neighbor lists (HnswNeighborIndex)
- put_batch() uses InsertMode::Auto with conditional rebuild
- Add InsertMode enum + incremental threshold to BatchInsertOptions
- *(cli)* add 'vanta-cli wal compact' and 'vanta-cli wal vacuum' commands (REC-007)
- *(REC-001)* add VantaFilterOp + VantaMemoryFilterItem foundation types
- COMP-018 double-linked relationship chains — direction param en SDK, WASM, Python bindings
- COMP-025 JSON shredding Phase 2 — typed comparison filters
- multi-level LSM compaction (L0→L1→L2→L3)
- *(core)* wire Edge.reverse, TraversalDirection, add_edge/remove_edge through engine and tests
- *(core)* restore lost changes — LsmConfig, Edge.reverse, add_edge/remove_edge bidireccional (COMP-018 parcial + COMP-026 infra)
- *(index)* ACORN bitset-aware HNSW search (COMP-024)
- *(core)* Supernode mitigation — indexed relationships + label-filtered traversal (COMP-016)
- *(core)* Binary Bulk Import — bulk_import_stream + Python/WASM bindings (COMP-009)
- *(core)* Segment Optimizer Pipeline — vacuum/merge/reindex orquestado con PipelineMode (COMP-013)
- *(core)* Pluggable VecIndex trait — CPIndex + IvfIndex implement, vector_memory_search usa trait object (COMP-008)
- *(core)* Edge Label Interning — label: String → label_id: u32 (COMP-006)
- add HTML report template with 40+ placeholders, conditional blocks, dark mode, and print support
- replace web/ with Next.js 16 + shadcn/ui — archive old Vite app as web_old/
- OLD-03 + OLD-08 — Chaos harness + snapshots hard-link
- OLD-09/11/12 — Bayesian decay + TUI interactivo + Pilot program
- OLD-19 rehidratación desde shadow archive — SDK + MCP + Python
- WAL auto-rotation at 256MB (OLD-16)
- MessageThread / GcWorker for agentic chat (OLD-14)
- GraphRAG pipeline formal (OLD-02)
- *(demo)* add Python demo app (examples/demo/)
- *(cli)* connect backup/restore/doctor/inspect/stats CLI handlers
- IVF Flat index — new IndexType for inverted-file vector search (#DRV-131)
- *(DRV-122)* IQL JOINs, subqueries, SQL compatibility — 3 phases complete
- Phase 3 — planner integration + JOIN/subquery tests
- Phase 2 — physical JOIN operators + subquery filter
- NUEVO-13 HNSW ef_search auto-tuning dampening + metric gauge
- Phase 1 — SELECT/JOIN/subquery parser types and grammar
- MVCC GC reclaim + O(1) conflict check doc
- *(VFY-011)* ACID Phase 3 — snapshot isolation / MVCC
- *(drv-130)* SearchProfile + prefetch audit + T3 node reordering WONTFIX
- add search profiling instrumentation for DRV-130
- *(web-04,drv-121,drv-123)* storage versioning + planner CBO + auto-embedding polish
- *(doc-20)* add mdBook docs site with organized SUMMARY.md
- parallelize flush_all across WAL shards
- resolve P1 security/critical infra tasks (triage + DRV-054)
- *(core)* reduce default features to essential set only
- *(search)* OLD-05 — Add Unicode accent folding to snippet generation and term highlighting
- *(search)* Unicode folding for accent-insensitive snippet matching [OLD-05]
- add .antigravity/ — complete opencode fork adapted for Antigravity
- *(VFY-010)* buffered write transactions — ACID Phase 2
- *(DRV-022)* remove governance/ dead code (1235L)
- add MCP profiles, DGM Loop, harness executor, and ECO task system
- 10/10 production-ready campaign — all 9 adapters + 3 providers

### Fixed

- *(ci)* make experimental provider crates standalone workspaces so experimental check can run
- *(ci)* make hot-node eviction test platform-stable and gate experimental check
- *(ci)* skip remaining Miri serialize tests hitting croaring FFI
- *(ci)* skip Miri tests hitting croaring FFI and relax new react-hooks lint rule
- *(web)* regenerate lockfile with all platform binaries
- *(ci)* make Miri runnable and complete lockfile for Linux builds
- restore Unix build after std::os::unix::fs::link removal
- *(test)* align parser certification with Int→Float literal change
- *(hardware)* remove needless returns in total_memory detection
- *(bench)* isolate Ingest timer double rebuild & consolidate competitive analysis docs
- *(index)* correct neighbor selection sort order and HNSW benches
- *(bench)* index vector_store by level index for concurrent benchmarks
- *(tests)* index vector_store by level index, update memory telemetry for LSM
- *(search)* remove L0-only VantaFile assumption from HNSW search
- correct accumulator test target and parser Int→Float expectations
- *(backlog)* update 5 web task descriptions to match current Next.js codebase
- skip crash active-writes test on Windows due to compiler OOM
- ignore triple backend parity test when rocksdb feature is disabled
- ChaosTestHarness field order for correct Drop on Windows
- prevent test binary hang from indicatif steady_tick background thread
- *(docs)* cross-validation corrections — pricing TBD, latency splits, CI status, tt fallback, web_old purge
- clippy double_ended_iterator_last in physical_plan.rs:466
- *(wasm)* wasm-opt -Oz explicito + HNSW contention docs
- *(wal)* eliminar clonacion de WalRecords en ShardedWal::batch_append
- *(security)* DRV-050 — Sanitize and validate input queries in MCP query_lisp tool to prevent injection attacks
- *(sdk)* add VANTADB_EXPORT_BASE_DIR with canonical path resolution for safe exports [H-SEC-IV-003]
- *(DRV-134)* add keyboard navigation to NbAccordion — Enter, Space, Arrow keys, aria attributes
- *(VFY-003)* paginate reindex_hnsw_from_text — prevent OOM on large DBs
- *(WEB-02)* correct false functional claims on landing page
- *(VFY-001)* replace empty catch blocks in hardening.test.ts — log WASM errors
- *(DRV-037)* correct types in test files — number vs string mismatches
- sync vantadb-ts package-lock.json version to 0.4.0
- remove stale RUSTSEC-2026-0176/0177 ignores from verify.ps1
- remove invalid target.wasm32-unknown-unknown.profile section from Cargo.toml
- pin release-plz/action to v0.5.131 instead of floating @main
- optimize pre-commit hook — drop redundant cargo check, scope to vantadb crate
- align tool configs with official docs, install cargo-semver-checks, update manual
- Bug Fix Phase 1 — 9 backlog tasks resolved
- normalize workflow JSONs — resolve template vars, unify casing (H7)
- expand vanta-lead and vanta-engine task permissions to match orchestration policy (C5)
- add server liveness check and error handling to campaign MCP server (ECO-004)
- close 4 pending review items — CI policy, advisory sync, experimental circuit breaker, WASM tests
- carry over uncommitted Rust/Python 10/10 fixes from sub-agents
- Rust providers top_k+namespace params, Python adapter fixes, transversal cleanup
- resolve P1-3 WASM storage scrutiny — 7 items

### Other

- fix release-plz path deps and changelog format
- versioned internal path deps + release-plz wasm block
- untrack files both committed and gitignored (env.example, review-deep tmp, Cargo_test.toml) — dirty working tree blocked release-plz
- add actions/checkout before release-plz (action needs the repo checked out)
- fix release-plz action — pass GITHUB_TOKEN via env, not with
- bump minimal-versions job timeout 15m to 30m (resolution of all minimal deps exceeds 15m)
- *(web)* add vercel.json with Next.js framework preset
- fix markdownlint violations (MD003, MD005, MD045, MD049)
- sync AutoTune opt-in in benches/tests, fix clippy/borrow, regen completions
- *(investigaciones)* complete INV-003, INV-004, and INV-005 audits
- *(bench)* mark C1/C2 as completed in BENCHMARK_OPTIMIZATION_2026.md
- *(bench)* complete P0-P4 verification cycle with full benchmark suite
- *(index)* optimize vector deserialization with bytemuck, add flat cached norms & ACORN benchmark
- *(index)* make AutoTune opt-in via HnswConfig and add efC sweep harness
- *(index)* optimize vector deserialization with bytemuck, add flat cached norms & ACORN benchmark
- *(index)* make AutoTune opt-in via HnswConfig and add efC sweep harness
- *(index)* remove unused NeighborVec import in ivf tests
- *(backlog)* update progress README and Backlog, task files and completions
- archive task files — 66 completed to complete/, 2 to closed/
- complete INV-002 memory telemetry schema design
- *(bench)* hallazgo 12 — search_layer +66-90% regression at ef>=200, root cause: neighbor list cloning
- *(INV-024)* unsafe blocks audit — 39 bloques revisados, 1 High + 1 Medium
- *(bench)* hallazgo 11 — CPU load contaminates benchmarks despite power plan
- *(bench)* B5 resolved in Fase 2 + thermal throttling confirmed
- *(bench)* regression root-cause — target-cpu=native missing from PyO3 wheel builds
- *(bench)* param_sweep results + hallazgos auto_tune/ground_truth
- *(bench)* mark B2 completed, A2 skipped in BENCHMARK_OPTIMIZATION_2026.md
- *(bench)* B2 visited capacity + A2 skipped + profile.bench
- *(benchmarks)* add baseline results from 4 cargo benches (2026-07-30)
- E2 — per-thread NeighborVec pool en search_layer
- E1 inline neighbor cache + neighbor_index DashMap flatten + D1-D4 benchmark
- *(perf)* Propuesta 2 (NN-Descent) revertida — regresión 7-1,300× vs parallel insert
- Documentar resultado Propuesta 1a — deferred shrink regresion +53%
- Add execution plan for INDEX_REBUILD_OPTIMIZATION
- Update COMPETITIVE_ANALYSIS + INDEX_REBUILD_OPTIMIZATION with real results
- Add incremental insert tests + Criterion benchmark
- cargo generate-lockfile (purge stale entries) + update INV-001 report
- *(audit)* investigate 3 RUSTSEC advisories (INV-001)
- update COMPETITIVE_ANALYSIS.md with Fase 2 benchmark results
- *(engine)* Phase 1 optimizations complete — WAL batch, ef_construction, select_neighbors, docs
- *(engine)* P1-P4 ingestion optimizations + cache warmer metrics + SDK fixes
- REC-010 py.typed marker + maturin wheel include
- add missing .md files — plan deletion + research docs
- backlog cleanup Jul 29 — DEVOPS-15 WONTFIX, COMP-029 investigation, plan cleanup
- add backlog validation audit report 2026-07-28
- update OLD-20 task status, engineering plan recitation, and MCP config
- gate engine_mmap_resident_bytes to test-only, clean dead_code annotations
- *(lsm)* add L3 archive tier with pre-allocated levels, remove unsafe dynamic segment growth
- update Backlog.md COMP-018 to ⚠️ Parcial + add progreso entry for lost changes restoration
- reorganize docs/ directory — move loose files to proper subdirs
- *(web)* showcase page copy — español nativo, tono comunidad
- clippy fixes — dead_code annotations + contains_key to Entry::Vacant
- COMP-013 Segment Optimizer Pipeline — audit completado y migrado a progreso
- pipeline review of OLD-10/16/20/21 — update backlog with findings
- migrate NUEVO-14 (WASM bundle size) from backlog to progreso
- update OLD-03 entry with post-certification hang fix details
- clippy fixes and test maintenance
- *(docs)* restructure docs/web/ into guides/reference/standards + instruccion unificacion
- migrate legacy skills (vantadb-certify/audit/full-review) to unified-review
- fix inaccuracies in web docs after file-level verification
- archive old Swiss/Neubrutalism design docs → docs/web_old/ and create new docs/web/ for Next.js 16 + shadcn/ui frontend
- update stale references from old Vite/TanStack web to Next.js 16
- P8 — mark CLI-01, DEVOPS-HOMEBREW, DEVOPS-PY313, DEVEX-DEMO, DEVEX-EXAMPLES completed
- *(ci)* verify published wheels on Python 3.13
- DRV-041 VFY-006 VFY-007 backlog housekeeping — mark completed, migrate to progreso
- update progreso, Backlog, CHANGELOG, and plan for DRV-131 (IVF index) (#DRV-131)
- *(drv-130)* mark complete, add cfg-gate fix to progreso and plan
- *(index)* gate SearchProfile behind #[cfg(debug_assertions)]
- add WEB-03, VFY-004, WEB-04, DRV-121, DRV-123 entries from P4 engineering health wave
- migrate DOC-20 (mdBook docs site) to progreso
- add ponytail comment on flat_search O(n) scan
- *(phase3)* evaluacion cobertura 7 modulos - todas document-only
- DRV-036, DRV-038, DRV-029, DRV-032, DRV-055 — TS guards/types, PyO3 cache allocs & MCP test cleanup
- *(ts)* DRV-034 — Eliminate 35 duplicate try-catch blocks in VantaDB TS SDK using private _wasm helper
- *(core)* add 21 Miri tests covering all unsafe patterns in src/index
- update Backlog and progreso for Phase 0 completion
- *(ci)* point dependabot PRs to develop branch
- close OLD-05 — remove from backlog, add to progreso, mark task completed
- update audit state for Jul 24 full audit
- update backlog metadata and progreso after Jul 24 triage
- add reindex_hnsw_from_text with pagination docs [VFY-003]
- *(python)* LRU cache O(n)→O(1) with u64 tick-based eviction [P2-3]
- fix prettier formatting in NbAccordion.tsx
- *(engine)* reduce UnifiedNode clones and merge cardinality_stats write in insert() [H3-ALLOC-001] [H3-LCK-002]
- *(engine)* split 4076L tests.rs into 7 focused module files [H08-ARCH-001]
- cargo fmt — engine/ops.rs, engine/tests.rs
- *(blog)* publish 3 existing blog posts
- remove stale plan files (completed campaigns)
- extract recover_valid_records() from WalWriter::open_with_buffer() (DRV-015)
- mark DRV-011 as completed in Backlog and progreso
- extract collect_scores() helper from vector_search and hybrid_search (DRV-008)
- update progreso tracking and Backlog after audit fixes
- add license MIT to TS SDK examples
- *(sdk)* paginate list() over IDs to prevent OOM — DRV-004
- update agent config, pipeline routing, MCP profiles + tracking
- *(sdk)* extract put_one() from put/put_batch — DRV-002
- *(sdk/search)* extract phrase/snippet/debug/text_index submodules
- plan file + DRV-001 task for harness test
- update agent configs, skills, prompts, and operating manual
- remove legacy task system files (legacy/, proxy/, iter.md, stale scripts, tasks/plan.md)
- remove dead Claude Code hooks (ECO-001)
- reconcile SKILLS-MANIFEST.md with disk, remove 13 dead skill dirs (ECO-003)
- remove contradictory --no-verify rule, keep Regla 1 as single source of truth (ECO-002)
- push line coverage from 53.85% to 80.55% (+728 tests, 23 modules)
- coverage desde 53.85% a 70.73% — +262 tests agregados
- remove 5 completed task files — keep only REV-003 (partial)
- resolve 6 pending task files — docs updated, CI evaluated
- cleanup — remove 58 stale task files, update completed plans
- resolve P1-1/P1-3b/P1-4/P2-2 — ADR tiers, WASM CI, TEST_MAP update
- resolve P0-1 and P0-2 — GHA continue-on-error audit + deny.toml cleanup
- restructure adapters by language — Python for frameworks, Rust for providers

### Added

- IVF Flat index — inverted file with k-means clustering (no external deps). New `IndexType::Ivf` on `HnswConfig`. Lazy-built on first search, serialized in v8 format. ~50× faster than brute-force Flat on 1M vectors at ~90% recall.
- Multi-level LSM compaction (L0→L1→L2→L3) — `StorageEngine.vector_store` splits into per-level VantaFiles. `SegmentRegistry` handles legacy migration. `compact_level()` promotes live nodes between tiers. New `PipelineMode::CompactOnly`/`CompactL0Only` variants. Write amplification reduced from O(all data) to O(L0 size).

## [0.4.0] - 2026-07-20

### Added

- Initial public release of VantaDB.
- Embedded persistent vector/graph database engine.
- HNSW vector index with configurable distance metrics.
- WAL (Write-Ahead Log) with automatic crash recovery.
- Arrow IPC integration for zero-copy data interchange.
- CLI tool (`vanta`) for database operations.
- HTTP server with rate limiting and TLS support.
- Python SDK (`vantadb_py`) with PyO3 bindings.
- WASM build for browser-based querying.
- TypeScript SDK (`vantadb-ts`).
- AI framework adapters: LangChain, LlamaIndex, Haystack, CrewAI, DSPy, Litellm, OpenAI, Ollama, Mem0, Letta.
- MCP server (`vantadb-mcp`) for Model Context Protocol.
- Prometheus metrics and OpenTelemetry tracing.
- Encryption at rest (AES-GCM).
- PITR (Point-in-Time Recovery).
- WAL shipping for replication.
- Hot-reload of configuration.
- Failpoints for fault injection testing.
- Custom allocator support (mimalloc, jemalloc).

### Fixed

- CI/CD pipelines: FUZZ, release binaries, adapters, SBOM, wheels, code coverage — all green.
- Serialization bounds check overflow in `src/index/serialize.rs`.
- `vantadb-mcp` excluded from binary releases (library-only crate).
- Conditional `Attach to Release` step in adapter release workflow.
- Code coverage runner RAM increase (6GB → 8GB) to prevent LLD SIGBUS.

### Changed

- Workspace version reset to v0.4.0 — clean semantic versioning start.
- All previous tags (v0.1.0 through v0.3.0-stable, wasm-*, ts-*, adapters-*) removed.
- Root crate version inherits from `[workspace.package]`.

### Removed

- All pre-release tags and orphan GitHub Releases from v0.1.x era.
