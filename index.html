/* Clima de Aula — lógica de la app (Firebase Realtime Database) */
(function(){
  const PREGUNTAS = [
    {id:'p1', txt:'Me siento a gusto en esta clase / con el ambiente del grupo.'},
    {id:'p2', txt:'Existe un trato respetuoso entre los miembros del grupo.'},
    {id:'p3', txt:'Puedo participar u opinar sin miedo a burlas o juicios.'},
    {id:'p4', txt:'Sé a quién puedo acudir si tengo un problema.'},
    {id:'p5', txt:'Creo que hay buen clima de convivencia en este grupo.'},
    {id:'p6', txt:'Me siento seguro/a en los espacios comunes (patio, pasillos, redes).'},
  ];
  const P7 = {id:'p7', txt:'Hay algún compañero/a al que veo solo/a con frecuencia, o creo que lo pasa mal (presencial o por redes) y nadie se entera.'};

  const params = new URLSearchParams(location.search);
  const esAlumno = params.get('alumno') === '1';

  function toast(msg){
    const t = document.getElementById('toast');
    if(!t) return;
    t.textContent = msg; t.classList.add('show');
    setTimeout(()=>t.classList.remove('show'), 2200);
  }
  function avg(arr){ arr = arr.filter(v=>v!=null && !isNaN(v)); return arr.length ? arr.reduce((a,b)=>a+b,0)/arr.length : null; }
  function fmt(n){ return (n===null||n===undefined) ? '—' : n.toFixed(2); }
  function badgeFor(m){
    if(m===null) return '<span class="badge">Sin datos</span>';
    if(m>=4) return '<span class="badge ok">Clima positivo</span>';
    if(m>=3) return '<span class="badge warn">Zona de atención</span>';
    return '<span class="badge alert">Alarma</span>';
  }
  function avgRonda(ronda){
    const resp = ronda.respuestas ? Object.values(ronda.respuestas) : [];
    const medias = {};
    PREGUNTAS.forEach(p=> medias[p.id] = avg(resp.map(r=>r[p.id])) );
    medias.p7 = avg(resp.map(r=>r.p7));
    medias._n = resp.length;
    return medias;
  }

  /* ================= MODO ALUMNO ================= */
  if(esAlumno){
    document.getElementById('alumnoWrap').style.display = 'block';
    const wrap = document.getElementById('alumnoWrap');
    let step = 0; // 0 curso, 1 grupo, 2 ronda, 3 alumno, 4 preguntas, 5 gracias
    let sel = {curso:null, grupo:null, rondaId:null, ronda:null, alumnoId:null};
    let respuestas = {};

    db.ref('cursos').once('value').then(snap=>{
      const data = snap.val() || {};
      renderStep(data);
    });

    function progreso(){
      const total = 5;
      return `<div class="progressBar"><div class="fill" style="width:${(step/total)*100}%"></div></div>`;
    }

    function renderStep(data){
      if(step===0){
        const cursos = Object.keys(data).sort();
        wrap.innerHTML = `<h1>Clima de Aula</h1><div class="subtitle">Encuesta anónima — Salesianos Triana</div>${progreso()}
        <div class="stepCard">
          <label class="field">Elige tu curso académico</label>
          ${cursos.map(c=>`<button class="bigChoice" data-c="${c}">${c}</button>`).join('') || '<div class="empty">No hay cursos configurados todavía. Pídele a tu profesor que lo prepare.</div>'}
        </div>`;
        wrap.querySelectorAll('[data-c]').forEach(b=> b.onclick = ()=>{ sel.curso=b.dataset.c; step=1; renderStep(data); });
      }
      else if(step===1){
        const grupos = Object.keys(data[sel.curso]?.grupos||{}).sort();
        wrap.innerHTML = `<h1>Clima de Aula</h1><div class="subtitle">${sel.curso}</div>${progreso()}
        <div class="stepCard">
          <label class="field">Elige tu grupo</label>
          ${grupos.map(g=>`<button class="bigChoice" data-g="${g}">${data[sel.curso].grupos[g].nombre||g}</button>`).join('') || '<div class="empty">Este curso no tiene grupos todavía.</div>'}
          <button class="btnGhost" style="margin-top:10px;" onclick="location.reload()">← Volver</button>
        </div>`;
        wrap.querySelectorAll('[data-g]').forEach(b=> b.onclick = ()=>{ sel.grupo=b.dataset.g; step=2; renderStep(data); });
      }
      else if(step===2){
        const rondas = data[sel.curso].grupos[sel.grupo].rondas || {};
        const activas = Object.entries(rondas).filter(([id,r])=>r.activa);
        wrap.innerHTML = `<h1>Clima de Aula</h1><div class="subtitle">${data[sel.curso].grupos[sel.grupo].nombre}</div>${progreso()}
        <div class="stepCard">
          <label class="field">Encuesta disponible</label>
          ${activas.map(([id,r])=>`<button class="bigChoice" data-r="${id}">${r.titulo}</button>`).join('') || '<div class="empty">No hay ninguna encuesta abierta para tu grupo ahora mismo. Pregúntale a tu profesor/a.</div>'}
        </div>`;
        wrap.querySelectorAll('[data-r]').forEach(b=> b.onclick = ()=>{
          sel.rondaId=b.dataset.r; sel.ronda = rondas[sel.rondaId];
          const recordado = localStorage.getItem(`climaAula_${sel.curso}_${sel.grupo}`);
          const alumnos = data[sel.curso].grupos[sel.grupo].alumnos || {};
          if(recordado){
            const ru = JSON.parse(recordado);
            if(alumnos[ru.id] === ru.nombre){ sel.alumnoId = ru.id; sel.recordadoNombre = ru.nombre; step = 3.5; renderStep(data); return; }
          }
          step=3; renderStep(data);
        });
      }
      else if(step===3.5){
        const ya = (sel.ronda.participantes)||{};
        wrap.innerHTML = `<h1>Clima de Aula</h1><div class="subtitle">${sel.ronda.titulo}</div>${progreso()}
        <div class="stepCard">
          <label class="field">Este dispositivo está guardado como:</label>
          <div style="font-family:'Fraunces',serif;font-size:1.3rem;margin:8px 0 18px;color:var(--azulejo-dark);">${sel.recordadoNombre} ${ya[sel.alumnoId]?' · ya respondida ✓':''}</div>
          <button class="btnPrimary" style="width:100%;margin-top:0;" id="btnSoyYo">Sí, soy yo — continuar</button>
          <button class="btnGhost" style="width:100%;margin-top:10px;" id="btnNoSoyYo">No soy yo, elegir otro nombre</button>
        </div>`;
        document.getElementById('btnSoyYo').onclick = ()=>{
          db.ref(`cursos/${sel.curso}/grupos/${sel.grupo}/rondas/${sel.rondaId}/participantes/${sel.alumnoId}`).set(true);
          step=4; renderStep(data);
        };
        document.getElementById('btnNoSoyYo').onclick = ()=>{
          localStorage.removeItem(`climaAula_${sel.curso}_${sel.grupo}`);
          step=3; renderStep(data);
        };
      }
      else if(step===3){
        const alumnos = data[sel.curso].grupos[sel.grupo].alumnos || {};
        const ya = (sel.ronda.participantes)||{};
        wrap.innerHTML = `<h1>Clima de Aula</h1><div class="subtitle">${sel.ronda.titulo} — Tu respuesta es anónima, solo se registra que has participado</div>${progreso()}
        <div class="stepCard">
          <label class="field">¿Quién eres? (esto no se une a tus respuestas)</label>
          ${Object.entries(alumnos).sort((a,b)=>a[1].localeCompare(b[1])).map(([id,nombre])=>`<button class="bigChoice" data-a="${id}" ${ya[id]?'style="opacity:.45;"':''}>${nombre} ${ya[id]?' · ya respondida ✓':''}</button>`).join('') || '<div class="empty">Este grupo aún no tiene alumnado registrado.</div>'}
        </div>`;
        wrap.querySelectorAll('[data-a]').forEach(b=> b.onclick = ()=>{
          sel.alumnoId=b.dataset.a;
          localStorage.setItem(`climaAula_${sel.curso}_${sel.grupo}`, JSON.stringify({id:sel.alumnoId, nombre:alumnos[sel.alumnoId]}));
          db.ref(`cursos/${sel.curso}/grupos/${sel.grupo}/rondas/${sel.rondaId}/participantes/${sel.alumnoId}`).set(true);
          step=4; renderStep(data);
        });
      }
      else if(step===4){
        const qs = PREGUNTAS.map(p=>`
          <div class="scaleQ">
            <div class="qtext">${p.txt}</div>
            <div class="scaleBtns" data-q="${p.id}">
              ${[1,2,3,4,5].map(v=>`<button data-v="${v}">${v}</button>`).join('')}
            </div>
          </div>`).join('');
        wrap.innerHTML = `<h1>Clima de Aula</h1><div class="subtitle">1 = nunca/nada de acuerdo · 5 = siempre/totalmente de acuerdo</div>${progreso()}
        <div class="stepCard">
          ${qs}
          <div class="scaleQ discreta">
            <div class="qtext">🔎 ${P7.txt}</div>
            <div class="scaleBtns" data-q="p7">${[1,2,3,4,5].map(v=>`<button data-v="${v}">${v}</button>`).join('')}</div>
          </div>
          <label class="field">¿Algo que te gustaría contar o cambiar? (opcional)</label>
          <textarea id="notasAlumno" placeholder="Escribe aquí si quieres..."></textarea>
          <button class="btnPrimary" id="btnEnviar" disabled>Enviar encuesta</button>
        </div>`;
        wrap.querySelectorAll('.scaleBtns').forEach(box=>{
          box.querySelectorAll('button').forEach(btn=>{
            btn.onclick = ()=>{
              respuestas[box.dataset.q] = parseInt(btn.dataset.v);
              box.querySelectorAll('button').forEach(x=>x.classList.remove('sel'));
              btn.classList.add('sel');
              checkListo();
            };
          });
        });
        function checkListo(){
          const okAll = PREGUNTAS.every(p=>respuestas[p.id]) && respuestas.p7;
          document.getElementById('btnEnviar').disabled = !okAll;
        }
        document.getElementById('btnEnviar').onclick = ()=>{
          const notas = document.getElementById('notasAlumno').value.trim();
          const payload = {...respuestas, notas, ts: Date.now()};
          db.ref(`cursos/${sel.curso}/grupos/${sel.grupo}/rondas/${sel.rondaId}/respuestas`).push(payload)
            .then(()=>{ step=5; renderStep(data); });
        };
      }
      else if(step===5){
        wrap.innerHTML = `<h1>¡Gracias! 🙌</h1><div class="subtitle">Tu respuesta se ha enviado de forma anónima.</div>
        <div class="stepCard"><p>Ya puedes cerrar esta página.</p></div>`;
      }
    }
    return; // no seguir cargando el modo profesor
  }

  /* ================= MODO PROFESOR ================= */
  document.getElementById('app').style.display = 'flex';
  let data = {};
  let curso=null, grupo=null, view='resumen';
  let comparar = {curso:null, grupo:null};
  let chartInstance = null;

  db.ref('cursos').on('value', snap=>{
    data = snap.val() || {};
    if(!curso || !data[curso]) curso = Object.keys(data).sort()[0] || null;
    if(curso){
      const gs = Object.keys(data[curso].grupos||{});
      if(!grupo || !gs.includes(grupo)) grupo = gs.sort()[0] || null;
    } else grupo = null;
    render();
  });

  function cursosList(){ return Object.keys(data).sort(); }
  function gruposList(c){ return c && data[c] && data[c].grupos ? Object.keys(data[c].grupos).sort() : []; }
  function gData(){ return (curso && grupo && data[curso] && data[curso].grupos && data[curso].grupos[grupo]) ? data[curso].grupos[grupo] : null; }
  function gPath(){ return `cursos/${curso}/grupos/${grupo}`; }

  function refreshSelectors(){
    const selC = document.getElementById('selCurso');
    const cursos = cursosList();
    selC.innerHTML = cursos.map(c=>`<option value="${c}" ${c===curso?'selected':''}>${c}</option>`).join('') || '<option value="">— crea un curso —</option>';
    const selG = document.getElementById('selGrupo');
    const grupos = gruposList(curso);
    selG.innerHTML = grupos.map(g=>`<option value="${g}" ${g===grupo?'selected':''}>${(data[curso].grupos[g].nombre)||g}</option>`).join('') || '<option value="">— crea un grupo —</option>';
  }

  function viewResumen(){
    const grupos = gruposList(curso);
    if(!grupos.length) return `<h2>Resumen</h2><div class="subtitle">${curso||'Crea un curso académico'}</div><div class="empty">Aún no hay grupos en este curso.</div>`;
    const cards = grupos.map(g=>{
      const gd = data[curso].grupos[g];
      const rondas = Object.entries(gd.rondas||{});
      const nAlum = Object.keys(gd.alumnos||{}).length;
      let mg = null, alertas = 0, ultima = null;
      if(rondas.length){
        rondas.sort((a,b)=>(a[1].fecha||'').localeCompare(b[1].fecha||''));
        const last = rondas[rondas.length-1][1];
        const m = avgRonda(last);
        mg = avg(PREGUNTAS.map(p=>m[p.id]));
        ultima = last;
        alertas = rondas.filter(([id,r])=> (avgRonda(r).p7||0) >= 4).length;
      }
      return `<div class="statCard">
        <div class="grupoName">${gd.nombre||g}</div>
        <div class="num">${fmt(mg)}</div>
        <div class="lbl">Media última encuesta</div>
        ${badgeFor(mg)}
        <div style="margin-top:8px;font-size:.78rem;color:var(--ink-soft);">${nAlum} alumnos · ${rondas.length} rondas</div>
        ${ultima ? `<div style="font-size:.78rem;color:var(--ink-soft);">Participación: ${ultima.respuestas?Object.keys(ultima.respuestas).length:0}/${nAlum}</div>` : ''}
        ${alertas>0?`<div style="margin-top:6px;font-size:.78rem;color:var(--coral);">⚠ ${alertas} ronda(s) con señal de aislamiento</div>`:''}
      </div>`;
    }).join('');
    return `<h2>Resumen — ${curso}</h2><div class="subtitle">Vista rápida de todos los grupos</div><div class="cardGrid">${cards}</div>`;
  }

  function viewAlumnado(){
    const d = gData();
    if(!d) return `<h2>Alumnado</h2><div class="empty">Selecciona o crea un grupo primero.</div>`;
    const alumnos = d.alumnos || {};
    const rows = Object.entries(alumnos).sort((a,b)=>a[1].localeCompare(b[1]))
      .map(([id,nombre])=>`<tr><td>${nombre}</td><td><button class="btnGhost btnDanger" onclick="climaApp.delAlumno('${id}')">Eliminar</button></td></tr>`).join('');
    return `<h2>Alumnado — ${d.nombre}</h2>
    <div class="subtitle">Gestión del grupo. Las respuestas de la encuesta no se vinculan a estos nombres.</div>
    <div class="card">
      <div class="row"><div><label class="field">Añadir alumno/a</label><input type="text" id="nuevoAlumno" placeholder="Nombre y apellidos"></div></div>
      <button class="btnPrimary" onclick="climaApp.addAlumno()">Añadir</button>
    </div>
    <div class="card">${Object.keys(alumnos).length ? `<table><tr><th>Nombre</th><th></th></tr>${rows}</table>` : '<div class="empty">Sin alumnado registrado todavía.</div>'}</div>`;
  }

  function viewRondas(){
    const d = gData();
    if(!d) return `<h2>Encuesta trimestral</h2><div class="empty">Selecciona o crea un grupo primero.</div>`;
    const rondas = Object.entries(d.rondas||{}).sort((a,b)=>(b[1].fecha||'').localeCompare(a[1].fecha||''));
    const nAlum = Object.keys(d.alumnos||{}).length;
    const linkAlumno = `${location.origin}${location.pathname}?alumno=1`;
    const rows = rondas.map(([id,r])=>{
      const m = avgRonda(r);
      const mg = avg(PREGUNTAS.map(p=>m[p.id]));
      const nPart = Object.keys(r.participantes||{}).length;
      return `<div class="card">
        <div style="display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:8px;">
          <div><b>${r.titulo}</b> <span class="pill ${r.activa?'activa':''}">${r.activa?'Abierta':'Cerrada'}</span></div>
          <div style="display:flex;gap:8px;">
            ${r.activa ? `<button class="btnGhost" onclick="climaApp.cerrarRonda('${id}')">Cerrar</button>` : `<button class="btnGhost" onclick="climaApp.abrirRonda('${id}')">Reabrir</button>`}
            <button class="btnGhost btnDanger" onclick="climaApp.delRonda('${id}')">Eliminar</button>
          </div>
        </div>
        <div class="subtitle" style="margin:8px 0;">Participación: ${nPart}/${nAlum} alumnos · ${m._n} respuestas recogidas</div>
        <div class="row">
          <div><div class="num" style="font-family:'IBM Plex Mono',monospace;font-size:1.4rem;">${fmt(mg)}</div><div class="lbl">Media global</div></div>
          <div><div class="num" style="font-family:'IBM Plex Mono',monospace;font-size:1.4rem;color:${m.p7>=4?'var(--coral)':'inherit'};">${fmt(m.p7)}</div><div class="lbl">P.7 alerta</div></div>
        </div>
        ${badgeFor(mg)}
      </div>`;
    }).join('');
    return `<h2>Encuesta trimestral — ${d.nombre}</h2>
    <div class="subtitle">Crea una ronda por trimestre y compártela con tu alumnado</div>
    <div class="card">
      <label class="field">Nueva ronda (ej: Trimestre 1)</label>
      <div style="display:flex;gap:8px;">
        <input type="text" id="inputRonda" placeholder="Ej: Trimestre 1" style="max-width:260px;">
        <button class="btnPrimary" style="margin:0;" onclick="climaApp.crearRonda()">Crear y abrir</button>
      </div>
      <div class="subtitle" style="margin-top:14px;margin-bottom:0;">Enlace para el alumnado (funciona para todos los grupos y rondas abiertas):</div>
      <div style="display:flex;gap:8px;align-items:center;margin-top:6px;">
        <input type="text" id="linkAlumno" value="${linkAlumno}" readonly style="max-width:400px;">
        <button class="btnGhost" onclick="climaApp.copiarLink()">Copiar enlace</button>
      </div>
    </div>
    ${rows || '<div class="empty">Sin rondas todavía. Crea la primera arriba.</div>'}`;
  }

  function viewSemaforo(){
    const d = gData();
    if(!d) return `<h2>Semáforo semanal</h2><div class="empty">Selecciona o crea un grupo primero.</div>`;
    const items = [{id:'relacion',txt:'Relación entre compañeros/as'},{id:'bienestar',txt:'Bienestar / seguridad'},{id:'participacion',txt:'Participación en clase'}];
    const blocks = items.map(it=>`
      <div style="margin-bottom:14px;">
        <div class="qtext" style="margin-bottom:4px;">${it.txt}</div>
        <div class="semaforoBtns" id="tile_${it.id}">
          <div class="tile" data-val="verde" onclick="climaApp.setTile('${it.id}','verde')">🟢</div>
          <div class="tile" data-val="amarillo" onclick="climaApp.setTile('${it.id}','amarillo')">🟡</div>
          <div class="tile" data-val="rojo" onclick="climaApp.setTile('${it.id}','rojo')">🔴</div>
        </div>
      </div>`).join('');
    const semaforos = Object.entries(d.semaforos||{}).sort((a,b)=>(b[1].fecha||'').localeCompare(a[1].fecha||''));
    const semColor = {verde:'🟢',amarillo:'🟡',rojo:'🔴'};
    const rows = semaforos.map(([id,s])=>`<tr><td>${s.fecha}</td><td>${semColor[s.relacion]||'—'}</td><td>${semColor[s.bienestar]||'—'}</td><td>${semColor[s.participacion]||'—'}</td><td><button class="btnGhost btnDanger" onclick="climaApp.delSemaforo('${id}')">Eliminar</button></td></tr>`).join('');
    return `<h2>Semáforo semanal — ${d.nombre}</h2>
    <div class="subtitle">Chequeo rápido del profesor, 1 minuto por semana</div>
    <div class="card">
      <label class="field">Fecha</label>
      <input type="date" id="fechaSemaforo" value="${new Date().toISOString().slice(0,10)}" style="max-width:200px;">
      ${blocks}
      <button class="btnPrimary" onclick="climaApp.guardarSemaforo()">Guardar semáforo</button>
    </div>
    <div class="card"><b>Histórico</b>${semaforos.length?`<table><tr><th>Fecha</th><th>Relación</th><th>Bienestar</th><th>Participación</th><th></th></tr>${rows}</table>`:'<div class="empty">Sin registros todavía.</div>'}</div>`;
  }

  function viewEvolucion(){
    const d = gData();
    if(!d) return `<h2>Evolución</h2><div class="empty">Selecciona o crea un grupo primero.</div>`;
    const rondas = Object.entries(d.rondas||{}).sort((a,b)=>(a[1].fecha||'').localeCompare(b[1].fecha||''));
    if(!rondas.length) return `<h2>Evolución — ${d.nombre}</h2><div class="empty">Necesitas al menos una ronda con respuestas para ver la evolución.</div>`;
    return `<h2>Evolución — ${d.nombre}</h2>
    <div class="subtitle">Media global y señal de alerta a lo largo de las rondas</div>
    <div class="card"><canvas id="chartEvo" height="90"></canvas><div class="legend" id="chartLegend"></div></div>
    <div class="card">
      <b>Comparar con otro curso/grupo</b>
      <div class="subtitle">Se alinean por número de ronda (1ª, 2ª, 3ª...)</div>
      <div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:8px;">
        <select class="formSel" id="selCompararCurso" style="max-width:220px;">
          <option value="">— ninguno —</option>
          ${cursosList().map(c=>`<option value="${c}" ${c===comparar.curso?'selected':''}>${c}${c===curso?' (este curso)':''}</option>`).join('')}
        </select>
        <select class="formSel" id="selCompararGrupo" style="max-width:220px;"><option value="">grupo…</option></select>
        <button class="btnGhost" onclick="climaApp.quitarComparacion()">Quitar comparación</button>
      </div>
      <div id="compararMsg" style="margin-top:10px;font-size:.85rem;"></div>
    </div>`;
  }

  function drawChart(){
    const canvas = document.getElementById('chartEvo');
    if(!canvas) return;
    const d = gData();
    const rondas = Object.entries(d.rondas||{}).sort((a,b)=>(a[1].fecha||'').localeCompare(b[1].fecha||''));
    const labels = rondas.map((r,i)=>`Ronda ${i+1}`);
    const medias = rondas.map(([id,r])=>{ const m=avgRonda(r); return avg(PREGUNTAS.map(p=>m[p.id])); });
    const p7 = rondas.map(([id,r])=> avgRonda(r).p7);
    const datasets = [
      {label:`${d.nombre} · Media global`, data:medias, borderColor:'#2B5876', backgroundColor:'#2B5876', tension:.25, spanGaps:true},
      {label:`${d.nombre} · P.7 alerta`, data:p7, borderColor:'#B5533C', backgroundColor:'#B5533C', tension:.25, spanGaps:true, borderDash:[4,3]},
    ];
    let finalLabels = labels;
    const msgBox = document.getElementById('compararMsg');
    if(comparar.curso && comparar.grupo && data[comparar.curso] && data[comparar.curso].grupos[comparar.grupo]){
      const cd = data[comparar.curso].grupos[comparar.grupo];
      const cRondas = Object.entries(cd.rondas||{}).sort((a,b)=>(a[1].fecha||'').localeCompare(b[1].fecha||''));
      if(!cRondas.length){
        if(msgBox) msgBox.innerHTML = `⚠️ <b>${cd.nombre}</b> (${comparar.curso}) todavía no tiene rondas con datos.`;
      } else {
        const cMedias = cRondas.map(([id,r])=>{ const m=avgRonda(r); return avg(PREGUNTAS.map(p=>m[p.id])); });
        const cP7 = cRondas.map(([id,r])=> avgRonda(r).p7);
        const maxLen = Math.max(labels.length, cMedias.length);
        finalLabels = Array.from({length:maxLen},(_, i)=>`Ronda ${i+1}`);
        datasets.push({label:`${cd.nombre} (${comparar.curso}) · Media global`, data:cMedias, borderColor:'#6E8B5A', backgroundColor:'#6E8B5A', tension:.25, spanGaps:true});
        datasets.push({label:`${cd.nombre} (${comparar.curso}) · P.7 alerta`, data:cP7, borderColor:'#C98A2E', backgroundColor:'#C98A2E', tension:.25, spanGaps:true, borderDash:[4,3]});
        if(msgBox) msgBox.innerHTML = `✅ Comparando con <b>${cd.nombre}</b> (${comparar.curso}) — ${cRondas.length} ronda(s).`;
      }
    } else if(msgBox){ msgBox.innerHTML = comparar.curso ? 'Elige también un grupo de ese curso.' : ''; }

    if(chartInstance) chartInstance.destroy();
    chartInstance = new Chart(canvas.getContext('2d'), {
      type:'line', data:{labels:finalLabels, datasets}, options:{scales:{y:{min:0,max:5}}, plugins:{legend:{display:false}}}
    });
    const legend = document.getElementById('chartLegend');
    if(legend) legend.innerHTML = datasets.map(ds=>`<span><span class="dot" style="background:${ds.borderColor}"></span>${ds.label}</span>`).join('');
  }

  function bindComparar(){
    const sc = document.getElementById('selCompararCurso');
    if(!sc) return;
    const sg = document.getElementById('selCompararGrupo');
    function gruposDisponibles(c){ return gruposList(c).filter(g => !(c===curso && g===grupo)); }
    if(comparar.curso) sg.innerHTML = '<option value="">grupo…</option>' + gruposDisponibles(comparar.curso).map(g=>`<option value="${g}" ${g===comparar.grupo?'selected':''}>${data[comparar.curso].grupos[g].nombre}</option>`).join('');
    sc.onchange = ()=>{
      comparar.curso = sc.value || null; comparar.grupo = null;
      sg.innerHTML = '<option value="">grupo…</option>' + gruposDisponibles(comparar.curso).map(g=>`<option value="${g}">${data[comparar.curso].grupos[g].nombre}</option>`).join('');
      drawChart();
    };
    sg.onchange = ()=>{ comparar.grupo = sg.value || null; drawChart(); };
  }

  function viewAlertas(){
    let rows = [];
    for(const c of cursosList()){
      for(const g of gruposList(c)){
        const gd = data[c].grupos[g];
        Object.entries(gd.rondas||{}).forEach(([id,r])=>{
          const m = avgRonda(r);
          if((m.p7||0) >= 4) rows.push({curso:c, grupo:gd.nombre, ronda:r.titulo, valor:m.p7, n:m._n});
        });
      }
    }
    if(!rows.length) return `<h2>Alertas</h2><div class="empty">No hay rondas con señal de posible aislamiento/acoso (P.7 ≥ 4) registradas.</div>`;
    const body = rows.map(r=>`<tr><td>${r.curso}</td><td>${r.grupo}</td><td>${r.ronda}</td><td style="color:var(--coral);font-weight:600;">${fmt(r.valor)}</td><td>${r.n} respuestas</td></tr>`).join('');
    return `<h2>Alertas — todos los cursos</h2>
    <div class="subtitle">Rondas donde la pregunta discreta obtuvo una media ≥ 4. Revisa aunque el resto del grupo vaya bien.</div>
    <div class="card"><table><tr><th>Curso</th><th>Grupo</th><th>Ronda</th><th>P.7</th><th>Respuestas</th></tr>${body}</table></div>`;
  }

  function render(){
    if(!curso){ document.getElementById('main').innerHTML = `<h2>Bienvenido</h2><div class="empty">Crea tu primer curso académico en el panel lateral para empezar.</div>`; return; }
    refreshSelectors();
    document.querySelectorAll('#nav button').forEach(b=>b.classList.toggle('active', b.dataset.view===view));
    const main = document.getElementById('main');
    if(view==='resumen') main.innerHTML = viewResumen();
    else if(view==='alumnado') main.innerHTML = viewAlumnado();
    else if(view==='rondas') main.innerHTML = viewRondas();
    else if(view==='semaforo') main.innerHTML = viewSemaforo();
    else if(view==='evolucion'){ main.innerHTML = viewEvolucion(); setTimeout(drawChart,0); bindComparar(); }
    else if(view==='alertas') main.innerHTML = viewAlertas();
  }

  const semTemp = {};
  window.climaApp = {
    addAlumno(){
      const inp = document.getElementById('nuevoAlumno');
      const v = inp.value.trim();
      if(!v) return;
      db.ref(`${gPath()}/alumnos`).push(v).then(()=> toast('Alumno/a añadido/a'));
    },
    delAlumno(id){ db.ref(`${gPath()}/alumnos/${id}`).remove().then(()=> toast('Eliminado')); },
    crearRonda(){
      const inp = document.getElementById('inputRonda');
      const t = inp.value.trim();
      if(!t){ toast('Escribe un nombre para la ronda'); return; }
      db.ref(`${gPath()}/rondas`).push({titulo:t, fecha:new Date().toISOString().slice(0,10), activa:true})
        .then(()=>{ inp.value=''; toast('Ronda creada y abierta'); });
    },
    cerrarRonda(id){ db.ref(`${gPath()}/rondas/${id}/activa`).set(false).then(()=> toast('Ronda cerrada')); },
    abrirRonda(id){ db.ref(`${gPath()}/rondas/${id}/activa`).set(true).then(()=> toast('Ronda reabierta')); },
    delRonda(id){ db.ref(`${gPath()}/rondas/${id}`).remove().then(()=> toast('Ronda eliminada')); },
    copiarLink(){
      const inp = document.getElementById('linkAlumno');
      inp.select(); document.execCommand('copy');
      toast('Enlace copiado');
    },
    setTile(campo,val){
      semTemp[campo]=val;
      const box = document.getElementById('tile_'+campo);
      box.querySelectorAll('.tile').forEach(t=>{
        t.classList.remove('sel-green','sel-amber','sel-red');
        if(t.dataset.val===val) t.classList.add(val==='verde'?'sel-green':val==='amarillo'?'sel-amber':'sel-red');
      });
    },
    guardarSemaforo(){
      const fecha = document.getElementById('fechaSemaforo').value;
      const rec = {fecha, relacion:semTemp.relacion||null, bienestar:semTemp.bienestar||null, participacion:semTemp.participacion||null};
      db.ref(`${gPath()}/semaforos`).push(rec).then(()=>{ toast('Semáforo guardado'); Object.keys(semTemp).forEach(k=>delete semTemp[k]); });
    },
    delSemaforo(id){ db.ref(`${gPath()}/semaforos/${id}`).remove().then(()=> toast('Eliminado')); },
    quitarComparacion(){ comparar={curso:null,grupo:null}; render(); },
  };

  document.getElementById('nav').addEventListener('click', e=>{
    const b = e.target.closest('button[data-view]');
    if(!b) return;
    view = b.dataset.view; render();
  });
  document.getElementById('selCurso').addEventListener('change', e=>{ curso=e.target.value; grupo=null; comparar={curso:null,grupo:null}; render(); });
  document.getElementById('selGrupo').addEventListener('change', e=>{ grupo=e.target.value; comparar={curso:null,grupo:null}; render(); });
  document.getElementById('btnNuevoCurso').addEventListener('click', ()=>{
    const inp = document.getElementById('inputNuevoCurso');
    const c = inp.value.trim();
    if(!c){ toast('Escribe primero el nombre del curso'); return; }
    db.ref(`cursos/${c}/creado`).set(true).then(()=>{ curso=c; grupo=null; inp.value=''; toast('Curso creado: '+c); });
  });
  document.getElementById('btnNuevoGrupo').addEventListener('click', ()=>{
    if(!curso){ toast('Crea primero un curso académico.'); return; }
    const inp = document.getElementById('inputNuevoGrupo');
    const g = inp.value.trim();
    if(!g){ toast('Escribe primero el nombre del grupo'); return; }
    db.ref(`cursos/${curso}/grupos/${g}/nombre`).set(g).then(()=>{ grupo=g; inp.value=''; toast('Grupo creado: '+g); });
  });
})();
