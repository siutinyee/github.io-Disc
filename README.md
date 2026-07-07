# github.io-Disc
Collect participant responses for summary.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Public Record</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Fraunces:wght@400;500;600;700&family=Inter:wght@400;500;600&family=IBM+Plex+Mono:wght@400;500&display=swap');

  :root{
    --paper:#EAE6DC;
    --paper-card:#F7F4EC;
    --ink:#1F2733;
    --ink-soft:#5B6472;
    --brass:#9C7A2E;
    --brass-light:#C9A961;
    --seal:#8C3527;
    --rule:#C9C2B0;
  }

  *{ box-sizing:border-box; }

  body{
    margin:0;
    background:var(--paper);
    background-image:
      linear-gradient(var(--rule) 1px, transparent 1px);
    background-size: 100% 42px;
    background-attachment: local;
    color:var(--ink);
    font-family:'Inter',sans-serif;
    padding:52px 20px 90px;
    line-height:1.5;
  }

  .page{ max-width:700px; margin:0 auto; }

  .masthead{
    display:flex; justify-content:space-between; align-items:flex-end;
    border-bottom:2px solid var(--ink);
    padding-bottom:14px; margin-bottom:8px;
    flex-wrap:wrap; gap:8px;
  }
  .masthead .brand{
    font-family:'IBM Plex Mono',monospace;
    font-size:11px; letter-spacing:.16em; text-transform:uppercase;
    color:var(--ink-soft);
  }
  .masthead .case-no{
    font-family:'IBM Plex Mono',monospace;
    font-size:11px; letter-spacing:.05em;
    color:var(--brass);
  }

  section{ margin-top:38px; }

  .eyebrow{
    font-family:'IBM Plex Mono',monospace;
    font-size:11px; letter-spacing:.14em; text-transform:uppercase;
    color:var(--brass);
    display:flex; align-items:center; gap:10px;
    margin-bottom:14px;
  }
  .eyebrow::after{
    content:''; flex:1; height:1px; background:var(--rule);
  }

  .storage-banner{
    margin-top:18px;
    font-family:'IBM Plex Mono',monospace;
    font-size:11.5px; line-height:1.5;
    color:var(--seal);
    border:1px solid var(--seal);
    border-radius:3px;
    padding:10px 12px;
  }

  .topic-block{ margin-top:18px; }
  .topic-heading{
    font-family:'Fraunces', serif;
    font-weight:600;
    font-size:clamp(24px, 4.4vw, 34px);
    line-height:1.22;
    margin:0;
  }
  .topic-heading.placeholder{ color:var(--ink-soft); font-style:italic; font-weight:400; }

  .edit-toggle{
    background:none; border:none; cursor:pointer;
    font-family:'IBM Plex Mono',monospace; font-size:11px;
    color:var(--ink-soft); text-decoration:underline;
    padding:0; margin-top:10px;
  }
  .edit-toggle:hover{ color:var(--ink); }

  .topic-editor{ margin-top:14px; display:none; }
  .topic-editor.open{ display:block; }
  .topic-editor textarea{ width:100%; }
  .editor-actions{ margin-top:8px; display:flex; gap:10px; }

  label{
    display:block;
    font-family:'IBM Plex Mono',monospace;
    font-size:11px; letter-spacing:.06em; text-transform:uppercase;
    color:var(--ink-soft);
    margin-bottom:6px;
  }

  input[type="text"], textarea{
    width:100%;
    font-family:'Inter',sans-serif;
    font-size:15px;
    color:var(--ink);
    background:var(--paper-card);
    border:1px solid var(--rule);
    border-radius:3px;
    padding:11px 13px;
    resize:vertical;
  }
  input[type="text"]:focus, textarea:focus{
    outline:2px solid var(--brass);
    outline-offset:1px;
  }

  .field{ margin-bottom:16px; }
  .char-count{
    font-family:'IBM Plex Mono',monospace;
    font-size:10.5px; color:var(--ink-soft);
    text-align:right; margin-top:4px;
  }

  .btn{
    font-family:'IBM Plex Mono',monospace;
    font-size:12px; letter-spacing:.06em; text-transform:uppercase;
    padding:11px 20px;
    border-radius:3px;
    border:1px solid var(--ink);
    background:var(--ink);
    color:var(--paper-card);
    cursor:pointer;
    transition: opacity .15s ease;
  }
  .btn:hover:not(:disabled){ opacity:.85; }
  .btn:disabled{ background:var(--rule); border-color:var(--rule); color:#8a8577; cursor:not-allowed; }
  .btn-ghost{
    background:none; color:var(--ink); border:1px solid var(--rule);
  }

  .status-line{
    font-family:'IBM Plex Mono',monospace;
    font-size:11.5px; margin-top:10px; min-height:16px;
    color:var(--ink-soft);
  }
  .status-line.err{ color:var(--seal); }

  .entries-count{ color:var(--ink-soft); font-weight:400; }

  .entry{
    padding:16px 0;
    border-bottom:1px solid var(--rule);
  }
  .entry:first-child{ padding-top:0; }
  .entry-meta{
    display:flex; gap:12px; align-items:baseline; margin-bottom:6px;
    flex-wrap:wrap;
  }
  .entry-no{
    font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--brass);
  }
  .entry-name{ font-weight:600; font-size:13.5px; }
  .entry-date{
    font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--ink-soft);
  }
  .entry-text{ font-size:15px; margin:0; }

  .empty-note{
    color:var(--ink-soft); font-style:italic; font-size:14px;
    padding:14px 0;
  }

  .seal-wrap{ display:flex; flex-direction:column; align-items:center; gap:10px; margin:40px 0; }
  .seal-btn{
    width:136px; height:136px; border-radius:50%;
    border:3px solid var(--seal);
    background:transparent; color:var(--seal);
    font-family:'IBM Plex Mono',monospace;
    font-size:12px; letter-spacing:.06em; text-transform:uppercase;
    cursor:pointer;
    display:flex; align-items:center; justify-content:center; text-align:center;
    padding:14px;
    position:relative;
    transition: transform .18s cubic-bezier(.34,1.56,.64,1), background .2s ease, color .2s ease;
  }
  .seal-btn::before{
    content:''; position:absolute; inset:9px; border:1px solid var(--seal);
    border-radius:50%; opacity:.55;
  }
  .seal-btn:hover:not(:disabled){ background:var(--seal); color:var(--paper-card); }
  .seal-btn:disabled{ border-color:var(--rule); color:var(--rule); cursor:not-allowed; }
  .seal-btn:disabled::before{ border-color:var(--rule); }
  .seal-btn.stamping{ transform:scale(.86) rotate(-4deg); }
  .seal-hint{
    font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--ink-soft);
    text-align:center; max-width:320px;
  }

  .manual-panel{
    margin:28px 0 40px;
    border:1px solid var(--rule);
    border-radius:3px;
    padding:16px 18px;
    background:var(--paper-card);
  }
  .manual-panel summary{
    cursor:pointer;
    font-family:'IBM Plex Mono',monospace;
    font-size:11.5px; letter-spacing:.08em; text-transform:uppercase;
    color:var(--brass);
  }
  .manual-panel summary:hover{ color:var(--ink); }
  .manual-copy{ font-size:13.5px; color:var(--ink-soft); margin:14px 0 8px; }
  .manual-steps{
    font-size:13.5px; color:var(--ink); margin:0 0 14px; padding-left:20px;
  }
  .manual-steps li{ margin-bottom:4px; }
  .manual-paste-field{ margin-top:16px; }

  .summary-stamp{
    display:inline-flex; align-items:center; gap:8px;
    border:2px solid var(--brass); color:var(--brass);
    padding:5px 13px; border-radius:3px;
    font-family:'IBM Plex Mono',monospace; font-size:10.5px; letter-spacing:.08em; text-transform:uppercase;
    transform:rotate(-1.5deg);
    margin-bottom:20px;
  }

  .stale-note{
    font-size:13px; color:var(--ink-soft); margin-bottom:16px;
    border-left:2px solid var(--brass); padding-left:10px;
  }

  .findings-list{
    list-style:none; counter-reset:finding; margin:0; padding:0;
  }
  .findings-list li{
    counter-increment:finding;
    padding:16px 0 16px 46px;
    border-bottom:1px solid var(--rule);
    position:relative;
  }
  .findings-list li:last-child{ border-bottom:none; }
  .findings-list li::before{
    content: counter(finding);
    position:absolute; left:0; top:16px;
    font-family:'Fraunces', serif; font-weight:700; font-size:20px;
    color:var(--brass);
    width:32px; text-align:center;
  }
  .f-title{
    font-family:'Fraunces', serif; font-weight:600; font-size:17px;
    display:block; margin-bottom:4px;
  }
  .findings-list p{ margin:0; font-size:14.5px; color:var(--ink); }

  .reset-row{ margin-top:56px; text-align:center; }
  .reset-link{
    background:none; border:none; cursor:pointer;
    font-family:'IBM Plex Mono',monospace; font-size:10.5px; color:var(--ink-soft);
    text-decoration:underline; letter-spacing:.04em;
  }
  .reset-link:hover{ color:var(--seal); }

  @media (prefers-reduced-motion: reduce){
    .seal-btn{ transition:none; }
    .seal-btn.stamping{ transform:none; }
  }

  @media (max-width:520px){
    body{ padding:36px 16px 70px; }
    .masthead{ align-items:flex-start; flex-direction:column; }
  }
</style>
</head>
<body>
  <div class="page">

    <div class="masthead">
      <span class="brand">Public Record · Comment Docket</span>
      <span class="case-no" id="caseNo">No. —</span>
    </div>

    <div class="storage-banner" id="storageBanner" style="display:none;">
      Running in local preview mode — responses won't be saved or shared with others until this is opened as an artifact in Claude.ai.
    </div>

    <div class="topic-block">
      <h1 class="topic-heading" id="topicHeading">Loading record…</h1>
      <button class="edit-toggle" id="editToggle" type="button">✎ Edit the issue</button>

      <div class="topic-editor" id="topicEditor">
        <div class="field">
          <label for="topicInput">Issue under review</label>
          <textarea id="topicInput" rows="2" maxlength="240"></textarea>
        </div>
        <div class="editor-actions">
          <button class="btn" id="saveTopicBtn" type="button">Save</button>
          <button class="btn btn-ghost" id="cancelTopicBtn" type="button">Cancel</button>
        </div>
        <div class="status-line" id="topicStatus"></div>
      </div>
    </div>

    <section>
      <div class="eyebrow">Submit Testimony</div>
      <form id="submitForm">
        <div class="field">
          <label for="nameInput">Name (optional)</label>
          <input type="text" id="nameInput" maxlength="60" placeholder="Anonymous">
        </div>
        <div class="field">
          <label for="textInput">Your response</label>
          <textarea id="textInput" rows="4" maxlength="1200" placeholder="Say what you think, and why."></textarea>
          <div class="char-count" id="charCount">0 / 1200</div>
        </div>
        <button class="btn" id="submitBtn" type="submit">File Response</button>
        <div class="status-line" id="submitStatus"></div>
      </form>
    </section>

    <section>
      <div class="eyebrow">Entries on Record <span class="entries-count" id="entryCount">(0)</span></div>
      <div id="entriesList"></div>
    </section>

    <div class="seal-wrap">
      <button class="seal-btn" id="compileBtn" type="button">Compile Findings</button>
      <div class="seal-hint" id="sealHint"></div>
      <div class="status-line" id="compileStatus"></div>
    </div>

    <details class="manual-panel" id="manualPanel">
      <summary>Compile it yourself instead</summary>
      <p class="manual-copy">
        If the automatic stamp above keeps failing, you can get the same result through
        a normal conversation with Claude:
      </p>
      <ol class="manual-steps">
        <li>Copy the responses below.</li>
        <li>Paste them into any chat with Claude and ask for 5 to 7 key points.</li>
        <li>Paste Claude's answer back in below and save it to the record.</li>
      </ol>
      <button class="btn btn-ghost" id="copyResponsesBtn" type="button">Copy responses to analyze</button>
      <span class="status-line" id="copyStatus"></span>

      <div class="field manual-paste-field">
        <label for="pasteInput">Paste Claude's analysis here</label>
        <textarea id="pasteInput" rows="6" placeholder="Paste the key points here — one per line, or as JSON."></textarea>
      </div>
      <button class="btn" id="savePastedBtn" type="button">Save these findings</button>
      <div class="status-line" id="pasteStatus"></div>
    </details>

    <section id="summarySection" style="display:none;">
      <div class="eyebrow">Official Summary</div>
      <div class="summary-stamp" id="summaryStamp"></div>
      <div class="stale-note" id="staleNote" style="display:none;"></div>
      <ol class="findings-list" id="findingsList"></ol>
    </section>

    <div class="reset-row">
      <button class="reset-link" id="resetBtn" type="button">Clear the entire record</button>
    </div>

  </div>

<script>
  const DEFAULT_TOPIC = '';
  const MIN_ENTRIES_TO_COMPILE = 3;

  let state = { topic: '', entries: [], summary: null };

  // --- storage layer: uses window.storage when available (persists & shares
  // across everyone viewing this artifact in Claude.ai). Falls back to an
  // in-memory store if window.storage is missing, e.g. when this file is
  // opened directly in a browser instead of Claude's artifact viewer - so
  // the app still works, just without persistence/sharing in that case. ---
  const storageAvailable = (typeof window.storage !== 'undefined' && window.storage !== null);
  const memoryStore = {};

  async function storageGet(key, shared){
    if(storageAvailable){
      return await window.storage.get(key, shared);
    }
    return Object.prototype.hasOwnProperty.call(memoryStore, key)
      ? { key, value: memoryStore[key], shared }
      : null;
  }

  async function storageSet(key, value, shared, attempts){
    attempts = attempts || 2;
    if(!storageAvailable){
      memoryStore[key] = value;
      return { key, value, shared };
    }
    let lastErr;
    for(let i = 0; i < attempts; i++){
      try{
        const result = await window.storage.set(key, value, shared);
        if(result) return result;
        lastErr = new Error('storage.set returned no result');
      }catch(e){
        lastErr = e;
      }
      if(i < attempts - 1) await new Promise(r => setTimeout(r, 350));
    }
    throw lastErr;
  }

  async function storageDelete(key, shared){
    if(!storageAvailable){
      delete memoryStore[key];
      return { key, deleted: true, shared };
    }
    return await window.storage.delete(key, shared);
  }

  function errSuffix(err){
    return (err && err.message) ? ' (' + err.message + ')' : '';
  }

  function escapeHtml(str){
    return String(str)
      .replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;')
      .replace(/"/g,'&quot;').replace(/'/g,'&#39;');
  }

  function formatDate(ts){
    const d = new Date(ts);
    return d.toLocaleDateString(undefined, { year:'numeric', month:'2-digit', day:'2-digit' });
  }

  function pad(n, len){ return String(n).padStart(len,'0'); }

  function setStatus(which, msg, isErr){
    const el = document.getElementById(which === 'submit' ? 'submitStatus' : 'compileStatus');
    el.textContent = msg || '';
    el.classList.toggle('err', !!isErr);
  }

  async function loadAll(){
    const banner = document.getElementById('storageBanner');
    if(!storageAvailable){
      banner.style.display = '';
    }

    try{
      const t = await storageGet('topic', true);
      state.topic = t ? t.value : DEFAULT_TOPIC;
    }catch(e){ state.topic = DEFAULT_TOPIC; }

    try{
      const e = await storageGet('entries', true);
      state.entries = e ? JSON.parse(e.value) : [];
    }catch(e){ state.entries = []; }

    try{
      const s = await storageGet('summary', true);
      state.summary = s ? JSON.parse(s.value) : null;
    }catch(e){ state.summary = null; }

    render();
  }

  function render(){
    // case number, derived from today
    const d = new Date();
    document.getElementById('caseNo').textContent =
      'No. ' + d.getFullYear() + '-' + pad(d.getMonth()+1,2) + pad(d.getDate(),2);

    // topic
    const heading = document.getElementById('topicHeading');
    if(state.topic && state.topic.trim()){
      heading.textContent = state.topic;
      heading.classList.remove('placeholder');
    } else {
      heading.textContent = 'No issue has been described yet — click “Edit the issue” to set one.';
      heading.classList.add('placeholder');
    }
    document.getElementById('topicInput').value = state.topic || '';

    // entries
    document.getElementById('entryCount').textContent = '(' + state.entries.length + ')';
    const list = document.getElementById('entriesList');
    if(state.entries.length === 0){
      list.innerHTML = '<div class="empty-note">No responses filed yet. Be the first.</div>';
    } else {
      list.innerHTML = state.entries.map((e, i) => `
        <div class="entry">
          <div class="entry-meta">
            <span class="entry-no">No.${pad(i+1,3)}</span>
            <span class="entry-name">${escapeHtml(e.name && e.name.trim() ? e.name.trim() : 'Anonymous')}</span>
            <span class="entry-date">${formatDate(e.ts)}</span>
          </div>
          <p class="entry-text">${escapeHtml(e.text)}</p>
        </div>
      `).join('');
    }

    // compile button
    const compileBtn = document.getElementById('compileBtn');
    const sealHint = document.getElementById('sealHint');
    const needed = MIN_ENTRIES_TO_COMPILE - state.entries.length;

    if(state.entries.length < MIN_ENTRIES_TO_COMPILE){
      compileBtn.disabled = true;
      compileBtn.textContent = 'Compile Findings';
      sealHint.textContent = needed === 1
        ? '1 more response needed before findings can be compiled.'
        : needed + ' more responses needed before findings can be compiled.';
    } else {
      compileBtn.disabled = false;
      compileBtn.textContent = state.summary ? 'Recompile Findings' : 'Compile Findings';
      sealHint.textContent = state.summary
        ? 'Stamp again to include responses filed since the last summary.'
        : 'Stamp to analyze all responses on record.';
    }

    // summary
    const summarySection = document.getElementById('summarySection');
    if(state.summary && state.summary.points && state.summary.points.length){
      summarySection.style.display = '';
      document.getElementById('summaryStamp').textContent =
        'Analyzed · ' + state.summary.basedOn + ' entries · ' + formatDate(state.summary.compiledAt);

      const staleNote = document.getElementById('staleNote');
      if(state.entries.length > state.summary.basedOn){
        staleNote.style.display = '';
        staleNote.textContent = (state.entries.length - state.summary.basedOn) +
          ' new response(s) filed since this summary was compiled. Recompile to include them.';
      } else {
        staleNote.style.display = 'none';
      }

      document.getElementById('findingsList').innerHTML = state.summary.points.map(p => `
        <li>
          <span class="f-title">${escapeHtml(p.title)}</span>
          <p>${escapeHtml(p.detail)}</p>
        </li>
      `).join('');
    } else {
      summarySection.style.display = 'none';
    }
  }

  // --- topic editing ---
  document.getElementById('editToggle').addEventListener('click', () => {
    document.getElementById('topicEditor').classList.toggle('open');
  });
  document.getElementById('cancelTopicBtn').addEventListener('click', () => {
    document.getElementById('topicInput').value = state.topic || '';
    document.getElementById('topicEditor').classList.remove('open');
  });
  document.getElementById('saveTopicBtn').addEventListener('click', async () => {
    const val = document.getElementById('topicInput').value.trim();
    const btn = document.getElementById('saveTopicBtn');
    const statusEl = document.getElementById('topicStatus');
    btn.disabled = true;
    statusEl.textContent = '';
    statusEl.classList.remove('err');
    try{
      await storageSet('topic', val, true);
      state.topic = val;
      document.getElementById('topicEditor').classList.remove('open');
      render();
    }catch(e){
      console.error(e);
      statusEl.textContent = 'Could not save the issue text' + errSuffix(e) + '. Please try again.';
      statusEl.classList.add('err');
    }finally{
      btn.disabled = false;
    }
  });

  // --- char counter ---
  document.getElementById('textInput').addEventListener('input', (ev) => {
    document.getElementById('charCount').textContent = ev.target.value.length + ' / 1200';
  });

  // --- submit response ---
  document.getElementById('submitForm').addEventListener('submit', async (ev) => {
    ev.preventDefault();
    const nameInput = document.getElementById('nameInput');
    const textInput = document.getElementById('textInput');
    const text = textInput.value.trim();

    if(text.length < 8){
      setStatus('submit', 'Please write a bit more detail before filing.', true);
      return;
    }

    const btn = document.getElementById('submitBtn');
    btn.disabled = true;
    btn.textContent = 'Filing…';
    setStatus('submit', '');

    try{
      const entry = {
        id: Date.now() + '-' + Math.random().toString(36).slice(2,7),
        name: nameInput.value.trim(),
        text,
        ts: Date.now()
      };

      let entries;
      try{
        const latest = await storageGet('entries', true);
        entries = latest ? JSON.parse(latest.value) : [];
      }catch(e){
        entries = state.entries.slice();
      }
      entries.push(entry);

      await storageSet('entries', JSON.stringify(entries), true);
      state.entries = entries;

      nameInput.value = '';
      textInput.value = '';
      document.getElementById('charCount').textContent = '0 / 1200';
      setStatus('submit', 'Response filed. Thank you.');
      render();
    }catch(err){
      console.error(err);
      setStatus('submit', 'Could not file your response' + errSuffix(err) + '. Please try again.', true);
    }finally{
      btn.disabled = false;
      btn.textContent = 'File Response';
    }
  });

  // --- compile findings via Claude ---
  document.getElementById('compileBtn').addEventListener('click', async () => {
    if(state.entries.length < MIN_ENTRIES_TO_COMPILE) return;

    const btn = document.getElementById('compileBtn');
    btn.classList.add('stamping');
    btn.disabled = true;
    setStatus('compile', 'Compiling findings…');

    try{
      const entriesText = state.entries.map((e, i) =>
        (i+1) + '. ' + (e.name && e.name.trim() ? e.name.trim() + ': ' : '') + e.text
      ).join('\n');

      const topicLine = state.topic && state.topic.trim()
        ? state.topic.trim()
        : '(no issue description was provided)';

      const prompt = 'You are analyzing public responses submitted about the following issue:\n"' +
        topicLine + '"\n\nHere are the submitted responses:\n' + entriesText +
        '\n\nAnalyze these responses and identify the 5 to 7 most important key points that summarize ' +
        'the range of views, concerns, and arguments expressed. Points should reflect what people actually ' +
        'said, including areas of agreement and disagreement where relevant. Respond ONLY with valid JSON ' +
        'in this exact format, with no other text and no markdown code fences:\n' +
        '{"points":[{"title":"short title, max 6 words","detail":"1-2 sentence explanation"}]}';

      let response;
      let fetchErr;
      const maxAttempts = 3;
      for(let attempt = 0; attempt < maxAttempts; attempt++){
        try{
          response = await fetch("https://api.anthropic.com/v1/messages", {
            method: "POST",
            headers: {
              "Content-Type": "application/json"
            },
            body: JSON.stringify({
              model: "claude-sonnet-4-6",
              max_tokens: 1000,
              messages: [{ role: "user", content: prompt }]
            })
          });
          fetchErr = null;
          break;
        }catch(e){
          fetchErr = e;
          console.error('Fetch attempt ' + (attempt + 1) + ' failed:', e.name, e.message, 'online:', navigator.onLine);
          if(attempt < maxAttempts - 1) await new Promise(r => setTimeout(r, 700 * (attempt + 1)));
        }
      }
      if(fetchErr){
        const detail = fetchErr.name ? (fetchErr.name + ': ' + fetchErr.message) : fetchErr.message;
        throw new Error('network error after ' + maxAttempts + ' attempts — ' + detail);
      }

      if(!response.ok){
        let bodyText = '';
        try{ bodyText = await response.text(); }catch(e){}
        console.error('API error body:', bodyText);
        throw new Error('API request failed: ' + response.status + (bodyText ? ' — ' + bodyText.slice(0, 200) : ''));
      }
      const data = await response.json();
      const textBlock = data.content.map(b => b.text || '').join('\n');
      const clean = textBlock.replace(/```json/g, '').replace(/```/g, '').trim();
      const parsed = JSON.parse(clean);

      if(!parsed.points || !Array.isArray(parsed.points) || parsed.points.length === 0){
        throw new Error('Unexpected response format');
      }

      state.summary = {
        points: parsed.points,
        compiledAt: Date.now(),
        basedOn: state.entries.length
      };
      await storageSet('summary', JSON.stringify(state.summary), true);
      setStatus('compile', '');
    }catch(err){
      console.error(err);
      setStatus('compile', 'Could not compile findings just now' + errSuffix(err) + '. Please try again.', true);
    }finally{
      btn.classList.remove('stamping');
      btn.disabled = false;
      render();
    }
  });

  // --- manual fallback: copy responses for analysis elsewhere ---
  document.getElementById('copyResponsesBtn').addEventListener('click', async () => {
    const statusEl = document.getElementById('copyStatus');
    const topicLine = state.topic && state.topic.trim() ? state.topic.trim() : '(no issue description was provided)';
    const entriesText = state.entries.map((e, i) =>
      (i+1) + '. ' + (e.name && e.name.trim() ? e.name.trim() + ': ' : '') + e.text
    ).join('\n');
    const payload = 'Issue: ' + topicLine + '\n\nResponses:\n' + entriesText +
      '\n\nPlease read these responses and give me the 5 to 7 most important key points that ' +
      'summarize the range of views expressed. Format each as:\nTitle — one to two sentence detail';

    try{
      if(navigator.clipboard && navigator.clipboard.writeText){
        await navigator.clipboard.writeText(payload);
      } else {
        throw new Error('clipboard API unavailable');
      }
      statusEl.textContent = 'Copied. Paste it into a chat with Claude.';
      statusEl.classList.remove('err');
    }catch(e){
      // fallback: select a temporary textarea so the person can copy manually
      const ta = document.createElement('textarea');
      ta.value = payload;
      ta.style.position = 'fixed';
      ta.style.opacity = '0';
      document.body.appendChild(ta);
      ta.select();
      try{ document.execCommand('copy'); statusEl.textContent = 'Copied. Paste it into a chat with Claude.'; statusEl.classList.remove('err'); }
      catch(e2){ statusEl.textContent = 'Could not copy automatically — select and copy the text shown in the paste box below.'; statusEl.classList.add('err'); document.getElementById('pasteInput').value = payload; }
      document.body.removeChild(ta);
    }
  });

  // Lenient parser: accepts JSON ({"points":[...]}), or plain lines like
  // "Title — detail" / "Title - detail" / "Title: detail" / "1. Title: detail"
  function parsePastedFindings(raw){
    const cleaned = raw.replace(/```json/gi, '').replace(/```/g, '').trim();

    try{
      const parsed = JSON.parse(cleaned);
      if(parsed && Array.isArray(parsed.points) && parsed.points.length){
        return parsed.points
          .map(p => ({ title: String(p.title || '').trim(), detail: String(p.detail || '').trim() }))
          .filter(p => p.title);
      }
    }catch(e){ /* not JSON, fall through to line parsing */ }

    const lines = cleaned.split('\n').map(l => l.trim()).filter(Boolean);
    const points = [];
    for(const line of lines){
      const noNum = line.replace(/^(\d+[\.\)]|\-|\*)\s*/, '').replace(/\*\*/g, '');
      if(!noNum) continue;
      const sepMatch = noNum.match(/\s[—–-]\s|:\s/);
      if(sepMatch){
        const idx = noNum.indexOf(sepMatch[0]);
        points.push({
          title: noNum.slice(0, idx).trim(),
          detail: noNum.slice(idx + sepMatch[0].length).trim()
        });
      } else {
        points.push({ title: noNum, detail: '' });
      }
    }
    return points;
  }

  document.getElementById('savePastedBtn').addEventListener('click', async () => {
    const statusEl = document.getElementById('pasteStatus');
    const raw = document.getElementById('pasteInput').value.trim();
    statusEl.textContent = '';
    statusEl.classList.remove('err');

    if(!raw){
      statusEl.textContent = 'Paste an analysis first.';
      statusEl.classList.add('err');
      return;
    }

    const points = parsePastedFindings(raw);
    if(points.length < 1){
      statusEl.textContent = 'Could not find any key points in that text — check the format and try again.';
      statusEl.classList.add('err');
      return;
    }

    const btn = document.getElementById('savePastedBtn');
    btn.disabled = true;
    try{
      state.summary = {
        points: points.slice(0, 10),
        compiledAt: Date.now(),
        basedOn: state.entries.length
      };
      await storageSet('summary', JSON.stringify(state.summary), true);
      document.getElementById('pasteInput').value = '';
      statusEl.textContent = 'Saved to the record.';
      document.getElementById('manualPanel').removeAttribute('open');
      render();
    }catch(e){
      console.error(e);
      statusEl.textContent = 'Could not save' + errSuffix(e) + '. Please try again.';
      statusEl.classList.add('err');
    }finally{
      btn.disabled = false;
    }
  });

  // --- reset ---
  document.getElementById('resetBtn').addEventListener('click', async () => {
    if(!confirm('This clears every response and the compiled summary for everyone. Continue?')) return;
    try{
      await storageSet('entries', JSON.stringify([]), true);
      await storageDelete('summary', true).catch(() => {});
      state.entries = [];
      state.summary = null;
      render();
    }catch(e){
      console.error(e);
      alert('Could not clear the record' + errSuffix(e) + '. Please try again.');
    }
  });

  loadAll();
</script>
</body>
</html>
