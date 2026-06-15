# Micrograd

> Date: 2026-06-15

## What I Learned
- A scalar autograd engine: every number is wrapped in a `Value` that remembers
  its `data`, its `grad`, the children that produced it (`_prev`), and the op
  (`_op`). Building expressions builds a DAG.
- Each op (`+`, `*`, `**`, `tanh`, `exp`) defines a local `_backward()` closure
  that knows how to push `out.grad` onto its inputs via the chain rule.
- `backward()` = topological sort of the graph, set the output's `grad = 1.0`,
  then call each node's `_backward()` in reverse topo order.
- A neural net is just a big expression: `Neuron` → `Layer` → `MLP`, and training
  is forward pass → compute loss → `backward()` → nudge every parameter by
  `-lr * grad`.

## Key Concepts
- **Chain rule, locally applied.** Backprop is just repeatedly multiplying local
  derivatives; no global magic.
- **Gradients accumulate (`+=`).** Critical when a node feeds multiple children
  (e.g. `b = a + a`). Using `=` instead of `+=` would be a silent bug.
- **Zero the grads each step.** Because grads accumulate, you must reset
  `p.grad = 0.0` before each `loss.backward()` in the training loop — forgetting
  this was the classic gotcha.
- **tanh derivative:** `1 - tanh(x)**2`. Verified my grads against PyTorch
  autograd and they matched.
- **Topological sort** guarantees we only call a node's `_backward()` after all
  of its outputs already have their grads.

## Questions
- How does this scale to tensors (PyTorch) instead of scalars? (vectorized ops,
  broadcasting — the next step.)
- Why `+=` exactly, derived from the multivariable chain rule — revisit in
  makemore Part 4 (Backprop Ninja).

## Summary
Built micrograd from scratch following Karpathy's video: a working scalar
autograd engine + a tiny MLP that trains on a 4-example toy dataset, with loss
dropping over 20 gradient-descent steps. Code in `code/micrograd.ipynb`.
Backprop is "just" the chain rule applied node-by-node over a topologically
sorted graph — this demystified what autograd actually does.
