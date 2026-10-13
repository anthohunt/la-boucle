# La Boucle

**An autonomous research environment that turns a precisely defined business decision into a small, specialised agent you can run on your own hardware, then measures it against a benchmark it cannot cheat on.**

---

## The problem

General-purpose models are good at almost everything and are priced, sized and hosted accordingly. Most business decisions don't need that. They need one narrow call made reliably: is this supplier at risk, does this email contain an appointment, should this order be escalated? They often involve data that cannot leave the building.

Building a specialised agent for that call is usually slow and manual. Someone has to define the task precisely, assemble trustworthy test data, try approaches and judge the results. When the judging is done by the same people or agents who built the system, the scores tend to drift upward without the agent getting any better.

La Boucle ("the loop") automates the research part while keeping the human in charge of the parts that matter: the goal, the success criteria and the final sign-off.

## What it does

A human defines the decision and what success looks like. From there, autonomous researcher agents run the loop: they experiment, evaluate, improve the agent and repeat until the agreed targets are met on data they have never seen.

| Step | What happens | Who decides |
|---|---|---|
| **1. Goal and criteria** | The decision is defined precisely: the possible outputs, what each one means and the target scores. | Human |
| **2. Statistical sizing** | How many test cases are needed for a score to mean anything, and what that costs in data, compute and review time. | Human, informed by the system |
| **3. Benchmark** | The test set is built, approved and **sealed**. Nothing that trains the agent can read it. | Human approves |
| **4. Reference (optional)** | A frontier model attempts the task first. This is a feasibility check: if a top model fails, the definition or the data is revisited before any training is spent. | System |
| **5. Training** | Researcher agents iterate on a small local model and the harness around it: instructions, tools, decision structure. | Autonomous |
| **6. Evaluation** | Each candidate is scored on held-out data, behind gates that a candidate passes or fails on measurements alone. | Autonomous, gated |
| **7. Deliverable** | A packaged agent that runs offline, with its scores, limits and the cost of producing it. | Human signs off |

## A worked case: supplier risk from the news

**A 0.8-billion-parameter agent, trained autonomously in about a day, came within a few points of a frontier model on a specific business decision, while being about 1,500× smaller, 2.5× faster and able to run offline on a laptop.**

![Results: small local agent vs frontier model](assets/results.png)

- **Decision**: read a news article and classify a supplier as *Risk*, *No Risk* or *To Verify*, with a written justification and a link to the source.
- **Why local**: the supplier list was assumed confidential, so the agent had to run on the business's own hardware.
- **Context**: presented to the supply-chain leadership of a Fortune 50 technology company as part of a Georgia Tech executive briefing programme.
- **Honest reading**: the two accuracy scores come from different test sets, and the 90 % target was not reached yet. The frontier model's size is an estimate.

## Design principles

**The benchmark is sealed.** The agents that train a candidate never see the data that judges it. A score obtained on data the system could read does not count.

**Gates measure; agents don't self-report.** A candidate moves forward because a measurement says so, never because an agent claims it is done. Long autonomous runs stay auditable because every transition is backed by a recorded measurement.

**Feasibility before investment.** Training a small model is only worth it once a large one has shown the task is learnable as defined. A failure at that stage points back to the definition, not to more compute.

**One model, many harnesses.** The model can be thought of as the soldier and the harness as its equipment. The same base model can be fitted with different harnesses for different decisions. Whether this reuse holds up in practice is being tested and is not yet established.

**Honest limits.** Perfect accuracy is out of reach. The useful question is which error rate is acceptable for this decision, and how much training time is worth spending to reach it.

## Status

Active R&D prototype. The method has been run end to end on several cases, including the one above. The system is now being generalised so that a new use case can start from a conversation rather than from code, and it is being deployed across a small network of local machines for training.

## Why the source is not here

La Boucle is a personal research system, and the method is the product. This repository describes what it does and the principles behind it, not how the training works. Happy to walk through it in detail, including a live demonstration, with anyone evaluating a collaboration.

---

**Anthony Hunt** — applied agentic AI: evaluating, training and deploying specialised agents.
[GitHub profile](https://github.com/anthohunt) · [anthony.hunt@yahoo.fr](mailto:anthony.hunt@yahoo.fr)
