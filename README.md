<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ian — Portfólio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,600;0,9..144,700;1,9..144,500&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
<script src="https://www.gstatic.com/firebasejs/10.13.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.13.0/firebase-database-compat.js"></script>
<style>
  .config-banner {
    background: #B91C1C; color: #fff; font-family: 'Space Grotesk', sans-serif;
    font-size: 14px; padding: 12px 20px; text-align: center;
  }
  .config-banner code { background: rgba(255,255,255,0.18); padding: 2px 6px; border-radius: 3px; }
  :root{
    --cork: #4A3423;
    --cork-dark: #3A2A1B;
    --paper: #F7F1E1;
    --ink: #2A1F16;
    --yellow: #FFC93C;
    --coral: #FF6B5B;
    --sky: #4EA8DE;
    --mint: #6BCB77;
    --violet: #A78BFA;
  }

  * { box-sizing: border-box; }

  body {
    margin: 0;
    background:
      radial-gradient(circle at 20% 20%, rgba(255,255,255,0.03) 0, transparent 40%),
      radial-gradient(circle at 80% 60%, rgba(0,0,0,0.08) 0, transparent 45%),
      var(--cork);
    background-color: var(--cork);
    background-image:
      radial-gradient(rgba(0,0,0,0.12) 1px, transparent 1px);
    background-size: 6px 6px;
    color: var(--paper);
    font-family: 'Space Grotesk', sans-serif;
    -webkit-font-smoothing: antialiased;
  }

  .wrap { max-width: 880px; margin: 0 auto; padding: 64px 24px 96px; }

  /* HERO */
  .hero { text-align: center; padding: 40px 0 56px; opacity: 0; animation: fadeUp 0.8s ease forwards; }
  @keyframes fadeUp { from { opacity: 0; transform: translateY(14px); } to { opacity: 1; transform: translateY(0); } }

  .hero-name {
    font-family: 'Fraunces', serif;
    font-weight: 700;
    font-size: clamp(48px, 9vw, 84px);
    color: var(--paper);
    margin: 0;
    letter-spacing: -0.01em;
  }

  .hero-tagline {
    font-family: 'Fraunces', serif;
    font-style: italic;
    font-weight: 500;
    font-size: clamp(19px, 3vw, 26px);
    color: var(--yellow);
    margin: 18px auto 0;
    max-width: 560px;
    line-height: 1.45;
    position: relative;
  }
  .hero-tagline::before { content: "“"; }
  .hero-tagline::after { content: "”"; }

  .hero-bio {
    font-size: 16px;
    color: rgba(247,241,225,0.72);
    max-width: 480px;
    margin: 22px auto 0;
    line-height: 1.6;
  }

  .hero-rule {
    width: 46px; height: 3px; background: var(--coral);
    margin: 30px auto 0; border-radius: 2px;
  }

  /* SECTION HEADER */
  .section-eyebrow {
    font-size: 13px; letter-spacing: 0.14em; text-transform: uppercase;
    color: var(--mint); font-weight: 600; text-align: center; margin-bottom: 6px;
  }
  .section-title {
    font-family: 'Fraunces', serif; font-weight: 600; text-align: center;
    font-size: clamp(28px, 5vw, 38px); margin: 0 0 8px;
  }
  .section-sub {
    text-align: center; color: rgba(247,241,225,0.62); font-size: 15px;
    max-width: 460px; margin: 0 auto 40px;
  }

  /* CORKBOARD */
  .board {
    background: linear-gradient(180deg, var(--cork-dark), var(--cork));
    border: 10px solid #2E2013;
    border-radius: 8px;
    box-shadow: 0 18px 40px rgba(0,0,0,0.4), inset 0 0 60px rgba(0,0,0,0.25);
    padding: 32px;
    position: relative;
  }

  /* ADD FORM — index card */
  .add-card {
    background: var(--paper);
    color: var(--ink);
    border-radius: 3px;
    padding: 20px 22px;
    max-width: 460px;
    margin: 0 auto 32px;
    box-shadow: 0 8px 18px rgba(0,0,0,0.35);
    transform: rotate(-0.6deg);
  }
  .add-card h3 {
    font-family: 'Fraunces', serif; font-weight: 600; font-size: 17px;
    margin: 0 0 14px;
  }
  .field-row { display: flex; gap: 10px; margin-bottom: 10px; }
  .field-row.stack { flex-direction: column; }
  .add-card input, .add-card select {
    font-family: 'Space Grotesk', sans-serif;
    font-size: 14px;
    padding: 9px 10px;
    border: 1px solid rgba(42,31,22,0.25);
    border-radius: 4px;
    background: #fff;
    color: var(--ink);
    flex: 1;
    width: 100%;
  }
  .add-card input:focus, .add-card select:focus, .add-card button:focus {
    outline: 2px solid var(--sky); outline-offset: 1px;
  }
  .add-btn {
    width: 100%; margin-top: 4px;
    background: var(--ink); color: var(--paper);
    border: none; border-radius: 4px;
    padding: 10px 14px; font-family: 'Space Grotesk', sans-serif;
    font-weight: 600; font-size: 14px; cursor: pointer;
    transition: transform 0.15s ease, background 0.15s ease;
  }
  .add-btn:hover { background: var(--coral); }
  .add-btn:active { transform: scale(0.98); }

  /* NOTES GRID */
  .notes-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(170px, 1fr));
    gap: 22px 18px;
  }

  .note {
    position: relative;
    padding: 20px 16px 18px;
    border-radius: 2px;
    box-shadow: 0 8px 16px rgba(0,0,0,0.32);
    color: var(--ink);
    min-height: 130px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    transition: transform 0.18s ease;
    animation: pinDrop 0.4s ease backwards;
  }
  @keyframes pinDrop { from { opacity: 0; transform: translateY(-10px) scale(0.95); } to { opacity: 1; transform: translateY(0) scale(1); } }
  .note:hover { transform: translateY(-3px) scale(1.02); }
  .note::before {
    content: ""; position: absolute; top: -8px; left: 50%; transform: translateX(-50%);
    width: 14px; height: 14px; border-radius: 50%;
    background: radial-gradient(circle at 35% 30%, #fff8, #8884 60%, #0004);
    box-shadow: 0 2px 3px rgba(0,0,0,0.4);
  }

  .note.n1 { background: var(--yellow); transform: rotate(-2deg); }
  .note.n2 { background: var(--coral); color: #fff; transform: rotate(1.5deg); }
  .note.n3 { background: var(--sky); color: #fff; transform: rotate(-1deg); }
  .note.n4 { background: var(--mint); transform: rotate(2deg); }
  .note.n5 { background: var(--violet); color: #fff; transform: rotate(-1.6deg); }
  .note:hover { transform: rotate(0deg) translateY(-3px) scale(1.03); }

  .note-subject {
    font-size: 11px; letter-spacing: 0.08em; text-transform: uppercase;
    font-weight: 700; opacity: 0.75; margin-bottom: 6px;
  }
  .note-title {
    font-family: 'Fraunces', serif; font-weight: 600; font-size: 16px;
    line-height: 1.3; margin-bottom: 10px; word-break: break-word;
  }
  .note.done .note-title { text-decoration: line-through; opacity: 0.55; }
  .note-footer {
    display: flex; align-items: center; justify-content: space-between;
    font-size: 12px; font-weight: 600;
  }
  .note-date { opacity: 0.8; }
  .note-actions { display: flex; gap: 8px; align-items: center; }
  .note-check, .note-del {
    background: rgba(255,255,255,0.35);
    border: none; border-radius: 4px; cursor: pointer;
    width: 24px; height: 24px; font-size: 13px;
    display: flex; align-items: center; justify-content: center;
    color: inherit;
  }
  .note-check:hover, .note-del:hover { background: rgba(255,255,255,0.6); }

  .empty-state {
    grid-column: 1 / -1;
    text-align: center; padding: 40px 20px;
    color: rgba(247,241,225,0.55); font-size: 14px;
    border: 1.5px dashed rgba(247,241,225,0.25); border-radius: 8px;
  }

  footer {
    text-align: center; margin-top: 56px;
    color: rgba(247,241,225,0.4); font-size: 13px;
  }

  @media (prefers-reduced-motion: reduce) {
    * { animation: none !important; transition: none !important; }
  }
</style>
</head>
<body>

<div class="config-banner" id="config-banner">
  ⚠️ O mural ainda não está conectado ao Firebase. Abra o arquivo em um editor de texto e preencha o objeto <code>firebaseConfig</code> no final do arquivo com os dados do seu projeto.
</div>

<div class="wrap">

  <section class="hero">
    <h1 class="hero-name">Ian</h1>
    <p class="hero-tagline">Aprendo perguntando, cresço duvidando.</p>
    <p class="hero-bio">Estudante, curioso por natureza — explorando ideias, tarefas e descobertas, um projeto de cada vez.</p>
    <div class="hero-rule"></div>
  </section>

  <section>
    <div class="section-eyebrow">Projeto em destaque</div>
    <h2 class="section-title">Mural da Turma</h2>
    <p class="section-sub">Onde as tarefas da turma ganham forma — adicione, acompanhe e risque o que já foi feito.</p>

    <div class="board">
      <form class="add-card" id="add-form">
        <h3>+ Nova tarefa</h3>
        <div class="field-row">
          <select id="f-subject" required>
            <option value="" disabled selected>Matéria</option>
            <option>Português</option>
            <option>História</option>
            <option>Biologia</option>
            <option>Matemática</option>
            <option>Geografia</option>
            <option>Inglês</option>
            <option>Outra</option>
          </select>
        </div>
        <div class="field-row">
          <input id="f-title" type="text" placeholder="O que precisa ser feito?" required>
        </div>
        <div class="field-row">
          <input id="f-date" type="date">
        </div>
        <button type="submit" class="add-btn">Fixar no mural</button>
      </form>

      <div class="notes-grid" id="notes-grid">
        <div class="empty-state" id="empty-state">Nenhuma tarefa fixada ainda. Adicione a primeira acima ↑</div>
      </div>
    </div>
  </section>

  <footer>Site privado · feito por Ian</footer>
</div>

<script>
(function(){
  const COLORS = ['n1','n2','n3','n4','n5'];
  let tasks = [];

  // ====================================================================
  // CONFIGURAÇÃO DO FIREBASE
  // Substitua os valores abaixo pelos do SEU projeto Firebase.
  // Veja o passo a passo que o Claude te enviou no chat para gerar isso.
  // ====================================================================
  const firebaseConfig = {
    apiKey: "COLE_AQUI_SUA_API_KEY",
    authDomain: "COLE_AQUI.firebaseapp.com",
    databaseURL: "https://COLE_AQUI-default-rtdb.firebaseio.com",
    projectId: "COLE_AQUI",
    storageBucket: "COLE_AQUI.appspot.com",
    messagingSenderId: "COLE_AQUI",
    appId: "COLE_AQUI"
  };

  const isConfigured = firebaseConfig.apiKey !== "COLE_AQUI_SUA_API_KEY";
  let dbRef = null;

  if (isConfigured) {
    document.getElementById('config-banner').style.display = 'none';
    firebase.initializeApp(firebaseConfig);
    dbRef = firebase.database().ref('muralTasks');
  } else {
    console.warn('Firebase não configurado — preencha firebaseConfig no arquivo.');
  }

  function fmtDate(d){
    if(!d) return 'sem data';
    const [y,m,day] = d.split('-');
    return day + '/' + m;
  }

  function render(){
    const grid = document.getElementById('notes-grid');
    grid.innerHTML = '';
    if(tasks.length === 0){
      const empty = document.createElement('div');
      empty.className = 'empty-state';
      empty.id = 'empty-state';
      empty.textContent = 'Nenhuma tarefa fixada ainda. Adicione a primeira acima ↑';
      grid.appendChild(empty);
      return;
    }
    tasks.forEach((t, i) => {
      const note = document.createElement('div');
      note.className = 'note ' + COLORS[i % COLORS.length] + (t.completed ? ' done' : '');
      note.innerHTML = `
        <div>
          <div class="note-subject">${t.subject}</div>
          <div class="note-title">${t.title}</div>
        </div>
        <div class="note-footer">
          <span class="note-date">${fmtDate(t.date)}</span>
          <span class="note-actions">
            <button class="note-check" title="Marcar como concluída" aria-label="Marcar como concluída">${t.completed ? '↺' : '✓'}</button>
            <button class="note-del" title="Remover" aria-label="Remover">✕</button>
          </span>
        </div>
      `;
      note.querySelector('.note-check').addEventListener('click', () => toggleTask(t.id));
      note.querySelector('.note-del').addEventListener('click', () => deleteTask(t.id));
      grid.appendChild(note);
    });
  }

  function tasksToObject(){
    const obj = {};
    tasks.forEach(t => { obj[t.id] = t; });
    return obj;
  }

  async function save(){
    if(!isConfigured){
      console.warn('Firebase não configurado — a tarefa não foi salva de forma compartilhada.');
      return;
    }
    try {
      await dbRef.set(tasksToObject());
    } catch(e) {
      console.warn('Não foi possível salvar o mural no Firebase:', e);
    }
  }

  function load(){
    if(!isConfigured){
      render();
      return;
    }
    // Escuta mudanças em tempo real — quando qualquer pessoa altera o mural,
    // todo mundo com a página aberta vê a atualização automaticamente.
    dbRef.on('value', (snapshot) => {
      const data = snapshot.val() || {};
      tasks = Object.values(data);
      render();
    }, (error) => {
      console.warn('Erro ao ler o mural do Firebase:', error);
    });
  }

  function toggleTask(id){
    const t = tasks.find(t => t.id === id);
    if(t){
      t.completed = !t.completed;
      if(t.completed) t.completedAt = new Date().toISOString();
      render();
      save();
    }
  }

  function deleteTask(id){
    tasks = tasks.filter(t => t.id !== id);
    render();
    save();
  }

  document.getElementById('add-form').addEventListener('submit', function(e){
    e.preventDefault();
    const subject = document.getElementById('f-subject').value;
    const title = document.getElementById('f-title').value.trim();
    const date = document.getElementById('f-date').value;
    if(!title) return;
    tasks.push({
      id: 't' + Date.now(),
      subject: subject || 'Outra',
      title: title,
      date: date,
      completed: false
    });
    render();
    save();
    this.reset();
  });

  load();
})();
</script>

</body>
</html><!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ian — Portfólio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,600;0,9..144,700;1,9..144,500&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
<script src="https://www.gstatic.com/firebasejs/10.13.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.13.0/firebase-database-compat.js"></script>
<style>
  .config-banner {
    background: #B91C1C; color: #fff; font-family: 'Space Grotesk', sans-serif;
    font-size: 14px; padding: 12px 20px; text-align: center;
  }
  .config-banner code { background: rgba(255,255,255,0.18); padding: 2px 6px; border-radius: 3px; }
  :root{
    --cork: #4A3423;
    --cork-dark: #3A2A1B;
    --paper: #F7F1E1;
    --ink: #2A1F16;
    --yellow: #FFC93C;
    --coral: #FF6B5B;
    --sky: #4EA8DE;
    --mint: #6BCB77;
    --violet: #A78BFA;
  }

  * { box-sizing: border-box; }

  body {
    margin: 0;
    background:
      radial-gradient(circle at 20% 20%, rgba(255,255,255,0.03) 0, transparent 40%),
      radial-gradient(circle at 80% 60%, rgba(0,0,0,0.08) 0, transparent 45%),
      var(--cork);
    background-color: var(--cork);
    background-image:
      radial-gradient(rgba(0,0,0,0.12) 1px, transparent 1px);
    background-size: 6px 6px;
    color: var(--paper);
    font-family: 'Space Grotesk', sans-serif;
    -webkit-font-smoothing: antialiased;
  }

  .wrap { max-width: 880px; margin: 0 auto; padding: 64px 24px 96px; }

  /* HERO */
  .hero { text-align: center; padding: 40px 0 56px; opacity: 0; animation: fadeUp 0.8s ease forwards; }
  @keyframes fadeUp { from { opacity: 0; transform: translateY(14px); } to { opacity: 1; transform: translateY(0); } }

  .hero-name {
    font-family: 'Fraunces', serif;
    font-weight: 700;
    font-size: clamp(48px, 9vw, 84px);
    color: var(--paper);
    margin: 0;
    letter-spacing: -0.01em;
  }

  .hero-tagline {
    font-family: 'Fraunces', serif;
    font-style: italic;
    font-weight: 500;
    font-size: clamp(19px, 3vw, 26px);
    color: var(--yellow);
    margin: 18px auto 0;
    max-width: 560px;
    line-height: 1.45;
    position: relative;
  }
  .hero-tagline::before { content: "“"; }
  .hero-tagline::after { content: "”"; }

  .hero-bio {
    font-size: 16px;
    color: rgba(247,241,225,0.72);
    max-width: 480px;
    margin: 22px auto 0;
    line-height: 1.6;
  }

  .hero-rule {
    width: 46px; height: 3px; background: var(--coral);
    margin: 30px auto 0; border-radius: 2px;
  }

  /* SECTION HEADER */
  .section-eyebrow {
    font-size: 13px; letter-spacing: 0.14em; text-transform: uppercase;
    color: var(--mint); font-weight: 600; text-align: center; margin-bottom: 6px;
  }
  .section-title {
    font-family: 'Fraunces', serif; font-weight: 600; text-align: center;
    font-size: clamp(28px, 5vw, 38px); margin: 0 0 8px;
  }
  .section-sub {
    text-align: center; color: rgba(247,241,225,0.62); font-size: 15px;
    max-width: 460px; margin: 0 auto 40px;
  }

  /* CORKBOARD */
  .board {
    background: linear-gradient(180deg, var(--cork-dark), var(--cork));
    border: 10px solid #2E2013;
    border-radius: 8px;
    box-shadow: 0 18px 40px rgba(0,0,0,0.4), inset 0 0 60px rgba(0,0,0,0.25);
    padding: 32px;
    position: relative;
  }

  /* ADD FORM — index card */
  .add-card {
    background: var(--paper);
    color: var(--ink);
    border-radius: 3px;
    padding: 20px 22px;
    max-width: 460px;
    margin: 0 auto 32px;
    box-shadow: 0 8px 18px rgba(0,0,0,0.35);
    transform: rotate(-0.6deg);
  }
  .add-card h3 {
    font-family: 'Fraunces', serif; font-weight: 600; font-size: 17px;
    margin: 0 0 14px;
  }
  .field-row { display: flex; gap: 10px; margin-bottom: 10px; }
  .field-row.stack { flex-direction: column; }
  .add-card input, .add-card select {
    font-family: 'Space Grotesk', sans-serif;
    font-size: 14px;
    padding: 9px 10px;
    border: 1px solid rgba(42,31,22,0.25);
    border-radius: 4px;
    background: #fff;
    color: var(--ink);
    flex: 1;
    width: 100%;
  }
  .add-card input:focus, .add-card select:focus, .add-card button:focus {
    outline: 2px solid var(--sky); outline-offset: 1px;
  }
  .add-btn {
    width: 100%; margin-top: 4px;
    background: var(--ink); color: var(--paper);
    border: none; border-radius: 4px;
    padding: 10px 14px; font-family: 'Space Grotesk', sans-serif;
    font-weight: 600; font-size: 14px; cursor: pointer;
    transition: transform 0.15s ease, background 0.15s ease;
  }
  .add-btn:hover { background: var(--coral); }
  .add-btn:active { transform: scale(0.98); }

  /* NOTES GRID */
  .notes-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(170px, 1fr));
    gap: 22px 18px;
  }

  .note {
    position: relative;
    padding: 20px 16px 18px;
    border-radius: 2px;
    box-shadow: 0 8px 16px rgba(0,0,0,0.32);
    color: var(--ink);
    min-height: 130px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    transition: transform 0.18s ease;
    animation: pinDrop 0.4s ease backwards;
  }
  @keyframes pinDrop { from { opacity: 0; transform: translateY(-10px) scale(0.95); } to { opacity: 1; transform: translateY(0) scale(1); } }
  .note:hover { transform: translateY(-3px) scale(1.02); }
  .note::before {
    content: ""; position: absolute; top: -8px; left: 50%; transform: translateX(-50%);
    width: 14px; height: 14px; border-radius: 50%;
    background: radial-gradient(circle at 35% 30%, #fff8, #8884 60%, #0004);
    box-shadow: 0 2px 3px rgba(0,0,0,0.4);
  }

  .note.n1 { background: var(--yellow); transform: rotate(-2deg); }
  .note.n2 { background: var(--coral); color: #fff; transform: rotate(1.5deg); }
  .note.n3 { background: var(--sky); color: #fff; transform: rotate(-1deg); }
  .note.n4 { background: var(--mint); transform: rotate(2deg); }
  .note.n5 { background: var(--violet); color: #fff; transform: rotate(-1.6deg); }
  .note:hover { transform: rotate(0deg) translateY(-3px) scale(1.03); }

  .note-subject {
    font-size: 11px; letter-spacing: 0.08em; text-transform: uppercase;
    font-weight: 700; opacity: 0.75; margin-bottom: 6px;
  }
  .note-title {
    font-family: 'Fraunces', serif; font-weight: 600; font-size: 16px;
    line-height: 1.3; margin-bottom: 10px; word-break: break-word;
  }
  .note.done .note-title { text-decoration: line-through; opacity: 0.55; }
  .note-footer {
    display: flex; align-items: center; justify-content: space-between;
    font-size: 12px; font-weight: 600;
  }
  .note-date { opacity: 0.8; }
  .note-actions { display: flex; gap: 8px; align-items: center; }
  .note-check, .note-del {
    background: rgba(255,255,255,0.35);
    border: none; border-radius: 4px; cursor: pointer;
    width: 24px; height: 24px; font-size: 13px;
    display: flex; align-items: center; justify-content: center;
    color: inherit;
  }
  .note-check:hover, .note-del:hover { background: rgba(255,255,255,0.6); }

  .empty-state {
    grid-column: 1 / -1;
    text-align: center; padding: 40px 20px;
    color: rgba(247,241,225,0.55); font-size: 14px;
    border: 1.5px dashed rgba(247,241,225,0.25); border-radius: 8px;
  }

  footer {
    text-align: center; margin-top: 56px;
    color: rgba(247,241,225,0.4); font-size: 13px;
  }

  @media (prefers-reduced-motion: reduce) {
    * { animation: none !important; transition: none !important; }
  }
</style>
</head>
<body>

<div class="config-banner" id="config-banner">
  ⚠️ O mural ainda não está conectado ao Firebase. Abra o arquivo em um editor de texto e preencha o objeto <code>firebaseConfig</code> no final do arquivo com os dados do seu projeto.
</div>

<div class="wrap">

  <section class="hero">
    <h1 class="hero-name">Ian</h1>
    <p class="hero-tagline">Aprendo perguntando, cresço duvidando.</p>
    <p class="hero-bio">Estudante, curioso por natureza — explorando ideias, tarefas e descobertas, um projeto de cada vez.</p>
    <div class="hero-rule"></div>
  </section>

  <section>
    <div class="section-eyebrow">Projeto em destaque</div>
    <h2 class="section-title">Mural da Turma</h2>
    <p class="section-sub">Onde as tarefas da turma ganham forma — adicione, acompanhe e risque o que já foi feito.</p>

    <div class="board">
      <form class="add-card" id="add-form">
        <h3>+ Nova tarefa</h3>
        <div class="field-row">
          <select id="f-subject" required>
            <option value="" disabled selected>Matéria</option>
            <option>Português</option>
            <option>História</option>
            <option>Biologia</option>
            <option>Matemática</option>
            <option>Geografia</option>
            <option>Inglês</option>
            <option>Outra</option>
          </select>
        </div>
        <div class="field-row">
          <input id="f-title" type="text" placeholder="O que precisa ser feito?" required>
        </div>
        <div class="field-row">
          <input id="f-date" type="date">
        </div>
        <button type="submit" class="add-btn">Fixar no mural</button>
      </form>

      <div class="notes-grid" id="notes-grid">
        <div class="empty-state" id="empty-state">Nenhuma tarefa fixada ainda. Adicione a primeira acima ↑</div>
      </div>
    </div>
  </section>

  <footer>Site privado · feito por Ian</footer>
</div>

<script>
(function(){
  const COLORS = ['n1','n2','n3','n4','n5'];
  let tasks = [];

  // ====================================================================
  // CONFIGURAÇÃO DO FIREBASE
  // Substitua os valores abaixo pelos do SEU projeto Firebase.
  // Veja o passo a passo que o Claude te enviou no chat para gerar isso.
  // ====================================================================
  const firebaseConfig = {
    apiKey: "COLE_AQUI_SUA_API_KEY",
    authDomain: "COLE_AQUI.firebaseapp.com",
    databaseURL: "https://COLE_AQUI-default-rtdb.firebaseio.com",
    projectId: "COLE_AQUI",
    storageBucket: "COLE_AQUI.appspot.com",
    messagingSenderId: "COLE_AQUI",
    appId: "COLE_AQUI"
  };

  const isConfigured = firebaseConfig.apiKey !== "COLE_AQUI_SUA_API_KEY";
  let dbRef = null;

  if (isConfigured) {
    document.getElementById('config-banner').style.display = 'none';
    firebase.initializeApp(firebaseConfig);
    dbRef = firebase.database().ref('muralTasks');
  } else {
    console.warn('Firebase não configurado — preencha firebaseConfig no arquivo.');
  }

  function fmtDate(d){
    if(!d) return 'sem data';
    const [y,m,day] = d.split('-');
    return day + '/' + m;
  }

  function render(){
    const grid = document.getElementById('notes-grid');
    grid.innerHTML = '';
    if(tasks.length === 0){
      const empty = document.createElement('div');
      empty.className = 'empty-state';
      empty.id = 'empty-state';
      empty.textContent = 'Nenhuma tarefa fixada ainda. Adicione a primeira acima ↑';
      grid.appendChild(empty);
      return;
    }
    tasks.forEach((t, i) => {
      const note = document.createElement('div');
      note.className = 'note ' + COLORS[i % COLORS.length] + (t.completed ? ' done' : '');
      note.innerHTML = `
        <div>
          <div class="note-subject">${t.subject}</div>
          <div class="note-title">${t.title}</div>
        </div>
        <div class="note-footer">
          <span class="note-date">${fmtDate(t.date)}</span>
          <span class="note-actions">
            <button class="note-check" title="Marcar como concluída" aria-label="Marcar como concluída">${t.completed ? '↺' : '✓'}</button>
            <button class="note-del" title="Remover" aria-label="Remover">✕</button>
          </span>
        </div>
      `;
      note.querySelector('.note-check').addEventListener('click', () => toggleTask(t.id));
      note.querySelector('.note-del').addEventListener('click', () => deleteTask(t.id));
      grid.appendChild(note);
    });
  }

  function tasksToObject(){
    const obj = {};
    tasks.forEach(t => { obj[t.id] = t; });
    return obj;
  }

  async function save(){
    if(!isConfigured){
      console.warn('Firebase não configurado — a tarefa não foi salva de forma compartilhada.');
      return;
    }
    try {
      await dbRef.set(tasksToObject());
    } catch(e) {
      console.warn('Não foi possível salvar o mural no Firebase:', e);
    }
  }

  function load(){
    if(!isConfigured){
      render();
      return;
    }
    // Escuta mudanças em tempo real — quando qualquer pessoa altera o mural,
    // todo mundo com a página aberta vê a atualização automaticamente.
    dbRef.on('value', (snapshot) => {
      const data = snapshot.val() || {};
      tasks = Object.values(data);
      render();
    }, (error) => {
      console.warn('Erro ao ler o mural do Firebase:', error);
    });
  }

  function toggleTask(id){
    const t = tasks.find(t => t.id === id);
    if(t){
      t.completed = !t.completed;
      if(t.completed) t.completedAt = new Date().toISOString();
      render();
      save();
    }
  }

  function deleteTask(id){
    tasks = tasks.filter(t => t.id !== id);
    render();
    save();
  }

  document.getElementById('add-form').addEventListener('submit', function(e){
    e.preventDefault();
    const subject = document.getElementById('f-subject').value;
    const title = document.getElementById('f-title').value.trim();
    const date = document.getElementById('f-date').value;
    if(!title) return;
    tasks.push({
      id: 't' + Date.now(),
      subject: subject || 'Outra',
      title: title,
      date: date,
      completed: false
    });
    render();
    save();
    this.reset();
  });

  load();
})();
</script>

</body>
</html>
