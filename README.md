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

    /* 成功畫面：直接展示賀卡 */
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
    <!-- 提問主畫面 -->
    <div id="questionScreen">
      <h1 id="questionText">Will you be my valentine? 💕</h1>
      <div class="subtitle">(There is only one correct answer.)</div>

      <div class="img-container">
        <!-- 詢問照片已改為 PNG 檔 -->
        <img src="https://imgur.com/a/pXd3Rrf" alt="Hyena with Rose" />
      </div>

      <div class="btn-group" id="btnGroup">
        <button class="btn-yes" onclick="acceptProposal()">YES 💗</button>
        <button class="btn-no" id="noBtn" onmouseover="handleNoInteraction()" onclick="handleNoInteraction()">NO 😈</button>
      </div>
    </div>

    <!-- 點擊 YES 轉跳後的最終賀卡頁面 -->
    <div class="success-screen" id="successScreen">
      <div class="img-container">
        <!-- 慶祝照片已改為 PNG 檔 -->
        <img src="https://imgur.com/a/z4xI6hS" alt="YAYYYYY! I knew you'd say yes!" />
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
        // 第一次：往左移動
        const currentRect = noBtn.getBoundingClientRect();
        noBtn.style.left = `${Math.max(20, currentRect.left - 150)}px`;
        noBtn.style.top = `${currentRect.top}px`;
      } 
      else if (attempt === 2) {
        // 第二次：跳到上方
        noBtn.style.top = '50px';
      } 
      else {
        // 第三次以上：變小 + 全螢幕隨機跳躍
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

      // 多次嘗試後更換文字
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
