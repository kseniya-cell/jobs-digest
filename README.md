# jobs-digest
<!doctype html>
<html lang="ru">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Дайджест вакансий</title>
  <meta name="description" content="Подборка актуальных вакансий в удобном и красивом формате." />
  <meta property="og:title" content="Дайджест вакансий" />
  <meta property="og:description" content="Подборка актуальных вакансий в удобном и красивом формате." />
  <meta property="og:type" content="website" />
  <meta property="og:image" content="" />
  <meta name="color-scheme" content="light dark" />
  <style>
    :root{
      --bg: #0b0c0f;
      --bg-soft: #111317;
      --card: #141821;
      --text: #e9eef6;
      --muted: #9aa6b2;
      --accent: #7c9cff;
      --accent-2: #59d2fa;
      --ok: #37c977;
      --warn: #ffcc66;
      --danger: #ff7b7b;
      --stroke: #252b36;
      --chip: #1b2230;
      --chip-text: #cbd5e1;
      --shadow: 0 10px 30px rgba(0,0,0,.35);
    }
    @media (prefers-color-scheme: light){
      :root{
        --bg: #f7f8fb;
        --bg-soft: #fff;
        --card: #fff;
        --text: #0f172a;
        --muted: #64748b;
        --accent: #3b82f6;
        --accent-2: #0ea5e9;
        --stroke: #e5e7eb;
        --chip: #f1f5f9;
        --chip-text: #334155;
        --shadow: 0 10px 30px rgba(2, 6, 23, .06);
      }
    }
    *{box-sizing:border-box}
    html,body{margin:0;padding:0;background:var(--bg);color:var(--text);font:16px/1.6 ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji","Segoe UI Emoji"}
    .wrap{max-width:1100px;margin:0 auto;padding:24px}
    header.hero{display:flex;gap:20px;align-items:center;justify-content:space-between;padding:24px;border:1px solid var(--stroke);border-radius:20px;background:linear-gradient(135deg,rgba(124,156,255,.1),rgba(89,210,250,.08)),var(--card);box-shadow:var(--shadow)}
    .title{display:flex;flex-direction:column;gap:8px}
    .title h1{margin:0;font-size:28px;letter-spacing:.2px}
    .title p{margin:0;color:var(--muted)}
    .actions{display:flex;gap:10px;flex-wrap:wrap}
    .btn{appearance:none;border:1px solid var(--stroke);background:var(--chip);color:var(--chip-text);padding:10px 14px;border-radius:12px;cursor:pointer;transition:.2s ease;display:inline-flex;align-items:center;gap:8px;text-decoration:none}
    .btn.primary{background:linear-gradient(135deg,var(--accent),var(--accent-2));border:none;color:white}
    .btn:hover{transform:translateY(-1px)}

    .filters{display:grid;grid-template-columns:1fr;gap:12px;margin:20px 0}
    .filters .row{display:flex;gap:10px;flex-wrap:wrap}
    .input{border:1px solid var(--stroke);background:var(--bg-soft);color:var(--text);padding:12px 14px;border-radius:12px;outline:none;min-width:200px}
    .chip{background:var(--chip);border:1px solid var(--stroke);color:var(--chip-text);padding:6px 10px;border-radius:999px;font-size:14px;cursor:pointer}
    .chip[data-active="true"]{background:linear-gradient(135deg, rgba(124,156,255,.3), rgba(89,210,250,.3));color:white;border-color:transparent}
    .switch{display:inline-flex;align-items:center;gap:8px}
    .switch input{width:42px;height:24px;border-radius:999px;appearance:none;background:var(--chip);border:1px solid var(--stroke);position:relative;outline:none;cursor:pointer}
    .switch input:checked{background:linear-gradient(135deg,var(--accent),var(--accent-2));border-color:transparent}
    .switch input::after{content:"";position:absolute;top:2px;left:2px;width:20px;height:20px;border-radius:50%;background:#fff;transition:.2s ease}
    .switch input:checked::after{transform:translateX(18px)}

    .grid{display:grid;grid-template-columns:repeat(3,1fr);gap:16px}
    @media (max-width:1000px){.grid{grid-template-columns:repeat(2,1fr)}}
    @media (max-width:640px){.grid{grid-template-columns:1fr}}

    .card{background:var(--card);border:1px solid var(--stroke);border-radius:16px;padding:18px;display:flex;flex-direction:column;gap:10px;box-shadow:var(--shadow)}
    .card .meta{display:flex;flex-wrap:wrap;gap:8px;color:var(--muted);font-size:14px}
    .badge{display:inline-flex;align-items:center;gap:6px;padding:4px 8px;border-radius:999px;background:var(--chip);border:1px solid var(--stroke);color:var(--chip-text);font-size:12px}
    .tags{display:flex;gap:8px;flex-wrap:wrap}
    .salary{font-weight:600}
    .desc{color:var(--muted)}
    .card .cta{margin-top:6px;display:flex;gap:10px;flex-wrap:wrap}
    .sep{width:100%;height:1px;background:var(--stroke);margin:8px 0}
    footer{margin:28px 0;color:var(--muted);text-align:center}
    .empty{border:1px dashed var(--stroke);border-radius:16px;padding:24px;text-align:center;color:var(--muted)}
  </style>
</head>
<body>
  <div class="wrap">
    <header class="hero">
      <div class="title">
        <h1>Дайджест вакансий</h1>
        <p id="sub">Актуальные предложения, удобно и красиво.</p>
      </div>
      <div class="actions">
        <a class="btn" id="btn-share" href="#">Поделиться</a>
        <a class="btn primary" id="btn-subscribe" href="#">Подписаться</a>
      </div>
    </header>

    <section class="filters" aria-label="Фильтры">
      <div class="row">
        <input id="q" class="input" type="search" placeholder="Поиск: компания, должность, тег…" />
        <select id="loc" class="input">
          <option value="">Локация — любая</option>
        </select>
        <select id="type" class="input">
          <option value="">Тип — любой</option>
          <option value="full-time">Полная занятость</option>
          <option value="part-time">Частичная занятость</option>
          <option value="contract">Контракт</option>
          <option value="internship">Стажировка</option>
        </select>
        <label class="switch"><input id="only-remote" type="checkbox"/><span>Только удалёнка</span></label>
      </div>
      <div id="chips" class="row"></div>
    </section>

    <section id="list" class="grid" aria-live="polite"></section>
    <div id="empty" class="empty" style="display:none">Ничего не найдено. Попробуйте изменить фильтры.</div>

    <footer>
      <div>© <span id="year"></span> Ваш бренд / канал. Связь: <a href="mailto:hr@example.com">hr@example.com</a></div>
    </footer>
  </div>

<script>
// ==== 1) ДАННЫЕ — редактируйте только этот блок =============================
const DIGEST_TITLE = "Дайджест вакансий — август"; // заголовок в шапке
const SUBTEXT = "Обновляем подборку по мере поступления новых ролей"; // подзаголовок

/**
 * Массив вакансий. Добавляйте/удаляйте объекты.
 * Поля:
 * id           — уникальный id (строка)
 * title        — должность
 * company      — компания/бренд
 * location     — город / страна / remote
 * remote       — true/false
 * type         — full-time | part-time | contract | internship
 * salary       — строка (например, "€3 000–4 000 net")
 * posted_at    — ISO дата (YYYY-MM-DD)
 * tags         — массив тегов
 * url          — ссылка на подробности (Google Docs/Drive/сайт)
 * description  — короткое описание (1–2 предложения)
 */
const JOBS = [
  {
    id: "job-001",
    title: "Product Manager",
    company: "Acme Tech",
    location: "Remote / EU",
    remote: true,
    type: "full-time",
    salary: "$4,000–5,500",
    posted_at: "2025-08-10",
    tags: ["product", "b2c", "analytics"],
    url: "https://example.com/vacancy-1",
    description: "Отвечать за развитие мобильного продукта, работа с метриками и A/B."
  },
  {
    id: "job-002",
    title: "Маркетолог performance",
    company: "Beta Media",
    location: "Алматы / Remote",
    remote: true,
    type: "contract",
    salary: "по договорённости",
    posted_at: "2025-08-05",
    tags: ["marketing", "performance", "meta-ads"],
    url: "https://example.com/vacancy-2",
    description: "Запуск и оптимизация рекламных кампаний, отчётность, рост ROI."
  },
  {
    id: "job-003",
    title: "HR Generalist",
    company: "Gamma Studio",
    location: "Тбилиси",
    remote: false,
    type: "part-time",
    salary: "$1,500",
    posted_at: "2025-07-30",
    tags: ["hr", "recruiting", "onboarding"],
    url: "https://example.com/vacancy-3",
    description: "Поддержка полного цикла: найм, адаптация, процессы."
  }
];

// ==== 2) ЛОГИКА — всё ниже можно не трогать ================================
const $ = (q, el=document) => el.querySelector(q);
const $$ = (q, el=document) => Array.from(el.querySelectorAll(q));

const by = (key, dir='asc') => (a,b)=>{
  const x=a[key], y=b[key];
  if (x==null || y==null) return 0;
  if (typeof x === 'string' && typeof y === 'string'){
    return dir==='asc'? x.localeCompare(y) : y.localeCompare(x);
  }
  return dir==='asc'? x-y : y-x;
};

function uniq(arr){ return Array.from(new Set(arr)); }

function formatDate(iso){
  if(!iso) return '';
  try{
    const d = new Date(iso);
    return d.toLocaleDateString('ru-RU', { day:'2-digit', month:'short'});
  }catch{ return iso }
}

function renderChips(allTags){
  const box = $('#chips');
  box.innerHTML = '';
  allTags.slice(0, 20).forEach(tag=>{
    const chip = document.createElement('button');
    chip.className='chip';
    chip.textContent = `#${tag}`;
    chip.dataset.tag = tag;
    chip.addEventListener('click', ()=>{
      const active = chip.getAttribute('data-active')==='true';
      chip.setAttribute('data-active', String(!active));
      render();
    });
    box.appendChild(chip);
  });
}

function getActiveTags(){
  return $$('#chips .chip[data-active="true"]').map(c=>c.dataset.tag);
}

function fillSelects(jobs){
  const locs = uniq(jobs.map(j=>j.location).filter(Boolean)).sort();
  const locSel = $('#loc');
  locSel.innerHTML = '<option value="">Локация — любая</option>' +
    locs.map(l=>`<option value="${l}">${l}</option>`).join('');
}

function card(job){
  const tgs = job.tags?.map(t=>`<span class="badge">#${t}</span>`).join('') || '';
  return `
  <article class="card" data-id="${job.id}">
    <div class="meta">
      <span class="badge" title="Дата размещения">📅 ${formatDate(job.posted_at)}</span>
      <span class="badge" title="Тип занятости">💼 ${labelType(job.type)}</span>
      ${job.remote ? '<span class="badge">🛰️ Удалёнка</span>' : ''}
      ${job.salary ? `<span class="badge salary">💰 ${job.salary}</span>` : ''}
    </div>
    <h3 style="margin:6px 0 0">${escapeHTML(job.title)}</h3>
    <div class="meta">
      <span>🏢 ${escapeHTML(job.company)}</span>
      <span>•</span>
      <span>📍 ${escapeHTML(job.location || '—')}</span>
    </div>
    <p class="desc">${escapeHTML(job.description || '')}</p>
    <div class="tags">${tgs}</div>
    <div class="sep"></div>
    <div class="cta">
      <a class="btn primary" href="${job.url}" target="_blank" rel="noopener">Подробнее</a>
      <button class="btn" data-copy="${job.url}">Скопировать ссылку</button>
      <button class="btn" data-share>Поделиться</button>
    </div>
  </article>`;
}

function labelType(t){
  return ({
    'full-time':'Полная занятость',
    'part-time':'Частичная занятость',
    'contract':'Контракт',
    'internship':'Стажировка'
  })[t] || 'Не указано';
}

function escapeHTML(s){
  return String(s).replace(/[&<>"']/g, m=>({
    '&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;','\'':'&#39;'
  })[m]);
}

function applyFilters(jobs){
  const q = $('#q').value.trim().toLowerCase();
  const loc = $('#loc').value;
  const type = $('#type').value;
  const onlyRemote = $('#only-remote').checked;
  const activeTags = new Set(getActiveTags());

  return jobs.filter(j=>{
    if (loc && j.location !== loc) return false;
    if (type && j.type !== type) return false;
    if (onlyRemote && !j.remote) return false;

    if (activeTags.size){
      const jt = new Set(j.tags||[]);
      for (const t of activeTags){ if(!jt.has(t)) return false; }
    }

    if (q){
      const hay = `${j.title} ${j.company} ${j.location} ${(j.tags||[]).join(' ')} ${j.description}`.toLowerCase();
      if(!hay.includes(q)) return false;
    }
    return true;
  }).sort(by('posted_at','desc'));
}

function render(){
  const list = $('#list');
  const jobs = applyFilters(JOBS);
  list.innerHTML = jobs.map(card).join('');
  $('#empty').style.display = jobs.length? 'none':'block';
  $$('#list [data-copy]').forEach(btn=>{
    btn.addEventListener('click', async ()=>{
      const url = btn.getAttribute('data-copy');
      try{ await navigator.clipboard.writeText(url); btn.textContent = 'Скопировано ✓'; setTimeout(()=>btn.textContent='Скопировать ссылку', 1500);}catch{ btn.textContent = 'Скопируйте вручную'; }
    });
  });
  $$('#list [data-share]').forEach(btn=>{
    btn.addEventListener('click', async (e)=>{
      const id = e.currentTarget.closest('.card').dataset.id;
      const job = JOBS.find(j=>j.id===id);
      if (navigator.share){
        try{ await navigator.share({ title: job.title, text: `${job.title} — ${job.company}`, url: job.url }); }catch{}
      } else {
        alert('Поделиться не поддерживается. Скопируйте ссылку «Подробнее».');
      }
    });
  });
}

function init(){
  document.title = DIGEST_TITLE;
  $('#sub').textContent = SUBTEXT;
  $('#year').textContent = new Date().getFullYear();

  const allTags = uniq(JOBS.flatMap(j=>j.tags||[]));
  renderChips(allTags);
  fillSelects(JOBS);
  render();

  $('#q').addEventListener('input', render);
  $('#loc').addEventListener('change', render);
  $('#type').addEventListener('change', render);
  $('#only-remote').addEventListener('change', render);

  $('#btn-share').addEventListener('click', async (e)=>{
    e.preventDefault();
    const url = location.href;
    if(navigator.share){ try{ await navigator.share({title: DIGEST_TITLE, url}); }catch{} }
    else{ await navigator.clipboard.writeText(url); e.currentTarget.textContent='Ссылка скопирована ✓'; setTimeout(()=>e.currentTarget.textContent='Поделиться',1400) }
  });
  $('#btn-subscribe').addEventListener('click', (e)=>{
    e.preventDefault();
    alert('Здесь можно поставить ссылку на ваш канал/бот подписки.');
  });
}

document.addEventListener('DOMContentLoaded', init);
</script>
</body>
</html>
