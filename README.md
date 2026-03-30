# ai-improve-opensource-ip-gsoc2026
GSoC 2026 — Using AI to Improve Open-Source IP | Verilog to TL-Verilog conversion using LLMs on BaseJump STL | FOSSi Foundation


# Using AI to Improve Open-Source IP — GSoC 2026

**Organization:** FOSSi Foundation  
**Project:** Using AI to Improve Open-Source IP  
**Mentor:** Steve Hoover  
**Applicant:** Harshitha  
**Duration:** 350 hours (Large)  

---

## Project Overview

Transaction-Level Verilog (TL-Verilog) models are smaller, cleaner, 
and less bug-prone than their Verilog counterparts. This project uses 
LLM-based agentic flows to automate conversion of open-source Verilog 
to TL-Verilog, backed by formal equivalence verification.

**Target Repository:** [BaseJump STL](https://github.com/bespoke-silicon-group/basejump_stl)  
**Conversion Tool:** [conversion-to-TLV](https://github.com/stevehoover/conversion-to-TLV)

---

## Target Modules (BaseJump STL)

| Module | Description | Complexity |
|--------|-------------|------------|
| `bsg_counter_clear_up` | Clearable up-counter | Simple |
| `bsg_arb_round_robin` | Round-robin arbiter | Medium |
| `bsg_arb_round_robin_composable` | Composable arbiter sub-module | Medium |
| `bsg_arb_round_robin_two_level` | Two-level priority arbiter | Medium |

---

## Tool Exploration Findings

By cloning and running the conversion tool on `bsg_counter_clear_up`, 
I identified these specific issues:

| # | Finding | Proposed Fix |
|---|---------|--------------|
| 1 | `bsg_defines.sv` dependency not auto-resolved | Automate include dependency resolution using Yosys |
| 2 | Tool uses `GOOGLE_API_KEY` but documents `GEMINI_API_KEY` | Fix API key variable naming inconsistency |
| 3 | `M5/bin/m5` binary missing — prompts not preprocessed | Fix M5 initialization in setup flow |
| 4 | Gemini response returns unexpected `macros` field — parser fails | Improve response validation and error recovery |
| 5 | No graceful retry/backoff for free tier rate limits | Add exponential backoff for API rate limits |

---

## Proposed Improvements

1. **Dependency Auto-Resolution** — use Yosys to scan and resolve
   `include` files before conversion begins
2. **API Key Consistency** — fix `GEMINI_API_KEY` vs `GOOGLE_API_KEY`
   mismatch across codebase
3. **M5 Setup Fix** — ensure M5 macro preprocessor initializes correctly
4. **Response Parser Hardening** — handle unexpected LLM response fields
   gracefully
5. **Rate Limit Handling** — add exponential backoff for free tier APIs
6. **Yosys Signal Matching Automation** — address the existing TODO item
   in the repo

---

## Environment Setup

Tools installed and verified:
- ✅ Yosys 0.58
- ✅ SymbiYosys v0.63
- ✅ EQY v0.63
- ✅ Python dependencies (openai, anthropic, google-generativeai)
- ✅ BaseJump STL cloned and explored
- ✅ Conversion flow run on `bsg_counter_clear_up`

---

## Timeline

| Weeks | Tasks |
|-------|-------|
| 1-2 | Fix tool bugs (M5, API key, dependency resolution) |
| 3-4 | Convert `bsg_counter_clear_up` — learn flow deeply |
| 5-8 | Convert `bsg_arb_round_robin` (3 sub-modules) |
| 9-11 | Automate Yosys signal matching (TODO item) |
| 12-14 | Document, push training data, final report |

---

## Screenshots
See `/screenshots` folder for tool exploration evidence.

---

## Skills
Verilog, Python, TL-Verilog, Formal Verification, LLM APIs, Yosys, 
SymbiYosys, EQY
