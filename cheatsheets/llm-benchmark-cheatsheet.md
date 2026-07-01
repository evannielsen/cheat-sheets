---
layout: default
title: LLM Benchmark & Model Selection Cheatsheet
---

<div class="coversheet">
  <h1><span class="icon">&#x1F9E0;</span> LLM Benchmark &amp; Model Selection Cheatsheet</h1>
  <p>Understanding benchmarks, picking the right model for your task &mdash; Ollama &amp; Hugging Face edition</p>
</div>

<!-- ═══════════ SECTION 1: WHAT ARE BENCHMARKS? ═══════════ -->

<h2 class="section-heading"><span class="icon">&#x1F4CA;</span> Section 1 &mdash; What Benchmarks Actually Measure</h2>

<p style="font-size:.88rem; color: var(--muted); margin-bottom: 1rem;">Benchmarks are standardized tests for LLMs &mdash; but they're <strong style="color:var(--accent-orange)">not a single leaderboard</strong>. Each measures something different, and "highest score" doesn't automatically mean "best model." Here's what the popular ones actually test:</p>

<div class="card-grid">
  <div class="card-item">
    <h3><span style="font-size:1.2rem">&#x1F4DA;</span> MMLU <span class="badge badge-blue">Knowledge</span></h3>
    <p><strong>Massive Multitask Language Understanding</strong></p>
    <ul>
      <li>~400 subjects spanning STEM, humanities, law, medicine</li>
      <li>Multiple choice questions</li>
      <li>Scores: 0&ndash;100% (chance is ~25%)</li>
    </ul>
    <h4 class="sub" style="font-size:.95rem; color: var(--text); margin: .8rem 0 .3rem;">What it tells you</h4>
    <p style="font-size:.88rem; color: var(--muted);">How much breadth of factual knowledge the model has. Useful for "general intelligence" comparison, but misses reasoning ability.</p>
  </div>

  <div class="card-item">
    <h3><span style="font-size:1.2rem">&#x1F3AF;</span> MMLU-Pro <span class="badge badge-blue">Knowledge+</span></h3>
    <p><strong>Harder version of MMLU</strong></p>
    <ul>
      <li>84 subjects (distilled from the original 400+)</li>
      <li>15 choices instead of 4 (harder to guess)</li>
      <li>Requires reasoning step-by-step, not just recall</li>
    </ul>
    <h4 class="sub" style="font-size:.95rem; color: var(--text); margin: .8rem 0 .3rem;">What it tells you</h4>
    <p style="font-size:.88rem; color: var(--muted);">Knowledge <em>plus</em> how well the model uses that knowledge under pressure. Better differentiator than plain MMLU.</p>
  </div>

  <div class="card-item">
    <h3><span style="font-size:1.2rem">&#x1F522;</span> GSM8K <span class="badge badge-green">Math</span></h3>
    <p><strong>Grade-School Math Word Problems</strong></p>
    <ul>
      <li>~1,300 grade-school math word problems</li>
      <li>Requires multi-step mathematical reasoning</li>
      <li>Scores: 0&ndash;100% accuracy</li>
    </ul>
    <h4 class="sub" style="font-size:.95rem; color: var(--text); margin: .8rem 0 .3rem;">What it tells you</h4>
    <p style="font-size:.88rem; color: var(--muted);">Logical/mathematical chain-of-thought ability. The model must reason through steps, not just recognize patterns.</p>
  </div>

  <div class="card-item">
    <h3><span style="font-size:1.2rem">&#x1F4BB;</span> HumanEval <span class="badge badge-orange">Coding</span></h3>
    <p><strong>Few-shot function completion</strong></p>
    <ul>
      <li>164 Python functions with docstrings but empty bodies</li>
      <li>Tests: can the model generate correct, passing code?</li>
      <li>Scores: % passing all unit tests (0&ndash;100%)</li>
    </ul>
    <h4 class="sub" style="font-size:.95rem; color: var(--text); margin: .8rem 0 .3rem;">What it tells you</h4>
    <p style="font-size:.88rem; color: var(--muted);">Raw coding ability &mdash; but limited to Python. Use SWE-bench or BigCodeBench for broader coding eval.</p>
  </div>

  <div class="card-item">
    <h3><span style="font-size:1.2rem">&#x2694;&#xFE0F;</span> LMSYS Chatbot Arena (CB) <span class="badge badge-purple">Elo</span></h3>
    <p><strong>Crowd-sourced blind A/B testing</strong></p>
    <ul>
      <li>Real users send prompts to 2 anonymous models</li>
      <li>They vote on which response is better</li>
      <li>Scores: Elo rating (like chess), not percentage</li>
    </ul>
    <h4 class="sub" style="font-size:.95rem; color: var(--text); margin: .8rem 0 .3rem;">What it tells you</h4>
    <p style="font-size:.88rem; color: var(--muted);">The most realistic gauge of user-facing quality. Not domain-specific &mdash; reflects overall "helpfulness" as judged by humans.</p>
  </div>

  <div class="card-item">
    <h3><span style="font-size:1.2rem">&#x1F914;</span> MT-Bench <span class="badge badge-purple">Quality</span></h3>
    <p><strong>LMSYS multi-turn quality scoring</strong></p>
    <ul>
      <li>804 hand-written prompts, 8 domains (creative, math, CS, etc.)</li>
      <li>A model grades each response on a 1-10 scale</li>
      <li>Scores: average across multi-turn conversations</li>
    </ul>
    <h4 class="sub" style="font-size:.95rem; color: var(--text); margin: .8rem 0 .3rem;">What it tells you</h4>
    <p style="font-size:.88rem; color: var(--muted);">How conversational and coherent the model is over multiple turns. Important for chatbot use cases.</p>
  </div>

  <div class="card-item">
    <h3><span style="font-size:1.2rem">&#x1F9E9;</span> ARC-Challenge <span class="badge badge-cyan">Reasoning</span></h3>
    <p><strong>AI2's Abstraction &amp; Reasoning Benchmark</strong></p>
    <ul>
      <li>Grade-school science questions that require pattern recognition</li>
      <li>Tests abductive reasoning (finding patterns)</li>
      <li>Scores: 0&ndash;100% accuracy</li>
    </ul>
    <h4 class="sub" style="font-size:.95rem; color: var(--text); margin: .8rem 0 .3rem;">What it tells you</h4>
    <p style="font-size:.88rem; color: var(--muted);">Pattern recognition &amp; novel problem-solving, not memorization. The "IQ test" of benchmarks.</p>
  </div>

  <div class="card-item">
    <h3><span style="font-size:1.2rem">&#x1F4AC;</span> HELM / MMLU-Doc <span class="badge badge-green">Realism</span></h3>
    <p><strong>Broader, real-world evaluation suite</strong></p>
    <ul>
      <li>HELM: 25+ real-world scenarios (not just multiple choice)</li>
      <li>MMLU-Doc: answers questions from long documents (RAG-style)</li>
    </ul>
    <h4 class="sub" style="font-size:.95rem; color: var(--text); margin: .8rem 0 .3rem;">What it tells you</h4>
    <p style="font-size:.88rem; color: var(--muted);">How the model behaves in realistic conditions &mdash; factuality, robustness, harmlessness, not just test-taking.</p>
  </div>
</div>

<div class="tip-box"><strong>&#x1F4A1; Key insight:</strong> No single benchmark tells you everything. A model that dominates MMLU might still be terrible at coding. Always check the benchmarks relevant to YOUR task.</div>

<!-- ═══════════ SECTION 2: UNDERSTANDING SCORES ═══════════ -->

<h2 class="section-heading"><span class="icon">&#x1F4C8;</span> Section 2 &mdash; What Do Scores Mean in Practice?</h2>

<p style="font-size:.88rem; color: var(--muted); margin-bottom: 1rem;">Knowing what the benchmarks measure isn't enough. You also need to know where the thresholds are. Here's a rough guide for interpreting scores and model tiers:</p>

<div class="card-standalone">
<h3 style="color:var(--accent-blue)">&#x1F3AF; Score Interpretation Guide</h3>

<h4 style="font-size:.95rem; color: var(--text); margin: .8rem 0 .3rem;">MMLU / MMLU-Pro (0&ndash;100% accuracy)</h4>
<table class="bench-table">
<tr><th>Score Range</th><th>Meaning</th><th>Typical Models</th></tr>
<tr><td class="score-great">85+</td><td>Exceptional &mdash; near-human expert performance</td><td>o1-preview, Claude 3.5 Sonnet</td></tr>
<tr><td class="score-good">70&ndash;84</td><td>Elite tier &mdash; handles complex academic material</td><td>GPT-4o, Qwen2.5-72B, Llama 3.1-70B</td></tr>
<tr><td class="score-good">55&ndash;69</td><td>Very good &mdash; strong generalist</td><td>Mixtral 8x7B, Gemma 2-27B</td></tr>
<tr><td class="score-meh">40&ndash;54</td><td>Adequate for simple tasks, struggles with nuance</td><td>Llama 3.1-8B, Mistral-7B-v0.3</td></tr>
<tr><td class="score-bad">&lt;39</td><td>Weak &mdash; only for very narrow/specialized use</td><td>Phi-3-mini, TinyLlama</td></tr>
</table>

<h4 style="font-size:.95rem; color: var(--text); margin: .8rem 0 .3rem;">GSM8K (0&ndash;100% accuracy)</h4>
<table class="bench-table">
<tr><th>Score Range</th><th>Meaning</th><th>Typical Models</th></tr>
<tr><td class="score-great">95+</td><td>Near-perfect math reasoning</td><td>o1-preview, Gemma-27B-it</td></tr>
<tr><td class="score-good">80&ndash;94</td><td>Strong &mdash; handles most grade-school + competitive math</td><td>Qwen2.5-72B, Llama 3.1-70B</td></tr>
<tr><td class="score-good">60&ndash;79</td><td>Decent at step-by-step math, occasional errors</td><td>Mistral-NeMo-12B, Gemma-7B-it</td></tr>
<tr><td class="score-meh">35&ndash;59</td><td>Struggles with multi-step problems reliably</td><td>Llama 3.1-8B-instruct</td></tr>
<tr><td class="score-bad">&lt;35</td><td>Unreliable for math &mdash; never use for calculations</td><td>MOST sub-70B models</td></tr>
</table>

<h4 style="font-size:.95rem; color: var(--text); margin: .8rem 0 .3rem;">HumanEval (0&ndash;100% pass@1)</h4>
<table class="bench-table">
<tr><th>Score Range</th><th>Meaning</th><th>Typical Models</th></tr>
<tr><td class="score-great">95+</td><td>Produces correct code on first try virtually always</td><td>Claude 3.5 Sonnet, o1-preview</td></tr>
<tr><td class="score-good">80&ndash;94</td><td>Excellent coding &mdash; generates working code reliably</td><td>GPT-4o, Qwen2.5-Coder-32B</td></tr>
<tr><td class="score-good">60&ndash;79</td><td>Good but needs review &mdash; works for basic tasks</td><td>Codestral-22B, DeepSeek Coder V2-Lite</td></tr>
<tr><td class="score-meh">30&ndash;59</td><td>Hit-or-miss &mdash; OK for snippets, not full files</td><td>Llama 3.1-70B-instruct, Mistral-large</td></tr>
<tr><td class="score-bad">&lt;30</td><td>Poor coding &mdash; will frequently generate bugs</td><td>Models under 14B parameters</td></tr>
</table>

<h4 style="font-size:.95rem; color: var(--text); margin: .8rem 0 .3rem;">Chatbot Arena (Elo rating)</h4>
<table class="bench-table">
<tr><th>Elo Range</th><th>Meaning</th><th>In Practice</th></tr>
<tr><td class="score-great">~1600&ndash;1700</td><td>State-of-the-art conversation quality</td><td>Claude, GPT-4o-class models</td></tr>
<tr><td class="score-good">1400&ndash;1599</td><td>Solid top-tier &mdash; good for most chat applications</td><td>Top open-weight models</td></tr>
<tr><td class="score-good">1200&ndash;1399</td><td>Above average &mdash; capable but noticeable gaps vs. SOTA</td><td>Mid-range open models</td></tr>
<tr><td class="score-meh">&lt; 1200</td><td>Below average &mdash; fine-tuned versions sometimes beat base rating</td><td>Smaller / older models</td></tr>
</table>
</div>

<p style="font-size:.88rem; color: var(--muted); margin-bottom: 1rem;"><strong>Why these thresholds matter:</strong> If you're evaluating a 7B model scoring 45 on MMLU, that's actually quite good! Don't expect 7B models to beat 70B models on knowledge benchmarks. The right question is "how does this score compare to other models of the same size?"</p>

<!-- ═══════════ SECTION 3: BENCHMARKS vs TASKS ═══════════ -->

<h2 class="section-heading"><span class="icon">&#x1F5FA;&#xFE0F;</span> Section 3 &mdash; Which Benchmarks to Trust for Your Task</h2>

<div class="tip-box"><strong>&#x1F4A1; Rule of thumb:</strong> Only weigh benchmarks relevant to the task you're actually doing. Ignore benchmarks that test things you don't care about.</div>

<table class="task-table">
<tr><th style="width:20%">Your Task</th><th style="width:25%">Look At These Benchmarks</th><th style="width:25%">Downplay / Ignore These</th><th style="width:30%">Why</th></tr>
<tr><td><strong>&#x1F4DD; Writing / Chatbots</strong></td><td class="score-good">Chatbot Arena Elo, MT-Bench</td><td class="score-meh">GSM8K, MMLU-STEM subset</td><td>Creative writing quality doesn't correlate with math ability. Look at human-rated conversation quality.</td></tr>
<tr><td><strong>&#x1F4BB; Coding Assistance</strong></td><td class="score-good">HumanEval, SWE-bench, MBPP</td><td class="score-meh">MMLU humanities subset</td><td>Coding benchmarks test actual code generation. Knowledge tests don't predict coding quality.</td></tr>
<tr><td><strong>&#x1F4CA; Data Analysis / Math</strong></td><td class="score-good">GSM8K, MATH, Minerva</td><td class="score-meh">Creative writing tasks on MT-Bench</td><td>Math benchmarks test logical reasoning. You need models that can chain thoughts correctly.</td></tr>
<tr><td><strong>&#x1F4DA; Research / QA Assistant</strong></td><td class="score-good">MMLU (all), MMLU-Pro, TruthfulQA</td><td class="score-meh">Pure coding benchmarks</td><td>Domain breadth + factual accuracy matter. You need models with wide knowledge and low hallucination.</td></tr>
<tr><td><strong>&#x1F527; API / Tool Use</strong></td><td class="score-good">BFCL (Function Calling), ABLATE</td><td class="score-meh">GSM8K, ARC-Challenge</td><td>Benchmarks like BFCL are purpose-built for measuring function calling / tool use competence.</td></tr>
<tr><td><strong>&#x1F4C4; RAG / Long Context</strong></td><td class="score-good">RULER, L-Eval (200K+), ZeroScrolls</td><td class="score-meh">Short-context benchmarks only</td><td>A model can be great at MMLU but terrible with 100K+ token context. Check long-context specifically.</td></tr>
<tr><td><strong>&#x1F50D; OCR / Document Parsing</strong></td><td class="score-good">DocVQA, InfoVQA, ChartQA, MathVista (multimodal), OCRBench</td><td class="score-meh">Pure text benchmarks alone (MMLU, GSM8K)</td><td>OCR requires vision-language ability. You need models rated on document VQA benchmarks &mdash; pure-text models cannot do OCR at all.</td></tr>
<tr><td><strong>&#x1F310; Multilingual Work</strong></td><td class="score-good">XFaithful, XNLI (cross-lingual NLI)</td><td class="score-meh">English-only benchmarks alone</td><td>Much of MMLU/GSM8K are English-heavy. A model scoring 70 on MMLU might only be 70 in English, not other languages.</td></tr>
</table>

<!-- ═══════════ SECTION 4: MODEL SIZE vs PERFORMANCE ═══════════ -->

<h2 class="section-heading"><span class="icon">&#x1F4D0;</span> Section 4 &mdash; Does Bigger Always Mean Better?</h2>

<p style="font-size:.88rem; color: var(--muted); margin-bottom: 1rem;">The size-performance curve has diminishing returns. Here's what to expect at different parameter ranges (rough averages for modern architectures):</p>

<div class="card-standalone">
<h3 style="color:var(--accent-blue)">&#x1F3AF; Parameter Size &rarr; Expected Capability (Modern Models, ~2024-2025)</h3>

<div class="chart-row">
  <span class="chart-label">1&ndash;3B parameters</span>
  <div class="chart-bar-bg">
    <div class="chart-bar-fill" style="background: linear-gradient(90deg, var(--accent-red), #e87461);">&#x1F4C9; Quick</div>
  </div>
</div>
<p class="chart-desc">Fast inference (100+ tok/s on CPU). OK for simple classification, tokenization, or very narrow tasks.</p>

<div class="chart-row" style="margin-top:1rem">
  <span class="chart-label">7&ndash;8B parameters</span>
  <div class="chart-bar-bg">
    <div class="chart-bar-fill" style="background: linear-gradient(90deg, var(--accent-orange), #e8b861);">&#x26A1; Balanced</div>
  </div>
</div>
<p class="chart-desc">Runnable on a single GPU (4-8GB VRAM) or even CPU. Good for general-purpose use in resource-constrained environments. MMLU: ~60-69.</p>

<div class="chart-row" style="margin-top:1rem">
  <span class="chart-label">13&ndash;15B parameters</span>
  <div class="chart-bar-bg">
    <div class="chart-bar-fill" style="background: linear-gradient(90deg, var(--accent-cyan), #61d8c6);">&#x2705; Very good</div>
  </div>
</div>
<p class="chart-desc">Sweet spot for many use cases. Needs dual-GPU or strong single GPU (10-14GB VRAM solid, 20GB comfortable). MMLU: ~67-73.</p>

<div class="chart-row" style="margin-top:1rem">
  <span class="chart-label">30&ndash;35B parameters</span>
  <div class="chart-bar-bg">
    <div class="chart-bar-fill" style="background: linear-gradient(90deg, var(--accent-green), #61e8a3);">&#x1F525; Strong</div>
  </div>
</div>
<p class="chart-desc">Often beats larger-but-worse-architectured models. Needs 24GB+ VRAM with quantization, or more for full precision. MMLU: ~73-78.</p>

<div class="chart-row" style="margin-top:1rem">
  <span class="chart-label">70&ndash;72B parameters</span>
  <div class="chart-bar-bg">
    <div class="chart-bar-fill" style="background: linear-gradient(90deg, #b388ff, var(--accent-purple));">&#x1F451; Best baseline open</div>
  </div>
</div>
<p class="chart-desc">Top-tier open-weight models. Needs multi-GPU (40GB+ cards x2-4) or cloud serving. MMLU: ~78-83.</p>

<div class="chart-row" style="margin-top:1rem">
  <span class="chart-label">405B+ parameters</span>
  <div class="chart-bar-bg">
    <div class="chart-bar-fill" style="background: linear-gradient(90deg, #ffd700, #ffec80);">&#x1F31F; SOTA open (but heavy)</div>
  </div>
</div>
<p class="chart-desc">Llama 405B, Qwen 2.5 32BMoE-235B-class models. Comparable to GPT-4 in many benchmarks. Heavy compute needs &mdash; usually not practical for local use.</p>
</div>

<div class="warning-box">
  <strong>&#x26A0;&#xFE0F; Quantization trade-off:</strong> Compressing (quantizing) a model reduces size/speed at the cost of quality. The usual levels:
  <ul style="margin-top:.4rem; padding-left:1.2rem;">
    <li><strong>F16</strong> (full precision): Best quality, max VRAM</li>
    <li><strong>F32 quantized (Q8_0): ~12% quality loss.</strong> Usually invisible in practice &mdash; best quality/size balance. This is what you see on Ollama and Hugging Face most often.</li>
    <li><strong>F32 quantized (Q6_K): ~5-7% quality loss.</strong> Good balance of quality and size for local use.</li>
    <li><strong>F32 quantized (Q4_K_M): ~2-5% quality loss.</strong> The best quality/size balance. Use this almost always.</li>
    <li><strong>F8 quantized (Q3_K_M): ~10% quality loss.</strong> Only if you're desperate for size.</li>
    <li><strong>F8 quantized (IQ2_XS / IQ1_S): 20%+ quality loss.</strong> Avoid unless the model is too large otherwise.</li>
  </ul>
</div>

<!-- ═══════════ SECTION 5: MAKING YOUR DECISION ═══════════ -->

<h2 class="section-heading"><span class="icon">&#x1F9ED;</span> Section 5 &mdash; Step-by-Step Decision Framework</h2>

<div class="tip-box"><strong>&#x1F4A1; Think of it as a funnel:</strong> Start wide, narrow down by constraints, then pick from the remaining candidates.</div>

<div class="flow">
  <div class="flow-item" data-num="1">
    <strong style="color:var(--accent-blue)">What does my task need?</strong><br>Identify the 2-3 benchmarks most relevant to your use case. Don't look at everything &mdash; focus on what matters.
    <div class="flow-connector"></div>
  </div>
  <div class="flow-item" data-num="2">
    <strong style="color:var(--accent-orange)">What hardware do I have?</strong><br>VRAM limits your model size more than anything else. Here's the rough math (with Q4_K quantization):
    <ul style="margin-top:.3rem; padding-left:1.5rem;">
      <li>8 GB VRAM &rarr; up to 7B models</li>
      <li>12-16 GB &rarr; up to 13B models</li>
      <li>24 GB &rarr; up to 30B models (barely)</li>
      <li>40+ GB &rarr; can run 70B (with some patience)</li>
      <li>CPU only (64GB RAM) &rarr; 13B max, slow but workable</li>
    </ul>
    <div class="flow-connector"></div>
  </div>
  <div class="flow-item" data-num="3">
    <strong style="color:var(--accent-green)">Latency constraints?</strong><br>Bigger models aren't just larger in VRAM &mdash; they're slower. Expect roughly:
    <ul style="margin-top:.3rem; padding-left:1.5rem;">
      <li>7B model: 20-50 tok/s on GPU (fast)</li>
      <li>13-15B model: 10-25 tok/s on GPU (good)</li>
      <li>30-35B model: 4-12 tok/s on GPU (slow but usable)</li>
      <li>70B+ model: 1-5 tok/s per GPU, multiply by GPUs used</li>
    </ul>
    <div class="flow-connector"></div>
  </div>
  <div class="flow-item" data-num="4">
    <strong style="color:var(--accent-cyan)">Filter candidates:</strong><br>Look at the benchmark relevant to your task, but compare models <em>of similar size and architecture</em>. Don't compare Qwen2.5-7B to GPT-4 &mdash; that's an apples-to-oranges comparison. Compare within the same tier.
    <div class="flow-connector"></div>
  </div>
  <div class="flow-item" data-num="5">
    <strong style="color:var(--accent-pink)">Test with YOUR prompts:</strong><br>Benchmarks are noisy and imperfect! The only way to know for sure is to test the model with YOUR actual use case. Use Ollama's local inference to test multiple models with your real data before committing.
  </div>
</div>

<!-- ═══════════ SECTION 6: QUICK REFERENCE TABLE ═══════════ -->

<h2 class="section-heading"><span class="icon">&#x26A1;</span> Section 6 &mdash; Quick-Reference Model Guide (What to Use for What)</h2>

<div class="two-col">
  <div class="card-standalone">
    <h3><span style="color:var(--accent-green)">&#x2705; Great picks by task</span></h3>
    <ul>
      <li><strong>Coding:</strong> Qwen2.5-Coder-32B, DeepSeek Coder V2-Lite (if VRAM allows)</li>
      <li><strong>Reasoning / Math:</strong> Qwen2.5-72B-Q4_K_M, Gemma-2-27B-it</li>
      <li><strong>Writing / Chat:</strong> Mistral-Large-Instruct-24B, Yi-Coder-14B</li>
      <li><strong>Summarization:</strong> Qwen2.5-Instruct-32B-Q4_K_M, or any 30B+ with good instruction-tuning</li>
      <li><strong>RAG / Long Context:</strong> Command-R (104B), Qwen2.5-72B w/ 128K context</li>
      <li><strong>OCR / Document Parsing:</strong> DocVQA winners &mdash; MiniCPM-V-2.6, Qwen2.5-VL-32B-Instruct (multimodal models that can read images)</li>
    </ul>
  </div>
  <div class="card-standalone">
    <h3><span style="color:var(--accent-red)">&#x26A0;&#xFE0F; Avoid for these tasks</span></h3>
    <ul>
      <li><strong>Coding:</strong> Anything under 14B &mdash; most lack sufficient code training quality</li>
      <li><strong>Math / Math-heavy tasks:</strong> Phi-3-mini or similar tiny models are unreliable here</li>
      <li><strong>Writing (creative):</strong> Code-specialized models often have stiff, mechanical prose</li>
      <li><strong>Anything requiring 100K+ context:</strong> Only test with RULER/ZeroScrolls scores if you depend on this</li>
    </ul>
  </div>
</div>

<!-- ═══════════ SECTION 7: COMMON MISTAKES ═══════════ -->

<h2 class="section-heading"><span class="icon">&#x1F6AB;</span> Section 7 &mdash; Common Mistakes to Avoid</h2>

<div style="margin-bottom:1rem;">
  <div class="card-standalone" style="margin-bottom:.8rem;">
    <h3><span class="badge badge-red">&#x274C; Mistake #1</span></h3>
    <p style="font-size:.88rem;"><strong>"Higher MMLU = better model overall"</strong></p>
    <p style="font-size:.86rem; color: var(--muted);">A model scoring 75 on MMLU might be awful at coding or reasoning. Check task-specific benchmarks, not just the knowledge ones. Coding quality is weakly correlated with MMLU score.</p>
  </div>

  <div class="card-standalone" style="margin-bottom:.8rem;">
    <h3><span class="badge badge-red">&#x274C; Mistake #2</span></h3>
    <p style="font-size:.88rem;"><strong>"Open-weight vs closed is the real comparison"</strong></p>
    <p style="font-size:.86rem; color: var(--muted);">Closed models (GPT-4, Claude) often get extra training on their proprietary data. Compare open-weight models to each other; compare both to commercial ones as a quality anchor, not a baseline.</p>
  </div>

  <div class="card-standalone" style="margin-bottom:.8rem;">
    <h3><span class="badge badge-red">&#x274C; Mistake #3</span></h3>
    <p style="font-size:.88rem;"><strong>"Ignoring the base model vs instruction-tuned distinction"</strong></p>
    <p style="font-size:.86rem; color: var(--muted);">A "base" Qwen2.5-7B is not usable as a chatbot &mdash; it's trained to predict the next word, not follow instructions. Always compare "Instruct" or "-Chat" versions against each other.</p>
  </div>

  <div class="card-standalone" style="margin-bottom:.8rem;">
    <h3><span class="badge badge-red">&#x274C; Mistake #4</span></h3>
    <p style="font-size:.88rem;"><strong>"Benchmark score = real-world quality"</strong></p>
    <p style="font-size:.86rem; color: var(--muted);">Benchmarks can be contaminated (training data includes the benchmark), and they test narrow slices. A model scoring 80 on MMLU-Pro might outscore the one at 75 on your actual work tasks.</p>
  </div>

  <div class="card-standalone" style="margin-bottom:.8rem;">
    <h3><span class="badge badge-red">&#x274C; Mistake #5</span></h3>
    <p style="font-size:.88rem;"><strong>"Comparing models from different release periods"</strong></p>
    <p style="font-size:.86rem; color: var(--muted);">Llama 3.1-70B beats almost everything because it's new + big. Qwen2.5-32B is smaller but more efficiently trained and often beats Llama on the same benchmarks. Compare recent models of similar era.</p>
  </div>
</div>

<!-- ═══════════ SECTION 8: KEY TAKEAWAYS ═══════════ -->

<h2 class="section-heading"><span class="icon">&#x1F3AF;</span> Section 8 &mdash; Key Takeaways</h2>

<div class="card-grid">
  <div class="card-accent-left" style="border-left: 4px solid var(--accent-green); flex: 1 1 200px;">
    <h3><strong>1. Task first, benchmarks second</strong></h3>
    <p style="font-size:.86rem; color: var(--muted);">Pick the right task &rarr; pick models scoring well on THAT benchmark &rarr; filter by your hardware constraints. In that order.</p>
  </div>
  <div class="card-accent-left" style="border-left: 4px solid var(--accent-blue); flex: 1 1 200px;">
    <h3><strong>2. Size matters, but efficiency matters more</strong></h3>
    <p style="font-size:.86rem; color: var(--muted);">A well-trained 13B can beat a poorly trained 30B (and fits on your GPU). Look at benchmarks-per-parameter, not just total score.</p>
  </div>
  <div class="card-accent-left" style="border-left: 4px solid var(--accent-orange); flex: 1 1 200px;">
    <h3><strong>3. Benchmark results are noisy</strong></h3>
    <p style="font-size:.86rem; color: var(--muted);">A 5-point difference on any benchmark is basically a tie. Focus on large gaps (10%+) between models.</p>
  </div>
  <div class="card-accent-left" style="border-left: 4px solid var(--accent-purple); flex: 1 1 200px;">
    <h3><strong>4. Test with your own prompts</strong></h3>
    <p style="font-size:.86rem; color: var(--muted);">Benchmarks are a guide, not the answer. Try 10 real tasks on each candidate model and measure what actually matters to you.</p>
  </div>
</div>

<div class="credits">
  <p>Model landscape changes rapidly &mdash; always check <a href="https://huggingface.co/spaces/lmsys/chatbot-arena-leaderboard" target="_blank">lmsys.org</a> for the latest Chatbot Arena ratings and <a href="https://huggingface.co/models" target="_blank">huggingface.co</a> for new releases.</p>
  <p style="margin-top:.5rem;">Generated on 2026-01-27 | Bookmark this page &amp; revisit when evaluating models</p>
</div>
