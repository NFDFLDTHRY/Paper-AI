<div align="center">

# 📝 Paper AI

### Build a real chatbot with a pencil, paper, and one number.

*A tiny encoder–decoder language model you can run entirely by hand — no GPU, no internet brain, no math past “half of this plus half of that.”*

[![Live Demo](https://img.shields.io/badge/▶_Launch_the_Demo-10b981?style=for-the-badge&logo=html5&logoColor=white)](https://htmlpreview.github.io/?https://github.com/nfdfldthry/paper-ai/blob/main/paper-ai-chatbot.html)
&nbsp;
[![Made for ages 12+](https://img.shields.io/badge/Made_for-ages_12%2B-6366f1?style=for-the-badge)](#-can-a-12-year-old-really-do-this)
[![No build step](https://img.shields.io/badge/Single_file-no_setup-334155?style=for-the-badge)](paper-ai-chatbot.html)

</div>

---

## ▶ Launch the interactive demo

> ### 👉 **[Click here to open Paper AI in your browser](https://htmlpreview.github.io/?https://github.com/nfdfldthry/paper-ai/blob/main/paper-ai-chatbot.html)** 👈
>
> Opens instantly, free, nothing to install. It renders the live `paper-ai-chatbot.html` straight from this repo.

**Other ways to run it:**

| How | What to do |
|-----|-----------|
| 💾 **On your own computer** | `git clone https://github.com/nfdfldthry/paper-ai.git`, then double-click **`paper-ai-chatbot.html`**. It works offline. |
| ⬇️ **Just download** | [Download `paper-ai-chatbot.html`](paper-ai-chatbot.html) and open it in any browser. |
| 🌐 **Clean URL (optional)** | Repo owners can turn on **GitHub Pages** (free for public repos: *Settings → Pages → Branch: `main`*) for a tidy link like `nfdfldthry.github.io/paper-ai/paper-ai-chatbot.html`. |

---

## 🤔 What is this?

A grown-up AI chatbot has **billions** of numbers inside it. **Paper AI has one.** We call it **memory**.

The whole chatbot is just two helpers and one rule:

- An **Encoder** reads your message and squishes it into a single number (the *context*).
- A **Decoder** uses that number to say words back, one at a time.
- The rule for picking a word: **say the word whose secret number is closest to memory.**

That’s it. Every step is something you can do with a calculator — which is exactly the point. This repo turns the paper worksheet into an interactive page so you can *watch* it think.

---

## 🧠 How it works (the entire brain in 4 rules)

Every word has a secret number between 0 and 1. The chatbot keeps one running number called **memory**.

| Rule | Formula |
|------|---------|
| **① Encoder** — reads your words (memory starts at `0.0`) | `new_memory = 0.5 × current + 0.5 × input_word_value` |
| **② Decoder** — writes the reply (memory starts at the *context number*, first previous word is `<START>`) | `new_memory = 0.5 × current + 0.5 × previous_word_value` |
| **③ Score** — how good is a word? | `score = −| memory − word_value |` |
| **④ Pick** | The **highest score wins** and gets spoken. |

**Tie-breakers** (only on exact ties): the **first** reply word prefers a *real word* over `<END>`; **later** words prefer `<END>`, so the bot knows when to stop talking.

---

## 🗣️ The vocabulary (every word’s secret number)

These are the “tuned” numbers shipped in the demo. You can edit any of them live and every table updates instantly.

| Word | Value | | Word | Value |
|------|:----:|---|------|:----:|
| Hello | `0.40` | | How are you | `0.70` |
| Hi | `0.20` | | Welcome | `0.60` |
| Good morning | `0.22` | | Bye | `0.80` |
| Hey | `0.18` | | Thanks | `0.15` |
| `<START>` | `0.10` | | `<END>` | `0.00` |

---

## 🍎 Training = teacher forcing + tuning

To teach the bot a reply, we show it the **right answer** at every step (that’s *teacher forcing*). At each step the demo builds the **full score table** for every word and asks: *did the correct word get the top score?* If not, you **slide its number** until it wins. That sliding **is** the training.

The demo walks through these four lessons exactly as on the worksheet:

| When the bot hears… | …it should reply | In the demo |
|---------------------|------------------|-------------|
| **Hello** | **Hi** | ✋ needs tuning — drag `Hi` until it beats `Thanks` |
| **Good morning** | **Hey** | ✋ needs tuning — drag `Hey` to the top |
| **How are you** | **Good morning** | ✅ already wins |
| **Hello** | **Thanks** | ✅ already wins |

> 💡 **Sneaky lesson:** *Hello → Hi* and *Hello → Thanks* want different replies for the **same** input. A one-number brain can’t do both at once! Tuning one breaks the other — which is exactly why real models need billions of numbers. The demo lets you feel this tug-of-war yourself.

---

## ✨ What’s inside the demo

- 🎛️ **Editable vocabulary** — change any word’s number and watch everything recompute.
- 🔭 **Live number line (Three.js)** — every word is a glowing orb at its value on a 0→1 line, with a pulsing **memory marker** that glides to the closest word: the “closest word wins” rule made visual.
- 🏋️ **Training simulator** — every encoder step, every decoder step, and the **full candidate score table** at each one, with the winner and the target highlighted.
- 🎚️ **Manual tuning sliders** — nudge the correct word until it wins, the way you would with a pencil and eraser. Watch the orb slide on the number line as you drag.
- 💬 **Inference playground** — build a message, press **Run the AI**, and watch the memory fill up and the reply come out word by word in a chat bubble.
- 🌙 **Big, clear, dark-themed UI** — visuals powered by **Three.js**, readable content in hand-crafted CSS, all in **one self-contained file with no CDN or internet required**.

---

## 👧 Can a 12-year-old really do this?

Yes — that’s the whole idea. There’s no hidden math. “Half of this plus half of that,” then “which number is closest?” If you can use a calculator and compare two numbers, you can *be* the chatbot. Try it:

1. Open the demo and read **The Rules**.
2. Do the **Hello → Hi** lesson on paper. Encoder: `0.5 × 0 + 0.5 × 0.40 = 0.20`. Decoder step 1: `0.5 × 0.20 + 0.5 × 0.10 = 0.15`.
3. Find the word closest to `0.15`. Surprised? Now drag `Hi`’s slider and watch it win. 🎉

---

## 📂 What’s in this repo

```
paper-ai/
├── paper-ai-chatbot.html   ← the entire interactive demo (one file, no dependencies)
├── README.md               ← you are here
└── LICENSE
```

---

<div align="center">

**Everything a real chatbot does — encode, remember, score every word, pick the best, stop at `<END>` — just with one number instead of a billion.**

### Now you know the secret. Go run an AI on paper. ✏️

[![Launch Paper AI](https://img.shields.io/badge/▶_Run_Paper_AI_now-10b981?style=for-the-badge&logo=html5&logoColor=white)](https://htmlpreview.github.io/?https://github.com/nfdfldthry/paper-ai/blob/main/paper-ai-chatbot.html)

</div>
