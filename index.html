/* game.js
 - Jogo da tabuada com 10 níveis (1..10)
 - Registra tentativas: timestamp, nível, multiplicando, multiplicador, resposta, correto, tempo
 - Salva em localStorage e permite exportar CSV / enviar resumo por mailto
 - Possibilidade de integrar EmailJS (ver comentários mais abaixo)
*/

(() => {
  // ----- elementos DOM -----
  const studentEmailInput = document.getElementById('student-email');
  const teacherEmailInput = document.getElementById('teacher-email');
  const levelSelect = document.getElementById('level-select');
  const startBtn = document.getElementById('start-btn');
  const gameArea = document.getElementById('game-area');
  const hudStudent = document.getElementById('hud-student');
  const hudLevel = document.getElementById('hud-level');
  const hudScore = document.getElementById('hud-score');
  const hudTime = document.getElementById('hud-time');
  const multiplierSpan = document.getElementById('multiplier');
  const multiplicandSpan = document.getElementById('multiplicand');
  const answerInput = document.getElementById('answer-input');
  const submitBtn = document.getElementById('submit-answer');
  const skipBtn = document.getElementById('skip-btn');
  const feedback = document.getElementById('feedback');
  const progressEl = document.getElementById('progress');
  const correctSpan = document.getElementById('correct');
  const totalPerLevelSpan = document.getElementById('total-per-level');
  const exportBtn = document.getElementById('export-csv');
  const mailtoBtn = document.getElementById('mailto-summary');
  const clearBtn = document.getElementById('clear-data');
  const logsOutput = document.getElementById('logs-output');
  const summaryPanel = document.getElementById('summary-panel');

  // preencher select 1..10
  for(let i=1;i<=10;i++){
    const opt = document.createElement('option');
    opt.value = i; opt.textContent = i;
    levelSelect.appendChild(opt);
  }

  // ----- estado do jogo -----
  let currentLevel = 1;             // tabuada n
  let multiplicand = 1;             // número variável (1..10)
  let correctCount = 0;
  let totalPerLevel = 10;
  let score = 0;
  let startTime = null;
  let attemptStart = null;

  // registros (tentativas)
  // formato: { timestamp, studentEmail, level, multiplicand, multiplier, answer, correct, timeMs }
  let logs = JSON.parse(localStorage.getItem('tabuada_logs') || '[]');

  // carregar hud
  function updateHud(){
    hudStudent.textContent = studentEmailInput.value || '—';
    hudLevel.textContent = currentLevel;
    hudScore.textContent = score;
  }

  function saveLogs(){
    localStorage.setItem('tabuada_logs', JSON.stringify(logs));
    renderLogs();
  }

  function renderLogs(){
    if(logs.length === 0){
      logsOutput.textContent = 'Nenhum registro ainda.';
      summaryPanel.classList.add('hidden');
      return;
    }
    summaryPanel.classList.remove('hidden');
    const lines = logs.slice().reverse().map(l => {
      const t = new Date(l.timestamp).toLocaleString();
      return `${t} — Aluno:${l.studentEmail} — Nível:${l.level} — ${l.multiplicand}×${l.multiplier} = ${l.answer} — ${l.correct ? 'OK' : 'ERR'} — ${Math.round(l.timeMs)} ms`;
    });
    logsOutput.textContent = lines.join('\n');
  }

  // ----- gerar pergunta -----
  function newQuestion(){
    multiplicand = Math.floor(Math.random()*10) + 1; // 1..10
    multiplier = currentLevel; // nível = tabuada do número escolhido
    multiplierSpan.textContent = multiplier;
    multiplicandSpan.textContent = multiplicand;
    answerInput.value = '';
    feedback.textContent = '';
    attemptStart = performance.now();
  }

  // ----- checar resposta -----
  function checkAnswer(submitted){
    const correctAns = multiplicand * multiplier;
    const now = performance.now();
    const timeMs = now - (attemptStart || now);
    const studentEmail = (studentEmailInput.value || '').trim();
    const teacherEmail = (teacherEmailInput.value || '').trim();

    const record = {
      timestamp: Date.now(),
      studentEmail,
      teacherEmail,
      level: currentLevel,
      multiplicand,
      multiplier,
      answer: submitted,
      correct: Number(submitted) === correctAns,
      timeMs
    };
    logs.push(record);
    saveLogs();

    if(record.correct){
      feedback.textContent = '✅ Correto!';
      correctCount++;
      score += Math.max(10, 50 - Math.round(timeMs/100)); // recompensa por rapidez
    } else {
      feedback.textContent = `❌ Errado — resposta certa: ${correctAns}`;
      score += 0;
    }

    // atualizar HUD e progresso
    correctSpan.textContent = correctCount;
    progressEl.value = correctCount;
    hudScore.textContent = score;

    // tentar enviar relatório automático (se configurado)
    trySendAutomatic(record);

    // próxima pergunta ou fim do nível
    setTimeout(()=>{
      if(correctCount >= totalPerLevel){
        // nível concluído
        feedback.textContent = `🎉 Nível ${currentLevel} concluído! Você fez ${correctCount}/${totalPerLevel}.`;
        // preparar para próximo nível (se tiver)
        if(currentLevel < 10){
          currentLevel++;
          levelSelect.value = currentLevel;
          resetLevel();
          updateHud();
          setTimeout(()=> newQuestion(), 1200);
        } else {
          // final do jogo
          feedback.textContent = `🏆 Jogo finalizado! Pontuação total: ${score}`;
          gameOver();
        }
      } else {
        newQuestion();
      }
    }, 900);
  }

  function resetLevel(){
    correctCount = 0;
    totalPerLevel = 10;
    progressEl.max = totalPerLevel;
    progressEl.value = 0;
    correctSpan.textContent = 0;
    totalPerLevelSpan.textContent = totalPerLevel;
  }

  // ----- iniciar nível -----
  startBtn.addEventListener('click', ()=>{
    if(!studentEmailInput.value){
      alert('Por favor, informe seu e-mail (aluno).');
      studentEmailInput.focus();
      return;
    }
    currentLevel = parseInt(levelSelect.value,10) || 1;
    hudStudent.textContent = studentEmailInput.value;
    hudLevel.textContent = currentLevel;
    resetLevel();
    score = 0;
    hudScore.textContent = 0;
    updateHud();
    gameArea.classList.remove('hidden');
    summaryPanel.classList.add('hidden');
    newQuestion();
    startTime = performance.now();
    // desenhar personagem
    drawHero(currentLevel);
    answerInput.focus();
  });

  // submit answer
  submitBtn.addEventListener('click', ()=>{
    const val = answerInput.value.trim();
    if(val === ''){ feedback.textContent = 'Digite uma resposta.'; return; }
    checkAnswer(val);
  });
  answerInput.addEventListener('keydown', (e)=>{
    if(e.key === 'Enter'){ submitBtn.click(); }
  });

  // skip
  skipBtn.addEventListener('click', ()=>{
    checkAnswer('skipped');
  });

  // export CSV
  exportBtn.addEventListener('click', ()=>{
    if(logs.length === 0){ alert('Nenhum registro para exportar.'); return; }
    const header = ['timestamp','studentEmail','teacherEmail','level','multiplicand','multiplier','answer','correct','timeMs'];
    const rows = logs.map(l => header.map(h => {
      let v = l[h];
      if(v === undefined) v = '';
      return `"${String(v).replace(/"/g,'""')}"`;
    }).join(','));
    const csv = [header.join(','), ...rows].join('\n');
    const blob = new Blob([csv], {type:'text/csv;charset=utf-8;'});
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `tabuada_logs_${(studentEmailInput.value||'aluno').replace(/[^a-z0-9]/gi,'_')}.csv`;
    a.click();
    URL.revokeObjectURL(url);
  });

  // mailto summary (fallback)
  mailtoBtn.addEventListener('click', ()=>{
    if(!studentEmailInput.value || !teacherEmailInput.value){ alert('Preencha e-mails do aluno e do professor.'); return; }
    const to = teacherEmailInput.value;
    const subject = encodeURIComponent(`Relatório Jogo Tabuada — ${studentEmailInput.value}`);
    // resumo: total tentativas, acertos por nível, tempo médio
    const total = logs.length;
    const corrects = logs.filter(l=>l.correct).length;
    const timeAvg = logs.length ? Math.round(logs.reduce((s,l)=>s+l.timeMs,0)/logs.length) : 0;
    const byLevel = {};
    logs.forEach(l=>{
      byLevel[l.level] = byLevel[l.level] || {total:0,correct:0};
      byLevel[l.level].total++;
      if(l.correct) byLevel[l.level].correct++;
    });
    let body = `Aluno: ${studentEmailInput.value}\nTotal tentativas: ${total}\nAcertos: ${corrects}\nTempo médio(ms): ${timeAvg}\n\nPor nível:\n`;
    Object.keys(byLevel).sort((a,b)=>a-b).forEach(k=>{
      body += `Nível ${k}: ${byLevel[k].correct}/${byLevel[k].total}\n`;
    });
    body += '\n(Envio automático: se desejar, configure EmailJS ou outro serviço.)';
    const mailto = `mailto:${encodeURIComponent(to)}?subject=${subject}&body=${encodeURIComponent(body)}`;
    window.location.href = mailto;
  });

  // limpar logs
  clearBtn.addEventListener('click', ()=>{
    if(!confirm('Apagar todos os registros locais?')) return;
    logs = [];
    saveLogs();
    localStorage.removeItem('tabuada_logs');
    renderLogs();
  });

  // game over handler
  function gameOver(){
    // mostra painel de resumo
    renderLogs();
    summaryPanel.classList.remove('hidden');
    gameArea.classList.add('hidden');
  }

  // initial render
  updateHud();
  renderLogs();

  // ---------- desenho do personagem (canvas) ----------
  const heroCanvas = document.getElementById('hero-canvas');
  const hctx = heroCanvas.getContext('2d');

  function drawHero(level=1){
    // desenho simples e "fofo" que muda um pouco conforme o nível
    const w = heroCanvas.width, h = heroCanvas.height;
    hctx.clearRect(0,0,w,h);
    // fundo
    const grad = hctx.createLinearGradient(0,0,0,h);
    grad.addColorStop(0, '#fff7f3');
    grad.addColorStop(1, '#f0fbff');
    hctx.fillStyle = grad;
    hctx.fillRect(0,0,w,h);

    // corpo (círculo grande)
    const centerX = w/2, centerY = h/2+10;
    const bodyRadius = 56 + (level%3)*4;
    hctx.beginPath();
    hctx.arc(centerX, centerY, bodyRadius, 0, Math.PI*2);
    hctx.fillStyle = '#ffd98a';
    hctx.fill();

    // olhos
    hctx.fillStyle = '#222';
    hctx.beginPath(); hctx.arc(centerX-18, centerY-12, 8, 0, Math.PI*2); hctx.fill();
    hctx.beginPath(); hctx.arc(centerX+18, centerY-12, 8, 0, Math.PI*2); hctx.fill();
    // brilho olhos
    hctx.fillStyle = 'white';
    hctx.beginPath(); hctx.arc(centerX-16, centerY-15, 3,0,Math.PI*2); hctx.fill();
    hctx.beginPath(); hctx.arc(centerX+20, centerY-15, 3,0,Math.PI*2); hctx.fill();

    // sorriso
    hctx.strokeStyle = '#b86a00';
    hctx.lineWidth = 3;
    hctx.beginPath();
    hctx.arc(centerX, centerY+8, 20, 0, Math.PI);
    hctx.stroke();

    // chapéu/adorno muda com nível
    hctx.fillStyle = ['#6fcf97','#7aa2ff','#ff9ab3','orange'][level%4];
    hctx.fillRect(centerX-40, centerY-60, 80, 14);
    hctx.fillRect(centerX-18, centerY-78, 36, 22);
  }

  // ---------- envio automático (EmailJS) ----------
  /*
    Para ativar envio automático direto do navegador você pode usar EmailJS:
    1) crie conta em https://www.emailjs.com/
    2) crie um "service" (ex: gmail) e um "template" com campos (ex: student_email, teacher_email, message)
    3) pegue SERVICE_ID, TEMPLATE_ID e USER_ID (public key)
    4) descomente o bloco abaixo e preencha os IDs nas variáveis
    5) O código faz "emailjs.send" para cada tentativa ou para um resumo, dependendo da sua escolha.

    Nota de privacidade: EmailJS usa chaves do lado cliente (public key). Para melhor segurança, preencha e teste ou prefira um endpoint servidor (Netlify Functions, Firebase Cloud Function, GitHub Action com secrets).
  */

  // Exemplo de função que tenta enviar com EmailJS (se configurado)
  const EMAILJS_ENABLED = false; // mude para true quando configurar
  const EMAILJS_SERVICE_ID = 'YOUR_SERVICE_ID';
  const EMAILJS_TEMPLATE_ID = 'YOUR_TEMPLATE_ID';
  const EMAILJS_USER_ID = 'YOUR_USER_ID'; // public key

  function trySendAutomatic(record){
    if(!EMAILJS_ENABLED) return;
    // carrega a lib (assumindo que incluiu <script src="https://cdn.emailjs.com/dist/email.min.js"></script> em index.html)
    if(typeof emailjs === 'undefined'){
      console.warn('EmailJS não encontrado. Inclua a lib em index.html.');
      return;
    }
    const payload = {
      student_email: record.studentEmail,
      teacher_email: record.teacherEmail,
      level: record.level,
      multiplicand: record.multiplicand,
      multiplier: record.multiplier,
      answer: record.answer,
      correct: record.correct ? 'SIM' : 'NÃO',
      time_ms: Math.round(record.timeMs)
    };
    emailjs.init(EMAILJS_USER_ID);
    emailjs.send(EMAILJS_SERVICE_ID, EMAILJS_TEMPLATE_ID, payload)
      .then(()=> console.log('Enviado por EmailJS'), err=> console.error('Falha EmailJS', err));
  }

  // pronto
})();
