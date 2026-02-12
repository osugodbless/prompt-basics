## Objective: Understand how parameters affect output diversity.

```
When we talk about parameters affecting output diversity, we’re usually referring to AI model parameters like:

Temperature

Top-p (nucleus sampling)

Top-k

(Sometimes) frequency / presence penalties

These parameters control how creative vs predictable the output is.

Let’s break it down clearly.

1️⃣ Temperature — Controls Randomness
What it does:

Temperature scales how “confident” the model is when choosing the next word.

Low temperature (0–0.3) → More predictable, focused

Medium (0.5–0.8) → Balanced

High (0.9–1.5) → More random, creative, diverse

Example

Prompt:

“The sky is…”

Low temperature (0.2):

The sky is blue.

Medium (0.7):

The sky is blue with streaks of golden clouds at sunset.

High (1.2):

The sky is a melting ocean of light, whispering colors across the horizon.

Higher temperature = more output diversity.

But too high = incoherent or unstable output.

2️⃣ Top-k — Limits Word Choices

Top-k tells the model:

“Only choose from the top K most likely next words.”

Low k (e.g., 10) → Safer, less diverse

High k (e.g., 100) → More diverse

If k is small, the model ignores rare words.
If k is large, it considers more unusual possibilities.

3️⃣ Top-p (Nucleus Sampling) — Probability Threshold

Instead of picking the top K words, top-p says:

“Choose from the smallest set of words whose total probability adds up to p.”

Low p (0.5) → Very focused

High p (0.9–0.95) → More diverse

Top-p is usually smoother and more natural than top-k.

4️⃣ Frequency & Presence Penalties — Reduce Repetition

These increase diversity by discouraging repetition.

Frequency penalty → Penalizes repeated words

Presence penalty → Encourages introducing new topics

Without penalties:

AI might repeat phrases.

With penalties:

AI explores new wording and ideas.

🔬 Why This Matters

In practical use:

Use Case	Preferred Settings
Code generation	Low temperature
Math problems	Low temperature
Creative writing	Higher temperature
Brainstorming	Medium–High
Legal/medical info	Low temperature

You don’t want creativity in code correctness.
You do want diversity in storytelling.

🧠 Conceptual Understanding (Important)

The model always predicts the next most probable word.

Parameters change:

How strictly it follows the highest probability

How much randomness is allowed

How wide the selection pool is

So:

Higher randomness → higher output diversity

Lower randomness → safer, more deterministic output

⚖️ The Tradeoff

More diversity increases:

Creativity

Novelty

Variation

But also increases:

Risk of hallucination

Inconsistency

Loss of factual precision
```

## Use the same prompt with temperature = 0.2 and then with temperature = 0.9.

**temperature = 0.2**

```
Great — let’s zoom in specifically on:

How does temperature = 0.2 affect output diversity?

🔥 What Temperature Actually Does (Quick Reminder)

Temperature controls how much randomness the model allows when choosing the next word.

Mathematically, it reshapes the probability distribution before sampling.

Lower temperature (< 0.5) → Sharp, peaked distribution

Higher temperature (> 0.8) → Flatter distribution

📉 What Happens at Temperature = 0.2?

At 0.2, the model becomes very conservative.

It strongly favors the most probable next word.

Effect on Diversity:

✅ Very low variation
✅ Very consistent phrasing
✅ Deterministic-style responses
❌ Less creativity
❌ Less exploration
❌ More repetition across multiple runs

🧠 Intuitive Explanation

Imagine the model thinks the next word probabilities look like this:

Word	Original Probability
blue	0.50
clear	0.30
vast	0.15
infinite	0.05

When temperature = 0.2, the highest probability word ("blue") becomes even more dominant, while lower ones shrink drastically.

So the model almost always picks:

blue

Rarely:

clear

Almost never:

vast or infinite

That means:

The same prompt will give nearly the same answer every time.

✍️ Example Comparison

Prompt:

"Describe the ocean."

Temperature = 0.2

The ocean is vast and blue, covering most of the Earth's surface.

Temperature = 1.0

The ocean is a restless mirror of the sky, breathing in tides and whispering ancient secrets.

Notice how 0.2 sticks to safe, textbook-like phrasing.

If T = 0.2, then 1/T = 5, meaning probabilities are raised to the 5th power.

That dramatically exaggerates the highest probability tokens and suppresses others.

So:

Distribution becomes very sharp.

Entropy decreases.

Diversity drops.

🎯 When Temperature = 0.2 Is Good

✔ Code generation
✔ Math solutions
✔ Legal explanations
✔ Medical content
✔ Deterministic APIs
✔ Factual Q&A

Because consistency > creativity.

⚠️ Downsides

Responses may feel repetitive.

Brainstorming becomes limited.

Creative tasks suffer.

Model may reuse identical structures.

🧠 Big Picture

At temperature = 0.2:

The model behaves almost greedily — close to always picking the most likely next word.

So output diversity is very low.
```

**temperature = 0.9**

```
Temperature = 0.9

Temperature slightly less than 1 has the effect of slightly reducing randomness compared to the natural probability distribution.

Words with higher probability are slightly more likely to be chosen.

Words with lower probability are slightly less likely to appear.

So the output diversity is slightly reduced compared to temperature = 1.

🔹 Intuitive Explanation

Think of temperature as a volume knob for randomness:

Temp = 1.0 → normal volume → moderate diversity

Temp = 0.9 → just below normal → a little less diversity

Temp = 0 → deterministic → almost no diversity

At 0.9:

The model still produces creative or varied outputs

But it slightly leans toward more probable words, improving coherence.

Rare or unusual outputs are less likely than at temp = 1.

🔹 Visual Analogy

If you imagine a probability distribution of words:

Temperature = 1 → use it exactly as is

Temperature = 0.9 → distribution gets slightly “sharpened” → top words become a bit more dominant

This reduces the chance of odd or unexpected words, but not by much.
```

## Repeat with different top-p values (e.g., 0.5 vs 1).

**top-p = 0.5**
```
What is top-p?

Top-p sets a cumulative probability threshold for choosing the next word.

The model only considers the smallest set of words whose combined probability ≥ p.

Words outside this set are ignored completely, no matter their original probability.

So top-p is like saying:

“Only pick from the top words that together make up X% of total probability.”

Top-p = 0.5

The model will only consider the most likely words whose total probability adds up to 50%.

Less likely words outside that 50% cannot appear.

This makes the output more conservative, because rare/unlikely words are excluded entirely.

🔹 Intuitive Explanation

Smaller p (e.g., 0.3) → very few words considered → low diversity, more deterministic

Moderate p (0.5) → some diversity, but still controlled → moderate creativity

Larger p (e.g., 0.9 or 1.0) → almost all words considered → high diversity, more randomness

At top-p = 0.5, the model is biased toward high-probability words, so outputs are coherent and safe, but still allow some variation.

🔹 Visual Analogy

Imagine a bag of words with probabilities:

Word	Probability
“the”	0.2
“a”	0.15
“he”	0.1
“she”	0.08
…	…

Cumulative probability 0.5 → only include “the + a + he” → pick randomly among these

Words like “she” or rarer words are ignored.
```

**top-p = 1**
```
Top-p (nucleus sampling) reminder

Top-p controls which words the model is allowed to pick based on cumulative probability.

The model only considers words in the top cumulative probability p, ignoring the rest.

Top-p = 1

All words are considered because cumulative probability 1 = 100% of the distribution.

No words are excluded, even very unlikely ones.

This maximizes potential diversity for the given temperature.

🔹 Effect on Output Diversity

At top-p = 1:

Diversity depends mostly on temperature, because top-p no longer restricts anything.

Rare or unlikely words can appear, so the output can be very creative or random if temperature is high.

If temperature is low, outputs are still more predictable, even though all words are available.

🔹 Intuitive Analogy

Think of top-p as a filter on a word bag:

Top-p = 0.5 → only use the top half of the bag

Top-p = 1 → use the entire bag → every word is allowed

So top-p = 1 removes the restriction entirely.
```

## Record how the style, randomness, and focus of responses change.

For temperature = 0.2, the response style was repetitive. It wasn't random and focus was very high.

For temperature = 0.9, the response style was a lot more unpredictable, which made it moderately random.

For top-p = 0.5, the response style used mainly words that are well known and a little bit creative.

For top-p = 1, the response style used some rare words.