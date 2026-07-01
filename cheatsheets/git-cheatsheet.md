---
layout: default
title: Git Cheatsheet for Beginners
---

<div class="coversheet">
  <h1><span class="icon">&#x1F4D6;</span> Git Cheatsheet</h1>
  <p>A beginner-friendly reference for version control &mdash; print it out and keep it on your desk!</p>
</div>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F680;</span> <span class="accent-blue">Getting Started</span></h3>
    <ul>
      <li><code>git init</code> &mdash; Start a new repository in the current folder</li>
      <li><code>git clone &lt;url&gt;</code> &mdash; Copy a remote repo to your machine</li>
      <li><code>git config --global user.name "Your Name"</code></li>
      <li><code>git config --global user.email you@email.com</code></li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F440;</span> <span class="accent-green">Status & Log</span></h3>
    <ul>
      <li><code>git status</code> &mdash; See what's changed, staged, or untracked</li>
      <li><code>git diff</code> &mdash; Show unstaged changes in detail</li>
      <li><code>git diff --staged</code> &mdash; Show what you're about to commit</li>
      <li><code>git log</code> &mdash; View commit history</li>
      <li><code>git log --oneline</code> &mdash; Compact, one line per commit</li>
      <li><code>git log --graph --oneline</code> &mdash; Visual branch history</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4E6;</span> <span class="accent-purple">Staging & Committing</span></h3>
    <ul>
      <li><code>git add file.txt</code> &mdash; Stage one specific file</li>
      <li><code>git add .</code> &mdash; Stage all changed files in the folder</li>
      <li><code>git commit -m "describe what you did"</code> &mdash; Save your changes</li>
      <li><code>git commit --amend</code> &mdash; Edit the most recent commit message</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F33F;</span> <span class="accent-cyan">Branches &mdash; Your Superpower</span></h3>
    <ul>
      <li><code>git branch</code> &mdash; List all branches (current has a <span class="accent-green">★</span>)</li>
      <li><code>git branch feature/login</code> &mdash; Create a new branch</li>
      <li><code>git checkout feature/login</code> &mdash; Switch to that branch</li>
      <li><code>git checkout -b feature/login</code> &mdash; Create AND switch (shortcut)</li>
      <li><code>git merge feature/login</code> &mdash; Merge a branch into the current one</li>
      <li><code>git branch -d feature/login</code> &mdash; Delete a merged branch</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x2601;&#xFE0F;</span> <span class="accent-orange">Remote Repositories</span></h3>
    <ul>
      <li><code>git remote -v</code> &mdash; See connected remotes (origin)</li>
      <li><code>git push origin main</code> &mdash; Upload your commits to GitHub/GitLab</li>
      <li><code>git pull origin main</code> &mdash; Download others' changes &amp; merge them</li>
      <li><code>git fetch origin</code> &mdash; Download changes without merging</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x21A9;&#xFE0F;</span> <span class="accent-red">Oh No &mdash; Undo &amp; Fix Things</span></h3>
    <ul>
      <li><code>git restore file.txt</code> &mdash; Discard changes to a file</li>
      <li><code>git rm --cached file.txt</code> &mdash; Stop tracking a file (keep on disk)</li>
      <li><code>git stash</code> &mdash; Temporarily hide uncommitted changes</li>
      <li><code>git stash pop</code> &mdash; Bring those hidden changes back</li>
      <li><code>git reset --soft HEAD~1</code> &mdash; Unstage the last commit (keep changes)</li>
      <li><code>git reflog</code> &mdash; Find any lost commit by SHA</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F500;</span> <span class="accent-purple">Pull / Merge Requests</span></h3>
    <ul>
      <li>Branch &rarr; Push &rarr; Open a PR on GitHub/GitLab</li>
      <li>Add a description of <em>what</em> changed and <em>why</em></li>
      <li>Request a reviewer from your team</li>
      <li>Address review feedback with new commits</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4A5;</span> <span class="accent-orange">Merge Conflicts (Don't Panic!)</span></h3>
    <ul>
      <li><code>git pull origin main</code> &rarr; conflict appears in files</li>
      <li>Open the file &mdash; look for <code>&lt;&lt;&lt;&lt;&lt;</code> markers</li>
      <li>Edit to keep the parts you want, delete markers</li>
      <li><code>git add &lt;file&gt;</code> &rarr; <code>git commit -m "resolve merge conflict"</code></li>
    </ul>
  </div>
</div>

<div class="card-standalone">
  <h2 class="section-heading"><span class="icon">&#x26A1;</span> Quick Tips &amp; Gotchas</h2>
  <div class="mini-grid">
    <div class="mini-item"><code>.gitignore</code> &mdash; List files to never track (node_modules/, .env, *.pyc)</div>
    <div class="mini-item"><code>git shortlog -sn --all</code> &mdash; Who contributed the most? &#x1F3C6;</div>
    <div class="mini-item">Commit often, push when ready. Git is cheap to commit.</div>
    <div class="mini-item">Use <code>git diff --cached</code> before every commit to double-check</div>
    <div class="mini-item"><code>git bisect start &rarr; bad/good</code> &mdash; Binary search for which commit broke something</div>
    <div class="mini-item">Never force-push shared branches (<code>git push --force-with-lease</code>)</div>
  </div>
</div>

<!-- Notes and tips rendered inline -->
<div class="card-grid" style="margin-bottom: 1rem;">
  <div class="card-item">
    <div class="note"><strong>Tip:</strong> Always configure your name &amp; email before committing. Your git username shows up on every commit.</div>
  </div>
  <div class="card-item">
    <div class="note"><strong>Run this daily:</strong> <code>git status</code> and <code>git log</code>. You can't get lost if you know where you are.</div>
  </div>
  <div class="card-item">
    <div class="note"><strong>Good commit message:</strong> Be specific and present tense. Instead of "fix stuff" write "fix sign-up form validation on Safari."</div>
  </div>
  <div class="card-item">
    <div class="note"><strong>Why?</strong> Branches let you experiment safely without breaking your working code. Delete the branch when done &mdash; nothing bad happened.</div>
  </div>
  <div class="card-item">
    <div class="note"><strong>Daily loop:</strong> <code>git pull</code> before you start &rarr; work &rarr; <code>git push</code> when done. Never work on stale code.</div>
  </div>
  <div class="card-item">
    <div class="note"><strong>Panic button:</strong> If you've already pushed a bad commit, don't panic. Tell your team and ask them to <code>git pull --rebase</code> while you fix it locally and push again.</div>
  </div>
  <div class="card-item">
    <div class="note"><strong>Rationale:</strong> The code between <span class="accent-green">=======</span> is yours; the other side is theirs. Keep what makes sense for each and remove the markers.</div>
  </div>
</div>

<!-- Code blocks (raw HTML since markdown can't color individual lines) -->
<h2 class="section-heading"><span class="icon">&#x1F4AC;</span> Example Workflows</h2>

<p style="font-size: .88rem; color: var(--muted); margin-bottom: 0.5rem;">Typical branch workflow:</p>
<pre><code># Create and switch to a new branch
git checkout -b feature/add-search
<span class="accent-green"># ... make changes and commit ...</span>
git commit -m "add search to header"
git checkout main
<span class="accent-purple">git merge feature/add-search</span></code></pre>

<p style="font-size: .88rem; color: var(--muted); margin-bottom: 0.5rem;">After finishing a feature:</p>
<pre><code><span class="accent-green"># Push your local main upstream</span>
git checkout main
<span class="accent-orange">git push origin main</span></code></pre>

<p style="font-size: .88rem; color: var(--muted); margin-bottom: 0.5rem;">Accidentally committed wrong files?</p>
<pre><code><span class="accent-red">git reset HEAD~1 --soft</span>     <span class="accent-orange"># Commit exists, but un-stages it</span></code></pre>

<p style="font-size: .88rem; color: var(--muted); margin-bottom: 0.5rem;">PR description template:</p>
<pre><code><span class="accent-green">## What &amp; Why</span>
Added dark mode toggle to the settings page...

<span class="accent-green">## Testing</span>
- Toggled on/off &mdash; works in Chrome &amp; Firefox</code></pre>

<p style="font-size: .88rem; color: var(--muted); margin-bottom: 0.5rem;">Merge conflict example:</p>
<pre><code><span class="accent-orange">&lt;&lt;&lt;&lt;&lt; feature/login</span>
  password = input("Enter password")
<span class="accent-green">=======</span>
  email = input("Enter email")
<span class="accent-red">&gt;&gt;&gt;&gt;&gt; main</span></code></pre>

<p class="credits">Made with <span style="color: var(--accent-pink);">&#x2764;</span> for the next generation of developers &mdash; keep building! &#x1F680;</p>
