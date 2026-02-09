<!doctype html>
<html lang="fr">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Will you be my Valentine?</title>
  <style>
    :root{
      --bg1:#ffdde1;
      --bg2:#ee9ca7;
      --card:#ffffffcc;
      --text:#222;
      --yes:#22c55e;
      --yesHover:#16a34a;
      --no:#ef4444;
      --noHover:#dc2626;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      min-height:100vh;
      display:flex;
      justify-content:center;
      align-items:center;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      background: radial-gradient(circle at top, var(--bg1), var(--bg2));
      overflow:hidden;
    }
    .card{
      width:min(520px, 92vw);
      padding:28px 22px;
      border-radius:18px;
      background: var(--card);
      backdrop-filter: blur(10px);
      box-shadow: 0 20px 60px rgba(0,0,0,.18);
      text-align:center;
      position:relative;
    }
    h1{
      margin:0 0 10px;
      font-size: clamp(24px, 4vw, 36px);
      color:var(--text);
    }
    p{margin:0 0 18px; color:#333}
    .gif{
      width: 240px;
      height: 240px;
      margin: 14px auto 18px;
      border-radius: 16px;
      background: #fff;
      display:flex;
      align-items:center;
      justify-content:center;
      overflow:hidden;
      box-shadow: 0 10px 30px rgba(0,0,0,.12);
    }
    .gif img{
      width:100%;
      height:100%;
      object-fit:cover;
    }

    .btns{
      display:flex;
      gap:12px;
      justify-content:center;
      align-items:center;
      margin-top:14px;
      position:relative;
      height:56px;
    }
    button{
      border:0;
      cursor:pointer;
      padding:14px 20px;
      border-radius:999px;
      font-weight:700;
      font-size:16px;
      transition: transform .12s ease, background .12s ease;
      user-select:none;
      touch-action: manipulation;
    }
    #yesBtn{
      background:var(--yes);
      color:white;
    }
    #yesBtn:hover{background:var(--yesHover); transform: translateY(-1px)}
    #noBtn{
      background:var(--no);
      color:white;
      position:absolute; /* pour pouvoir le déplacer */
      left: 50%;
      transform: translateX(140px); /* position de départ à droite du yes */
    }
    #noBtn:hover{background:var(--noHover)}

    .footer{
      margin-top:18px;
      font-size:12px;
      color:#444;
      opacity:.85;
    }

    /* petits coeurs en fond */
    .heart{
      position:absolute;
      width:14px; height:14px;
      transform: rotate(45deg);
      background: rgba(255,255,255,.65);
      border-radius: 2px;
      animation: float 6s linear infinite;
      pointer-events:none;
    }
    .heart::before, .heart::after{
      content:"";
      position:absolute;
      width:14px; height:14px;
      background: inherit;
      border-radius:50%;
    }
    .heart::before{ left:-7px; top:0; }
    .heart::after{ left:0; top:-7px; }

    @keyframes float{
      from{ transform: translateY(40vh) rotate(45deg); opacity:.0; }
      10%{opacity:.7}
      to{ transform: translateY(-70vh) rotate(45deg); opacity:0; }
    }

    /* écran final */
    .hidden{display:none}
    .big{
      font-size: clamp(22px, 4vw, 34px);
      font-weight:900;
      margin-top:8px;
    }
  </style>
</head>
<body>

  <div class="card" id="screen1">
    <h1>Will you be my Valentine? 💘</h1>
    <p>Allez… dis oui 😌</p>

    <div class="gif">
      <!-- Remplace par ton gif / image -->
      <img src="https://media.giphy.com/media/MDJ9IbxxvDUQM/giphy.gif" alt="cute" />
    </div>

    <div class="btns" id="btnArea">
      <button id="yesBtn">Yes</button>
      <button id="noBtn">No</button>
    </div>

    <div class="footer">PS : le bouton “No” est un petit filou 😈</div>
  </div>

  <div class="card hidden" id="screen2">
    <h1>Yeeeees!! 💖</h1>
    <div class="gif">
      <img src="https://media.giphy.com/media/l0MYt5jPR6QX5pnqM/giphy.gif" alt="yay" />
    </div>
    <div class="big">Rendez-vous le 14 ? 🥰</div>
    <p style="margin-top:10px;">(Tu peux changer ce texte par ton message.)</p>
  </div>

  <script>
    const noBtn = document.getElementById("noBtn");
    const yesBtn = document.getElementById("yesBtn");
    const btnArea = document.getElementById("btnArea");
    const screen1 = document.getElementById("screen1");
    const screen2 = document.getElementById("screen2");

    // coeurs en fond
    function spawnHearts(){
      const h = document.createElement("div");
      h.className = "heart";
      h.style.left = Math.random()*100 + "vw";
      h.style.animationDuration = (4 + Math.random()*5) + "s";
      h.style.opacity = (0.3 + Math.random()*0.6);
      document.body.appendChild(h);
      setTimeout(()=>h.remove(), 9000);
    }
    setInterval(spawnHearts, 350);

    // déplacement du bouton "No" dans la zone des boutons
    function moveNo(){
      const rect = btnArea.getBoundingClientRect();
      const btnRect = noBtn.getBoundingClientRect();

      // marges pour éviter que ça sorte de la zone
      const padding = 6;
      const maxX = rect.width - btnRect.width - padding;
      const maxY = rect.height - btnRect.height - padding;

      const x = padding + Math.random() * maxX;
      const y = padding + Math.random() * maxY;

      // position absolue dans btnArea
      noBtn.style.left = x + "px";
      noBtn.style.top  = y + "px";
      noBtn.style.transform = "none";
    }

    // Sur desktop: dès que la souris approche / survole
    noBtn.addEventListener("mouseenter", moveNo);

    // Sur mobile: dès qu'on touche (sinon c'est trop facile)
    noBtn.addEventListener("touchstart", (e)=> {
      e.preventDefault();
      moveNo();
    }, {passive:false});

    // Clique Yes => écran final
    yesBtn.addEventListener("click", ()=>{
      screen1.classList.add("hidden");
      screen2.classList.remove("hidden");
      // petite pluie de coeurs
      for(let i=0;i<20;i++) setTimeout(spawnHearts, i*60);
    });

    // Option: si jamais il arrive à cliquer No (rare), tu peux faire un message:
    noBtn.addEventListener("click", ()=>{
      // moveNo(); // ou affiche un toast, ou change le texte
      moveNo();
    });
  </script>
</body>
</html>
