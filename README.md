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
