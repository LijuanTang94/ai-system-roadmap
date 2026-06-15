# Progress

Log once a week. The template is at the bottom — copy it to the top and fill it in.

---

## Week 1 (2026-06-13 ~ )

**Completed:**
- Micrograd: watched Karpathy's "building micrograd" video and reimplemented it
  from scratch (`code/micrograd.ipynb`) — `Value` autograd engine, `backward()`
  via topological sort, `Neuron`/`Layer`/`MLP`, and a working training loop.
  Verified grads against PyTorch autograd. Note: `notes/micrograd.md`.

**Hours:**
-

**Reflection:**
- Backprop clicked: it's the chain rule applied locally, node by node. The two
  gotchas were grad accumulation (`+=`) and zeroing grads each training step.

---

<!--
Template:

## Week N (YYYY-MM-DD ~ )

**Completed:**
-

**Hours:**
-

**Reflection:**
-
-->
