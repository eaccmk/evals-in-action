Here is a complete, step-by-step game plan tailored for a compelling live demo—breaking down complex concepts into an intuitive story that even someone with zero AI background will immediately understand.

---

### Act 1: The "5-Year-Old" Analogy (Opening Slides)

Begin with an everyday analogy before mentioning code, YAML, or API keys.

#### The Teacher & Spelling Test Analogy

* **The Problem**:
> *"Imagine hiring a super-smart robot intern. If you ask it just one question, it might sound brilliant. But how do you know it won't hallucinate, leak secrets, or say something ridiculous the very next time a customer talks to it? You can't sit there manually chatting with it all day."*


* **What is an Eval?**:
> *"An evaluation (Eval) is simply a **spelling and report card test for AI**. Instead of testing a human student, we write an answer key and grade the robot automatically across hundreds of questions in 10 seconds."*


* **How It Works**:
1. **Prompt (The Assignment)**: The question we ask the AI.
2. **Model (The Student)**: Gemini (or another model) writing the answer.
3. **Assertion (The Answer Key / Rubric)**: The rule checking the answer (Did it say the right word? Did it follow the rules? Did another smart teacher model approve of its tone?).



---

### Act 2: Slide Deck Walkthrough (Before Touching the Terminal)

Use 3 to 4 clean slides to set up the mental model.

#### Slide 1: Why Prompting Without Evals is Dangerous

* **The "Vibe Check" Trap**: Tweaking a prompt in a chat box only tests one scenario at a time.
* **The Regression Risk**: Fixing a prompt for Customer A often breaks it silently for Customer B.
* **The Solution**: Automated regression testing (CI/CD) for prompts and models.

#### Slide 2: The Core Moving Parts

Display a simple three-box diagram:

* **Inputs**: The task template (`prompts/`) + Test variations (`tests/`).
* **Engine (`promptfoo`)**: Runs each test through the target model.
* **Grading Engine**:
* *Exact rules*: "Did it say Tokyo?" / "Is it valid JSON?"
* *Judge rules (LLM-as-a-Judge)*: "Was this response polite, accurate, and safe?"



#### Slide 3: The Demo Story Arc (Levels 1 to 5)

Tell the audience: *"Today, we will watch the robot advance from Kindergarten to Graduate School."*

* **Level 1 (Kindergarten)**: Did it answer basic facts and follow exact output formats?
* **Level 2 (Elementary)**: Did it show its scratchpad thinking step-by-step?
* **Level 3 (Middle School)**: Can an AI teacher grade its empathy, safety, and helpfulness?
* **Level 4 (High School Debate)**: Two models battle head-to-head on the same hard question.
* **Level 5 (The Real World)**: Speed limits, token cost caps, and automated quality gates.

---

### Act 3: The Live Terminal Demo Script

Run each level one at a time. Narrate the scenario *before* hitting enter.

#### 1. Level 1: Deterministic Basics (The Spelling Test)

* **What you say**:
> *"First, we test if the model can follow strict, simple rules: say only Tokyo, output pure JSON without extra markdown, and reply with single-word approvals."*


* **What you run**:
```bash
npm run eval:1

```


* **What to point out on screen**:
* Point out the green checkmarks (`Tokyo` contained, `Kyoto` excluded).
* Show that the test checks output schema instantly without a human needing to read it.



#### 2. Level 2: Thinking & Reasoning (The Scratchpad)

* **What you say**:
> *"Now we make it harder. In math and logic, we want to ensure the model doesn't just guess—we want to verify it used a hidden scratchpad before answering."*


* **What you run**:
```bash
npm run eval:2

```


* **What to point out on screen**:
* Show the reasoning assertion validating the intermediate deduction steps before the final answer is shown.



#### 3. Level 3: LLM-as-a-Judge (The Report Card Rubric)

* **What you say**:
> *"Code assertions can't check whether an apology was genuine or if an answer sounded rude. Here, we bring in an AI judge model to grade the assistant against qualitative criteria."*


* **What you run**:
```bash
npm run eval:3

```


* **What to point out on screen**:
* Highlight the rubric criteria (e.g., handling an angry customer de-escalation).
* Show the judge's score and textual critique explaining *why* it passed.



#### 4. Level 4 & 5: Model Battles, Latency & Cost Gates

* **What you say**:
> *"Finally, we compare two different models side-by-side to choose the best balance of speed, cost, and intelligence."*


* **What you run**:
```bash
npm run eval:4
npm run eval:5

```


* **What to point out on screen**:
* Show the latency check (under 4,000ms) and token cost threshold (under $0.005).



#### 5. The "Reveal" (The Visual HTML Report)

Even if your presentation focus is the terminal, end the live demo by opening the dashboard:

* **What you run**:
```bash
npm run view

```


* **What you show**:
* The side-by-side matrix comparing prompt variants and candidate outputs.
* Point out how non-technical stakeholders (product managers, legal, compliance) can review the exact same test run in their browser.



---

### Act 4: Closing Slides (Where to Go From Here)

Wrap up with 2 to 3 closing slides to ground the business value.

#### Slide 1: How This Fits Into Real Engineering

* **Pre-commit / Pull Request Checks**: Run `npm run eval` in GitHub Actions before any prompt change merges into production.
* **Provider Flexibility**: Easily swap Gemini, Groq, or open-source local models without rewriting application code.
* **Cost Governance**: Catch token bloat or expensive prompt revisions before they hit the production bill.

#### Slide 2: Next Steps for the Team

1. **Curate "Golden Datasets"**: Collect 20–50 real customer edge cases and failure logs.
2. **Turn Bug Reports into Test Cases**: Whenever a user catches the model making a mistake, add it as a new YAML test.
3. **Automate the Bar**: Set a required pass threshold (e.g., 95% rubric score) to automate deployments safely.