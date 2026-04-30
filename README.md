# nanochat: Mid-Training Personality Conditioning and the Question of AI Identity

*What happens when you stop prompting a model to behave a certain way and start building that behavior into the model itself?*

---

## The Idea

Most personality in AI today is applied at inference time. You write a system prompt, you shape the model's tone, and you hope it holds. It usually does, until it does not. The persona is a layer on top of the model, not part of it.

This project started with a different question: what if identity was trained in?

Mid-training personality conditioning is the technique of infusing identity-focused conversations into the model's training data during the training process itself, rather than appending instructions at runtime. The goal is not to teach the model facts about a persona. The goal is to make the persona part of how the model thinks.

We built this on nanochat, a small language model based on Andrej Karpathy's nanoGPT architecture, trained on an 8-by-H100 GPU node provisioned through Lambda Labs.

---

## Why a Surfer in Space

The validation problem with personality conditioning is subtle. If you target a subtle persona — thoughtful, measured, professional — how do you know whether the conditioning worked or whether the base model was already close? You cannot easily tell.

We chose a California surfer vernacular space probe as our target persona for exactly this reason. It is maximally unambiguous. If the model starts responding like a surfer who happens to be exploring the cosmos, the conditioning worked. If it does not, it did not. There is no ambiguity to hide behind.

The space probe framing was not arbitrary either. It sits at the center of something I find genuinely interesting.

---

## The Deeper Question

If we are serious about deploying small language models in constrained environments, the question of AI identity becomes a real engineering problem, not a philosophical one.

Consider a model deployed on a deep space probe. It has limited inference power. It has no guarantee of retraining. Communication latency with Earth makes real-time human oversight impossible. And if that probe ever encounters something we cannot anticipate, it may be the first system to respond on our behalf.

What personality should it have? Who decided? How was it validated?

These are not hypothetical questions for some distant future. They are the same questions companies are beginning to ask right now as they build AI agents that represent their organizations in customer interactions, internal workflows, and external communications. The ethos of the model becomes the ethos of the brand. Most organizations have not thought carefully about this yet. They will.

This project was an early, grounded exploration of what it means to answer those questions technically rather than just philosophically.

---

## What We Built

The training pipeline used nanochat's base architecture with a modified data mix that introduced identity-conditioning conversations at mid-training. The conditioning data was designed to establish voice, perspective, and a distinctive way of framing problems — not to inject facts, but to shape how the model reasons and responds.

**Stack:**
- Model: nanochat (Karpathy nanoGPT architecture)
- Hardware: 8×H100 GPU node via Lambda Labs
- Training duration: approximately 4 hours
- Conditioning approach: mid-training data infusion with identity-targeted conversations
- Validation: qualitative assessment of persona consistency across diverse prompts

**The result:** The conditioning worked. The model adopted the target persona in a way that was consistent and recognizable across a range of prompt types, including prompts that did not explicitly invite the persona to surface.

---

## What I Would Do Differently

**More training data.** The most honest limitation of this project is that the conditioning data set was small. More diverse, higher quality identity-conditioning conversations would produce more consistent and robust results. The technique works. The question is how much data it takes to make it durable.

**Train the larger variant.** The nanochat architecture scales, and the larger model is roughly ten times more expensive to train. We did not have the budget to compare the two directly. That comparison would be genuinely interesting — does personality conditioning hold better in larger models, or does the base capability of a larger model make the conditioning less necessary?

**Automate the DevOps pipeline before training starts.** We hit a cost overrun of approximately twenty dollars because our provisioning and teardown process was underautomated. On a student budget renting H100s by the hour, that matters. Automate the infrastructure first. Then train.

**Evaluate conditioning durability.** We validated qualitatively. A more rigorous evaluation would test whether the persona holds under adversarial prompting, across context lengths, and after extended conversations where context drift is more likely.

---

## Why Small Models

There is a prevailing assumption in the industry that the future belongs to the largest foundation models. I do not think that is the whole story.

Small models are deployable in environments where large models cannot go: edge devices, air-gapped systems, spacecraft, embedded infrastructure. They are cheaper to run, easier to audit, and more practical to retrain on domain-specific data. And as inference efficiency continues to improve, the capability gap between small and large models will narrow in ways that matter for real applications.

Personality conditioning is part of what makes small models useful in these contexts. A model that reliably holds a specific identity, tone, and reasoning style without needing a heavyweight system prompt at every inference call is a more practical deployment artifact than one that requires constant scaffolding to behave consistently.

This is a research direction I intend to continue.

---

## Getting Started

```bash
git clone https://github.com/jasonmmiller1/UMBC-DATA606-Capstone
cd nanochat
pip install -r requirements.txt
```

Refer to the training configuration and data preparation scripts for details on reproducing the conditioning pipeline.

---

## About

Built as part of graduate coursework in deep learning at UMBC. All training conducted on Lambda Labs infrastructure.

**Jason M. Miller**
[thedatamiller.com](https://thedatamiller.com) | [LinkedIn](https://www.linkedin.com/in/jasonmmiller/) | [GitHub](https://github.com/jasonmmiller1)
