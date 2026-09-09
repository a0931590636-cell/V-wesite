<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Will you be my valentine? 💕</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: #fcf6f0;
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 20px;
      overflow: hidden;
    }

    .card {
      background: #fffbf7;
      border: 1px solid #f2e3d5;
      border-radius: 28px;
      padding: 30px 20px;
      max-width: 420px;
      width: 100%;
      box-shadow: 0 10px 30px rgba(220, 180, 180, 0.15);
      text-align: center;
      position: relative;
    }

    h1 {
      color: #2b2b2b;
      font-size: 24px;
      font-weight: 700;
      margin-bottom: 8px;
      transition: all 0.3s ease;
    }

    .subtitle {
      color: #888888;
      font-size: 14px;
      margin-bottom: 20px;
    }

    .img-container {
      width: 100%;
      border-radius: 20px;
      overflow: hidden;
      margin-bottom: 20px;
      background-color: #eee;
    }

    .img-container img {
      width: 100%;
      height: auto;
      display: block;
      border-radius: 20px;
    }

    .btn-group {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 20px;
      min-height: 60px;
      position: relative;
    }

    button {
      padding: 12px 28px;
      font-size: 18px;
      font-weight: 700;
      border: none;
      border-radius: 25px;
      cursor: pointer;
      transition: transform 0.2s ease, top 0.3s ease, left 0.3s ease, background-color 0.2s ease;
    }

    .btn-yes {
      background-color: #ffccd5;
      color: #c92a2a;
      z-index: 2;
    }

    .btn-yes:hover {
      background-color: #ffb3c1;
      transform: scale(1.08);
    }

    .btn-no {
      background-color: #e9ecef;
      color: #495057;
      position: relative;
      z-index: 1;
    }

    .success-screen {
      display: none;
    }

    .success-screen .img-container {
      margin-bottom: 0;
    }
  </style>
</head>
<body>

  <div class="card">
    <!-- 詢問主頁面 -->
    <div id="questionScreen">
      <h1 id="questionText">Will you be my valentine? 💕</h1>
      <div class="subtitle">(There is only one correct answer.)</div>

      <div class="img-container">
        <!-- 詢問圖片：hyena_ask 乾淨直連網址 -->
        <img src="https://i.imgur.com/BHitwmt.png" alt="Hyena with Rose" />
      </div>

      <div class="btn-group" id="btnGroup">
        <button class="btn-yes" onclick="acceptProposal()">YES 💗</button>
        <button class="btn-no" id="noBtn" onmouseover="handleNoInteraction()" onclick="handleNoInteraction()">NO 😈</button>
      </div>
    </div>

    <!-- 點擊 YES 轉跳後的成功頁面 -->
    <div class="success-screen" id="successScreen">
      <div class="img-container">
        <!-- ⚠️ 請將下方的網址替換成第二張圖片 (hyena_yes) 複製出來的直連網址 (例如：https://i.imgur.com/xxxx.png) -->
        <img src="https://i.imgur.com/你的第二張成功圖片ID.png" alt="YAYYYYY! I knew you'd say yes!" />
      </div>
    </div>
  </div>

  <script>
    const noBtn = document.getElementById('noBtn');
    const questionText = document.getElementById('questionText');
    let attempt = 0;

    function handleNoInteraction() {
      attempt++;

      noBtn.style.position = 'fixed';

      if (attempt === 1) {
        const currentRect = noBtn.getBoundingClientRect();
        noBtn.style.left = `${Math.max(20, currentRect.left - 150)}px`;
        noBtn.style.top = `${currentRect.top}px`;
      } 
      else if (attempt === 2) {
        noBtn.style.top = '50px';
      } 
      else {
        const currentScale = Math.max(0.3, 1 - (attempt - 2) * 0.15);
        noBtn.style.transform = `scale(${currentScale})`;

        const padding = 60;
        const maxX = window.innerWidth - noBtn.offsetWidth - padding;
        const maxY = window.innerHeight - noBtn.offsetHeight - padding;

        const randomX = Math.max(padding, Math.floor(Math.random() * maxX));
        const randomY = Math.max(padding, Math.floor(Math.random() * maxY));

        noBtn.style.left = `${randomX}px`;
        noBtn.style.top = `${randomY}px`;
      }

      if (attempt >= 4) {
        questionText.innerText = "You really thought I would let you say no? 😭";
      }
    }

    function acceptProposal() {
      document.getElementById('questionScreen').style.display = 'none';
      document.getElementById('successScreen').style.display = 'block';
    }
  </script>
</body>
</html>
