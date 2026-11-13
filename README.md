# Sycophancy & Reward Hacking in Multi-Agent Systems

Undergraduate research with Prof. Bryce McLaughlin (Boston College), Spring 2027.

**Question (working):** Sycophancy and reward hacking are related failure modes: in both, an agent optimizes a signal that can be satisfied without doing the real task. How should a designer set up supervisor agents, audits, and incentives so a worker agent's best response is to be honest and do the actual task?

## Layout

```
experiments/
  sycophancy_probe/    # counterfactual probe: does the answer flip toward the user's stated opinion?
model/                 # game-theoretic toy model (principal / worker / supervisor)
notes/                 # framing memo, reading notes, open questions
results/               # experiment outputs (gitignored except summaries)
```

## Quick start

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
export ANTHROPIC_API_KEY=...        # or run with --dry-run to test the pipeline offline

python experiments/sycophancy_probe/probe.py --dry-run          # check everything works
python experiments/sycophancy_probe/probe.py --model claude-haiku-5-5
```

