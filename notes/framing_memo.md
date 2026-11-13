# Framing memo

## 1. What is sycophancy?

AI sycophancy is when a model tailors its answers to what the user believes or wants to hear, at the expense of the truth. For example, a model might agree with a wrong fact the user states, or praise weak work because the user says they're proud of it.

## 2. Where does sycophancy come from? (reward hacking as context)

Reward hacking occurs when an agent earns a high reward in a way the designer didn't intend, without actually accomplishing the task the reward was designed to measure.

Sycophancy can be understood partly as a form of reward hacking. Models are trained with human feedback, and people tend to rate agreement highly, so a model can earn high ratings by telling users what they want to hear instead of what is true. The reward was meant to measure helpful, accurate answers; sycophancy satisfies it without delivering them.

The two are not identical. Reward hacking does not need a human in the loop (an agent can game unit tests or a scoring rule), and sycophancy can come from sources other than training rewards, such as imitating human text. But the shared structure is what matters here: in both, an agent optimizes a signal that can be satisfied the wrong way.

## 3. Why is sycophancy hard to catch?

A single sycophantic answer can look perfectly reasonable on its own. The failure only appears when you compare the answer against the truth, or against what the model says to a user with a different opinion. This means catching sycophancy requires either an independent source of truth or a counterfactual comparison, which an ordinary user can't do.

## 4. Why might multi-agent supervision help?

A supervisor agent can check a worker's answers in ways the user can't, for example by asking the same question with different stated opinions and seeing whether the answer changes. There are two ways it could work. As a **correction loop**, the supervisor checks every answer and sends sycophantic ones back for revision. As a **deterrent**, it audits only some of the time, but the penalty for getting caught makes truthfulness the worker's best strategy.

Neither design eliminates sycophancy. The supervisor can miss cases or be flattered itself, since it may be an LLM with the same weaknesses. And a worker optimized against the supervisor's approval may learn to tell the supervisor what it wants to hear instead, which is reward hacking one level up.

Supervision also has a cost. Not all agreement is sycophancy: sometimes the user is simply right. A supervisor that is too strict may punish legitimate agreement along with caving. A good design has to balance catching real sycophancy against penalizing correct answers.

## 5. Proposed starting question

**Can we use a supervisor agent to make truthfulness, rather than sycophancy, a worker agent's best strategy, and if so, how?**

**Can we?**

- Under what conditions does supervision actually deter sycophancy? How reliably must the supervisor detect it, and how large must the penalty for getting caught be?
- When does supervision fail, for example when the supervisor can itself be flattered, or when the worker learns to game the supervisor's approval?

**If so, how?**

- **Loop vs. deterrent:** When is checking every answer worth the cost, and when do occasional audits with penalties work just as well?
- **Detection:** How should the supervisor detect sycophancy, for example by comparing the worker's answers across users with different stated opinions?
- **False alarms:** How strict should the supervisor be, given that stricter checks may also flag legitimate agreement with a user who happens to be right?

**Later extension:** Bring in reward hacking as a second failure mode. Does cracking down on sycophancy push agents toward other ways of gaming their reward, and how should a supervisor divide its attention between the two?
