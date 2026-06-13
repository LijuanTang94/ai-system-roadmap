# Curriculum — What to Study, With Materials

A concrete plan for the roadmap in [README.md](README.md).
Each item lists the **primary material** (watch/read) and a **deliverable** (build/write).
Default pace: ~10 hrs/week, ~12 weeks. Adjust freely.

> Rule of thumb: for every video you watch, write the code yourself in `code/`
> and a short note in `notes/`. Don't just watch — rebuild.

---

## Suggested 12-Week Schedule

| Week | Focus | Items |
|------|-------|-------|
| 1 | Neural Networks | Micrograd, Backpropagation |
| 2 | Neural Networks | Embedding (makemore) |
| 3 | Transformer | Attention, Self-Attention |
| 4 | Transformer | Multi-Head Attention (build nanoGPT) |
| 5 | CS336 | Tokenization (BPE) |
| 6–7 | CS336 | Training a Transformer LM |
| 8 | CS336 | Scaling Laws |
| 9 | Inference | KV Cache |
| 10 | Inference | PagedAttention |
| 11 | Inference | Continuous Batching |
| 12 | SGLang | Scheduler, Router, Prefix Cache |

---

## Karpathy "Zero to Hero" — Which Videos, In What Order

The playlist (https://karpathy.ai/zero-to-hero.html) has 9 videos (~18h).
You do **not** need to watch them all. Follow this order:

| # | Video | Length | Roadmap | Must-watch? |
|---|-------|--------|---------|-------------|
| 1 | The spelled-out intro to neural networks and backpropagation: **building micrograd** | ~2h25 | Phase 1 · Micrograd + Backprop | ✅ Yes |
| 2 | The spelled-out intro to language modeling: **building makemore** | ~2h | Phase 1 · Embedding (foundation) | ✅ Yes |
| 3 | Building makemore **Part 2: MLP** | ~1h15 | Phase 1 · Embedding | ✅ Yes |
| 4 | Building makemore Part 3: Activations & Gradients, BatchNorm | ~1h55 | (training tricks) | ⚪ Skippable |
| 5 | Building makemore **Part 4: Backprop Ninja** | ~1h55 | Phase 1 · Backpropagation | 🔸 Recommended |
| 6 | Building makemore Part 5: WaveNet | ~56m | — | ⚪ Skippable |
| 7 | **Let's build GPT: from scratch, in code, spelled out** | ~2h | Phase 2 · all (Attention) | ✅ Yes |
| 8 | **Let's build the GPT Tokenizer** | ~2h13 | Phase 3 · Tokenization | ✅ Yes |
| 9 | Let's reproduce GPT-2 (124M) | ~4h | Phase 2/3 stretch | 🔸 Optional |

**Minimal path:** #1 → #2 → #3 → #7 gets you through the main line (write your own
micrograd, a char-level LM, then a GPT from scratch). Come back for #8 at Phase 3.

While watching, type the code yourself (repos at github.com/karpathy) and save it in `code/`.

---

## Phase 1: Neural Networks
**Course:** Andrej Karpathy — *Neural Networks: Zero to Hero*
(playlist: https://karpathy.ai/zero-to-hero.html)

| Item | Primary material | Deliverable |
|------|------------------|-------------|
| Micrograd | Video: *The spelled-out intro to neural networks and backpropagation: building micrograd* (~2.5h) · repo: github.com/karpathy/micrograd | Reimplement micrograd from scratch in `code/micrograd/` (Value, backward, a tiny MLP) |
| Backpropagation | Same video + *Building makemore Part 4: Becoming a Backprop Ninja* | Hand-derive grads for one layer; verify against autograd |
| Embedding | *The spelled-out intro to language modeling: building makemore* + *Part 2: MLP* | Bigram + MLP char-level model; visualize the embedding table |

## Phase 2: Transformer
**Read first:** *Attention Is All You Need* (arxiv 1706.03762) · Jay Alammar — *The Illustrated Transformer*

| Item | Primary material | Deliverable |
|------|------------------|-------------|
| Attention | Karpathy *Let's build GPT: from scratch, in code, spelled out* (~2h) | Implement scaled dot-product attention by hand |
| Self Attention | Same video (self-attention section) | Single-head self-attention block on toy data |
| Multi Head Attention | Same video + repo: github.com/karpathy/nanoGPT | Build a working nanoGPT in `code/transformer/`; train on tiny Shakespeare |

*(Optional stretch: Karpathy — Let's reproduce GPT-2 (124M).)*

## Phase 3: CS336
**Course:** Stanford CS336 — *Language Modeling from Scratch*
(site: stanford-cs336.github.io · lectures on YouTube · assignments are public)

| Item | Primary material | Deliverable |
|------|------------------|-------------|
| Tokenization | CS336 tokenization lecture + Assignment 1 (BPE) · also Karpathy *Let's build the GPT Tokenizer* | Implement a BPE tokenizer in `code/bpe/`; train it on a small corpus |
| Training | CS336 Assignment 1/2 (build & train a Transformer LM) + systems/optimization lectures | Train your own small LM end-to-end; log loss curve |
| Scaling Laws | CS336 scaling-laws lecture · papers: Kaplan et al. 2020 (arxiv 2001.08361), Chinchilla / Hoffmann et al. 2022 (arxiv 2203.15556) | Note in `papers/` summarizing the compute-optimal (Chinchilla) result |

## Phase 4: Inference
| Item | Primary material | Deliverable |
|------|------------------|-------------|
| KV Cache | Blog: *Transformers KV Caching Explained* (search) + add caching to your nanoGPT | Add a KV cache to your Phase-2 model; measure the speedup |
| PagedAttention | Paper: *Efficient Memory Management for LLM Serving with PagedAttention* (vLLM, arxiv 2309.06180) + vLLM blog | `papers/vllm-pagedattention.md`: explain the block table & why it helps |
| Continuous Batching | Orca paper (OSDI '22) + Anyscale blog *How continuous batching enables 23x throughput* | Note contrasting static vs. continuous batching |

## Phase 5: SGLang
**Read first:** *SGLang: Efficient Execution of Structured Language Model Programs* (arxiv 2312.07104) — covers RadixAttention.
**Repo:** github.com/sgl-project/sglang (read the code + docs)

| Item | Primary material | Deliverable |
|------|------------------|-------------|
| Scheduler | SGLang source (`python/sglang/srt/managers/`) | Trace one request through the scheduler; write up the flow |
| Router | SGLang router docs/code | Note on how requests are load-balanced across workers |
| Prefix Cache | SGLang paper (RadixAttention section) + code | Explain how the radix tree reuses shared prefixes |

---

## Daily Loop
1. Watch/read the material for today's item.
2. Rebuild it yourself in `code/` (or write the paper note in `papers/`).
3. Add a note in `notes/` from `notes/_TEMPLATE.md`.
4. Check the box in `README.md`, then `git add -A && git commit && git push`.
