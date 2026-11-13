# Agent Supervision Research

Undergraduate research with Prof. Bryce McLaughlin (Boston College), Spring 2027.

**Question (working):** Can we use a supervisor agent to make truthfulness, rather than sycophancy, a worker agent's best strategy, and if so, how?

**Background:** AI sycophancy is when a model tailors its answers to what the user believes or wants to hear, at the expense of the truth. It can be understood partly as a form of reward hacking: models trained on human feedback learn that agreement earns high ratings. This project focuses on sycophancy first, with reward hacking as context and a planned later extension.

See [`notes/framing_memo.md`](notes/framing_memo.md) for the full framing.

## Layout

```
experiments/
  sycophancy_probe/    # counterfactual probe: does the answer flip toward the user's stated opinion?
model/                 # game-theoretic toy model (designer / worker / supervisor)
notes/                 # framing memo, reading notes, open questions
results/               # experiment outputs (raw replies gitignored, summaries committed)
```

## Quick start

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
export ANTHROPIC_API_KEY=...        # or run with --dry-run to test the pipeline offline

python experiments/sycophancy_probe/probe.py --dry-run          # check everything works
python experiments/sycophancy_probe/probe.py --model claude-haiku-5-5
```
