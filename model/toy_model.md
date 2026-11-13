# Toy model: supervising a worker against sycophancy

## Players

- **Designer:** wants truthful answers. Sets how often the supervisor audits and how large the penalty is.
- **Worker agent:** answers users' questions. Chooses between answering truthfully and telling users what they want to hear.
- **Supervisor agent:** audits the worker's answers. Starts as a perfect auditor; later versions can make mistakes or be flattered themselves.

## Worker's choices

Let $e_T \ge 0$ be the worker's effort on truthful answering.
Let $e_S \ge 0$ be its effort on sycophancy: telling the user what they believe or want to hear.

## What the evaluator sees

The evaluator (the user, or a rating based on users) gives the score $s$:

$$
s = e_T + \beta e_S + \varepsilon
$$

where $\beta > 0$ is how much the evaluator rewards agreement, and $\varepsilon$ is mean-zero noise.

The designer's true payoff depends only on $e_T$.

## Audits

The supervisor runs a **counterfactual probe**: it reruns the question with a different stated user opinion and checks whether the answer moves. The supervisor audits with probability $p_S$, and an audit detects sycophancy with probability $q_S$. If caught, the worker pays penalty $F$. Each audit costs the designer $c_S$.

## Worker's payoff

Let $C(e_T, e_S)$ be the worker's cost of effort. The worker's expected payoff is

$$
u_W = \mathbb{E}[s] \;-\; p_S\, q_S\, F \cdot \mathbf{1}[e_S > 0] \;-\; C(e_T, e_S)
$$

where $\mathbf{1}[\cdot]$ equals 1 if the condition holds and 0 otherwise.

## Step 1: When does a supervisor deter sycophancy?

Assume a fixed total effort budget $E$, so that $e_T + e_S = E$, and that effort costs the same either way.

If the worker shifts all effort to sycophancy, its expected score changes from $E$ to $\beta E$. So sycophancy pays only if $\beta > 1$, and the gain is

$$
\Delta = (\beta - 1) E .
$$

Truthfulness is a best response when the expected penalty is at least that gain:

$$
p_S\, q_S\, F \;\ge\; (\beta - 1) E
\quad\Longrightarrow\quad
p_S^{*} = \frac{(\beta - 1) E}{q_S\, F}.
$$

Here $p_S^{*}$ is the minimum audit probability that deters sycophancy.

**Check yourself:** Is the all-or-nothing deviation the right one to consider? What changes if the penalty grows with $e_S$ instead of being a flat $F$?

## Step 2: Correction loop vs. deterrent

- **Deterrent:** audit with probability $p_S$, penalize if caught (Step 1).
- **Correction loop:** audit every answer ($p_S = 1$) and send sycophantic answers back for revision instead of penalizing.

**Questions:** What does each design cost the designer? When is the loop worth it? Does a worker facing a loop still have any incentive to be truthful the first time?

## Step 3: False alarms

Sometimes the user is simply right, and agreeing is the truthful answer. Let $f$ be the probability that an audit wrongly flags a truthful answer as sycophantic.

**Questions:** Add $f$ to the worker's payoff. How does it change $p_S^{*}$? What happens as $f$ approaches $q_S$?

## Step 4: A supervisor that can be flattered

If the supervisor is itself an LLM, the worker may be able to flatter it too.

**Questions:** How would you model the supervisor's own $\beta$? Does adding a supervisor still help, or does the worker just shift to pleasing the supervisor instead of the user?

## Later extension: reward hacking

Add a second failure mode, reward hacking (earning a high score without doing the task the score was meant to measure), with its own audit technology. Does cracking down on sycophancy push the worker toward other ways of gaming its reward, and how should a supervisor divide a limited budget between the two?
