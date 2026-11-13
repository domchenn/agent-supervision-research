# Toy model: supervising a worker with two bad channels

## Players

- **Designer (principal):** wants the real task done. Sets the audit policy and penalty.
- **Worker agent:** chooses how to split effort between the real task and two ways of gaming the evaluation.
- **Supervisor agent:** runs audits chosen by the designer. Starts as a perfect auditor; later versions can be imperfect or sycophantic themselves.

## Worker's choices

Let $e_T \ge 0$ be the worker's effort on the true task.
Let $e_S \ge 0$ be its effort on sycophancy: appealing to what the evaluator believes or wants to hear.
Let $e_H \ge 0$ be its effort on reward hacking: exploiting a flaw in how the output is scored.

## What the evaluator sees

The evaluator gives the score $s$:

$$
s = e_T + \beta e_S + \gamma e_H + \varepsilon
$$

where $\beta > 0$ is how much the evaluator rewards agreement, $\gamma > 0$ is how exploitable the scoring rule is, and $\varepsilon$ is mean-zero noise.

The designer's true payoff depends only on $e_T$.

## Audits

The supervisor has two audit technologies, because the two failures leave different evidence:

- **Counterfactual probe** (catches sycophancy): rerun the task with a different stated user opinion and see if the answer moves. Run with probability $p_S$; if run, it detects sycophancy with probability $q_S$.
- **Process inspection** (catches hacking): inspect how the output was produced, or score it on a held-out evaluator. Run with probability $p_H$; if run, it detects hacking with probability $q_H$.

If caught, the worker pays penalty $F$. Each audit costs the designer $c_S$ or $c_H$.

## Worker's payoff

Let $C(e_T, e_S, e_H)$ be the worker's cost of effort. The worker's expected payoff is

$$
u_W = \mathbb{E}[s] \;-\; p_S\, q_S\, F \cdot \mathbf{1}[e_S > 0] \;-\; p_H\, q_H\, F \cdot \mathbf{1}[e_H > 0] \;-\; C(e_T, e_S, e_H)
$$

where $\mathbf{1}[\cdot]$ equals 1 if the condition holds and 0 otherwise.

## Step 1 (single channel)

Drop hacking: set $e_H = 0$. Assume a fixed total effort budget $E$ so that $e_T + e_S = E$, and that effort costs are the same either way.

If the worker shifts all effort to sycophancy, its expected score changes from $E$ to $\beta E$. So sycophancy pays only if $\beta > 1$, and the gain is

$$
\Delta = (\beta - 1) E .
$$

Honesty is a best response when the expected penalty is at least that gain:

$$
p_S\, q_S\, F \;\ge\; (\beta - 1) E
\quad\Longrightarrow\quad
p_S^{*} = \frac{(\beta - 1) E}{q_S\, F}.
$$

Here $p_S^{*}$ is the minimum audit probability that deters sycophancy.

**Things to check yourself:** Is the all-or-nothing deviation the right one to consider? What changes if the penalty scales with $e_S$ instead of being a flat $F$?

## Step 2 (two channels, budget)

The designer has an audit budget $B$:

$$
p_S\, c_S + p_H\, c_H \le B .
$$

**Questions:**
1. Given $B$, how should the designer split audits between the two technologies?
2. If $p_S$ rises, does the worker move effort into hacking (substitution)?
3. What if the supervisor is itself an LLM with its own $\beta$ (it can be flattered)?

## Step 3 (open)

- Multiple workers; supervisor attention as a scarce resource.
- Debate: two workers critique each other instead of a supervisor auditing.
- The hybrid case (Wen et al. 2024): hacking carried out *through* persuasion. Is that a third channel?
