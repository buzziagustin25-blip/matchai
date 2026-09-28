<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>MatchAI — Tu agente laboral</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: Arial, Helvetica, sans-serif;
      background: #08090d;
      color: #fff;
      min-height: 100vh;
    }

    .container {
      width: min(1100px, 92%);
      margin: auto;
    }

    nav {
      height: 80px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .logo {
      font-size: 25px;
      font-weight: 800;
    }

    .logo span {
      color: #8b6cff;
    }

    .badge {
      border: 1px solid #302b48;
      background: #14121d;
      color: #b8adff;
      padding: 8px 14px;
      border-radius: 30px;
      font-size: 13px;
    }

    .hero {
      text-align: center;
      padding: 80px 10px 60px;
    }

    .tag {
      display: inline-block;
      padding: 8px 15px;
      border-radius: 30px;
      border: 1px solid #302b48;
      background: #14121d;
      color: #b8adff;
      margin-bottom: 25px;
      font-size: 14px;
    }

    h1 {
      font-size: clamp(45px, 7vw, 80px);
      line-height: .98;
      letter-spacing: -4px;
      max-width: 900px;
      margin: auto;
    }

    h1 span {
      color: #8b6cff;
    }

    .subtitle {
      max-width: 650px;
      margin: 30px auto;
      color: #9da0ac;
      font-size: 18px;
      line-height: 1.6;
    }

    .buttons {
      display: flex;
      justify-content: center;
      gap: 15px;
      flex-wrap: wrap;
      margin-top: 35px;
    }

    button {
      cursor: pointer;
      border: none;
      border-radius: 12px;
      padding: 16px 25px;
      font-size: 15px;
      font-weight: 700;
      transition: .2s;
    }

    button:hover {
      transform: translateY(-2px);
    }

    .primary {
      background: #7c5cff;
      color: white;
    }

    .secondary {
      background: #15161c;
      color: white;
      border: 1px solid #30323c;
    }

    .features {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 18px;
      margin: 30px 0 80px;
    }

    .feature {
      background: #111217;
      border: 1px solid #252731;
      border-radius: 18px;
      padding: 28px;
    }

    .feature-icon {
      font-size: 30px;
      margin-bottom: 15px;
    }

    .feature h3 {
      margin-bottom: 10px;
    }

    .feature p {
      color: #8f929e;
      line-height: 1.6;
      font-size: 14px;
    }

    /* PANTALLAS */

    .screen {
      display: none;
      padding: 50px 0 100px;
    }

    .screen.active {
      display: block;
    }

    .back {
      background: transparent;
      border: 1px solid #30323c;
      color: #aaa;
      margin-bottom: 30px;
    }

    .screen-title {
      font-size: 42px;
      margin-bottom: 10px;
    }

    .screen-subtitle {
      color: #9295a2;
      margin-bottom: 35px;
      line-height: 1.6;
    }

    .form {
      max-width: 750px;
      margin: auto;
      background: #111217;
      border: 1px solid #292b35;
      border-radius: 22px;
      padding: 30px;
    }

    .field {
      margin-bottom: 22px;
    }

    .field label {
      display: block;
      font-weight: 700;
      margin-bottom: 9px;
    }

    .field small {
      display: block;
      color: #777b88;
      margin-bottom: 9px;
    }

    input,
    textarea,
    select {
      width: 100%;
      background: #090a0e;
      color: white;
      border: 1px solid #30323c;
      border-radius: 10px;
      padding: 14px;
      font-size: 15px;
      outline: none;
    }

    textarea {
      min-height: 110px;
      resize: vertical;
    }

    input:focus,
    textarea:focus,
    select:focus {
      border-color: #7c5cff;
    }

    .analyze {
      width: 100%;
      margin-top: 10px;
      background: #7c5cff;
      color: white;
      padding: 18px;
    }

    /* RESULTADO */

    .result {
      display: none;
      max-width: 850px;
      margin: 30px auto 0;
    }

    .result.active {
      display: block;
    }

    .result-header {
      text-align: center;
      padding: 35px;
      background: linear-gradient(135deg, #151222, #111217);
      border: 1px solid #332b55;
      border-radius: 22px;
      margin-bottom: 18px;
    }

    .ai {
      color: #b8adff;
      font-size: 14px;
      margin-bottom: 10px;
    }

    .result-header h2 {
      font-size: 32px;
    }

    .matches {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 15px;
    }

    .match-card {
      background: #111217;
      border: 1px solid #292b35;
      border-radius: 17px;
      padding: 23px;
    }

    .match-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 15px;
    }

    .score {
      color: #8b6cff;
      font-size: 22px;
      font-weight: 800;
    }

    .match-card p {
      color: #898c98;
      font-size: 14px;
      line-height: 1.6;
    }

    .restart {
      margin-top: 25px;
      width: 100%;
    }

    footer {
      border-top: 1px solid #202129;
      padding: 30px 0;
      text-align: center;
      color: #656874;
      font-size: 13px;
    }

    @media(max-width: 700px) {
      .features,
      .matches {
        grid-template-columns: 1fr;
      }

      h1 {
        letter-spacing: -2px;
      }

      .screen-title {
        font-size: 32px;
      }
    }
  </style>
</head>

<body>

<div class="container">

  <nav>
    <div class="logo">Match<span>AI</span></div>
    <div class="badge">🤖 Tu agente laboral</div>
  </nav>

  <!-- INICIO -->

  <section id="home" class="screen active">

    <div class="hero">

      <div class="tag">
        Inteligencia artificial para conectar talento
      </div>

      <h1>
        Encontrá el trabajo correcto.<br>
        <span>Encontrá la persona correcta.</span>
      </h1>

      <p class="subtitle">
        MatchAI entiende lo que buscás, analiza tus habilidades
        y conecta personas y empresas según compatibilidad real.
      </p>

      <div class="buttons">

        <button class="primary" onclick="showScreen('worker')">
          👨‍💻 Busco trabajo
        </button>

        <button class="secondary" onclick="showScreen('company')">
          🏢 Busco empleados
        </button>

      </div>

    </div>

    <div class="features">

      <div class="feature">
        <div class="feature-icon">🧠</div>
        <h3>La IA te entiende</h3>
        <p>
          No necesitás saber qué puesto buscar.
          Contale a MatchAI qué sabés hacer y qué querés.
        </p>
      </div>

      <div class="feature">
        <div class="feature-icon">🎯</div>
        <h3>Matching inteligente</h3>
        <p>
          Comparamos experiencia, habilidades, horarios,
          salario y preferencias.
        </p>
      </div>

      <div class="feature">
        <div class="feature-icon">🤝</div>
        <h3>Conectamos las dos partes</h3>
        <p>
          Personas encuentran oportunidades y empresas
          encuentran talento.
        </p>
      </div>

    </div>

  </section>


  <!-- TRABAJADOR -->

  <section id="worker" class="screen">

    <button class="back" onclick="showScreen('home')">
      ← Volver
    </button>

    <h2 class="screen-title">
      👨‍💻 Contale a MatchAI quién sos
    </h2>

    <p class="screen-subtitle">
      No necesitás saber qué puesto buscar.
      Nosotros analizamos tu perfil y buscamos qué oportunidades
      pueden encajar con vos.
    </p>

    <div class="form">

      <div class="field">
        <label>¿Qué sabés hacer?</label>
        <small>Contanos tus habilidades, aunque no tengas un título.</small>
        <textarea id="skills"
          placeholder="Ej: atención al cliente, ventas, electricidad, cámaras, computación..."></textarea>
      </div>

      <div class="field">
        <label>¿Qué experiencia tenés?</label>
        <textarea id="experience"
          placeholder="Contanos qué trabajos hiciste y qué tareas realizabas."></textarea>
      </div>

      <div class="field">
        <label>¿Qué tipo de trabajo te gustaría hacer?</label>
        <input id="desired"
          placeholder="Ej: soporte técnico, atención al cliente, ventas...">
      </div>

      <div class="field">
        <label>¿Cuánto querés ganar por mes?</label>
        <input id="salary"
          placeholder="Ej: USD 800">
      </div>

      <div class="field">
        <label>¿Cuántas horas por semana podés trabajar?</label>
        <input id="hours"
          placeholder="Ej: 25">
      </div>

      <div class="field">
        <label>¿Cómo querés trabajar?</label>

        <select id="mode">
          <option>Remoto</option>
          <option>Presencial</option>
          <option>Remoto o presencial</option>
        </select>
      </div>

      <div class="field">
        <label>Idiomas</label>
        <input id="languages"
          placeholder="Ej: Español nativo, Inglés B2">
      </div>

      <div class="field">
        <label>¿Qué NO querés hacer?</label>
        <textarea id="avoid"
          placeholder="Ej: llamadas telefónicas, ventas puerta a puerta, horarios nocturnos..."></textarea>
      </div>

      <button class="analyze" onclick="analyzeWorker()">
        🤖 ANALIZAR MI PERFIL
      </button>

    </div>

    <div id="workerResult" class="result"></div>

  </section>


  <!-- EMPRESA -->

  <section id="company" class="screen">

    <button class="back" onclick="showScreen('home')">
      ← Volver
    </button>

    <h2 class="screen-title">
      🏢 Contale a MatchAI qué persona necesitás
    </h2>

    <p class="screen-subtitle">
      Describí la necesidad de tu empresa con tus propias palabras.
      La IA transforma la necesidad en una búsqueda inteligente.
    </p>

    <div class="form">

      <div class="field">
        <label>¿Qué necesitás?</label>

        <textarea id="companyNeed"
          placeholder="Ej: necesito una persona para atender clientes por chat y email..."></textarea>
      </div>

      <div class="field">
        <label>Habilidades obligatorias</label>

        <textarea id="companySkills"
          placeholder="Ej: inglés, atención al cliente, Zendesk..."></textarea>
      </div>

      <div class="field">
        <label>Presupuesto mensual</label>

        <input id="companySalary"
          placeholder="Ej: USD 800–1000">
      </div>

      <div class="field">
        <label>Horas semanales</label>

        <input id="companyHours"
          placeholder="Ej: 25">
      </div>

      <button class="analyze" onclick="analyzeCompany()">
        🤖 ENCONTRAR TALENTO
      </button>

    </div>

    <div id="companyResult" class="result"></div>

  </section>


  <footer>
    MatchAI © 2026 — Tu agente laboral.
  </footer>

</div>


<script>

function showScreen(screen) {

  document.querySelectorAll(".screen").forEach(function(section) {
    section.classList.remove("active");
  });

  document.getElementById(screen).classList.add("active");

  window.scrollTo({
    top: 0,
    behavior: "smooth"
  });
}


function analyzeWorker() {

  const skills = document.getElementById("skills").value;
  const experience = document.getElementById("experience").value;
  const desired = document.getElementById("desired").value;
  const salary = document.getElementById("salary").value;
  const hours = document.getElementById("hours").value;
  const mode = document.getElementById("mode").value;
  const languages = document.getElementById("languages").value;
  const avoid = document.getElementById("avoid").value;

  if (!skills || !experience || !desired) {
    alert("Completá al menos qué sabés hacer, tu experiencia y qué tipo de trabajo buscás.");
    return;
  }

  const profile = {
    skills,
    experience,
    desired,
    salary,
    hours,
    mode,
    languages,
    avoid
  };

  localStorage.setItem("matchai_worker_profile", JSON.stringify(profile));

  document.getElementById("workerResult").innerHTML = `

    <div class="result-header">

      <div class="ai">🤖 MATCHAI ANALIZÓ TU PERFIL</div>

      <h2>Encontramos posibles caminos laborales</h2>

      <div class="score">Perfil creado ✓</div>

      <p>
        La próxima versión conectará este perfil con ofertas reales
        y calculará automáticamente la compatibilidad.
      </p>

    </div>

    <div class="matches">

      <div class="match-card">
        <div class="match-top">
          <strong>Customer Support</strong>
          <span class="score">94%</span>
        </div>

        <p>
          Atención de clientes por chat y email.
          Compatible con trabajo remoto y experiencia transferible.
        </p>
      </div>

      <div class="match-card">
        <div class="match-top">
          <strong>Technical Support</strong>
          <span class="score">91%</span>
        </div>

        <p>
          Resolución de problemas técnicos y asistencia
          a usuarios mediante sistemas de tickets.
        </p>
      </div>

      <div class="match-card">
        <div class="match-top">
          <strong>Operations Assistant</strong>
          <span class="score">84%</span>
        </div>

        <p>
          Organización, seguimiento de tareas y soporte
          operativo para empresas.
        </p>
      </div>

      <div class="match-card">
        <div class="match-top">
          <strong>Virtual Assistant</strong>
          <span class="score">79%</span>
        </div>

        <p>
          Administración, seguimiento de clientes y
          tareas digitales remotas.
        </p>
      </div>

    </div>

    <button class="secondary restart"
      onclick="showScreen('home')">
      ← Volver al inicio
    </button>
  `;

  document.getElementById("workerResult").classList.add("active");

  document.getElementById("workerResult")
    .scrollIntoView({ behavior: "smooth" });
}


function analyzeCompany() {

  const need = document.getElementById("companyNeed").value;

  if (!need) {
    alert("Contanos primero qué persona necesitás.");
    return;
  }

  document.getElementById("companyResult").innerHTML = `

    <div class="result-header">

      <div class="ai">🤖 MATCHAI ANALIZÓ TU NECESIDAD</div>

      <h2>Búsqueda creada ✓</h2>

      <div class="score">Matching listo</div>

      <p>
        En la próxima versión la IA podrá comparar esta búsqueda
        contra nuestra base de candidatos y presentar los perfiles
        más compatibles.
      </p>

    </div>

    <div class="
