<!doctype html>
<html lang="fr">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Valentine</title>

  <style>
    :root{
      --bg1:#ffe6ef;
      --bg2:#ffb3c7;
      --card:#ffffffcc;
      --text:#1f1f1f;
      --yes:#22c55e;
      --no:#ef4444;
    }

    *{box-sizing:border-box}

    body{
      margin:0;
      min-height:100vh;
      display:flex;
      justify-content:center;
      align-items:center;
      font-family: system-ui, Arial, sans-serif;
      background: radial-gradient(circle at top, var(--bg1), var(--bg2));
      overflow:hidden;
    }

    .card{
      width:min(560px, 94vw);
      padding:28px 22px;
      border-radius:18px;
      background: var(--card);
      backdrop-filter: blur(10px);
      box-shadow: 0 20px 60px rgba(0,0,0,.18);
      text-align:center;
    }

    h1{margin:0 0 10px}
    p{margin:0 0 18px}

    .gif{
      width:260px;
      height:260px;
      margin:14px auto 18px;
      border-radius:18px;
      overflow:hidden;
      background:#fff;
      display:flex;
      align-items:center;
      justify-content:center;
    }

    .gif img{
      width:100%;
      height:100%;
      object-fit:cover;
    }

    .btns{
      display:flex;
      justify-content:center;
      align-items:center;
      gap:14px;
      margin-top:12px;
      position:relative;
      height:80px;
    }

    button{
      border:0;
      cursor:pointer;
      padding:14px 22px;
      border-radius:999px;
      font-weight:800;
      font-size:16px;
      transition:.15s;
    }

    #yesBtn{
      background:var(--yes);
      color:white;
      transform:scale(1);
    }

    #noBtn{
      background:var(--no);
      color:white;
      position:absolute;
      left:60%;
      top:50%;
      transform:translate(-50%,-50%);
    }

    .hidden{display:none}

    .heart{
      position:absolute;
      width:14px;height:14px;
      transform: rotate(45deg);
      background: rgba(255,255,255,.7);
      animation: float 6s linear infinite;
    }
    .heart::before,.heart::after{
      content:"";
      position:absolute;
      width:14px;height:14px;
      background:inherit;
      border-radius:50%;
    }
    .heart::before{left:-7px}
    .heart::after{top:-7px}

    @keyframes float{
      from{transform:translateY(40vh) rotate(45deg);opacity:0}
      10%{opacity:.8}
      to{transform:translateY(-70vh) rotate(45deg);opacity:0}
    }
  </style>
</head>

<body>

<div class="card" id="screen1">

  <h1 id="question">Tu veux être ma Valentine ? 🍓</h1>
  <p id="sub">Réfléchis bien 😌</p>

  <div class="gif">
    <img src="franui-roses.png" alt="Franui et roses">
  </div>

  <div class="btns" id="btnArea">
    <button id="yesBtn">Oui</button>
    <button id="noBtn">Non</button>
  </div>

</div>

<div class="card hidden" id="screen2">
  <h1>OUIIII 💖</h1>
  <div class="gif">
    <img src="franui-roses.png" alt="Franui et roses">
  </div>
  <p style="font-size:18px;font-weight:800;">Rendez-vous le 14 ?</p>
</div>

<script>
const noBtn=document.getElementById("noBtn");
const yesBtn=document.getElementById("yesBtn");
const btnArea=document.getElementById("btnArea");
const screen1=document.getElementById("screen1");
const screen2=document.getElementById("screen2");
const sub=document.getElementById("sub");

const phrases=[
"T’es sûre ?",
"Vraiment ?",
"Allez… dis oui",
"Tu me brises le cœur",
"Dernière chance",
"Je retente encore"
];

let count=0;
let scale=1;

function moveNo(){
  const rect=btnArea.getBoundingClientRect();
  const btnRect=noBtn.getBoundingClientRect();
  const maxX=rect.width-btnRect.width;
  const maxY=rect.height-btnRect.height;
  const x=Math.random()*maxX;
  const y=Math.random()*maxY;
  noBtn.style.left=x+"px";
  noBtn.style.top=y+"px";
  noBtn.style.transform="none";
}

function growYes(){
  scale=Math.min(3,scale+0.2);
  yesBtn.style.transform="scale("+scale+")";
}

noBtn.addEventListener("click",()=>{
  count++;
  sub.textContent=phrases[count%phrases.length];
  growYes();
  moveNo();
});

yesBtn.addEventListener("click",()=>{
  screen1.classList.add("hidden");
  screen2.classList.remove("hidden");
  for(let i=0;i<25;i++){
    setTimeout(()=>{
      const h=document.createElement("div");
      h.className="heart";
      h.style.left=Math.random()*100+"vw";
      document.body.appendChild(h);
      setTimeout(()=>h.remove(),6000);
    },i*80);
  }
});
</script>

</body>
</html>
