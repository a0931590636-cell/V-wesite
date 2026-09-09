<script>
    const noBtn = document.getElementById('noBtn');
    const questionText = document.getElementById('questionText');
    let attempt = 0;

    const noMessages = [
      "No way! 😜",
      "Nice try! 😂",
      "Wrong button! 🥺",
      "Are you sure? 😭"
    ];

    function handleNoInteraction(event) {
      if (event) {
        event.preventDefault(); // 防止手機觸控雙重觸發
      }

      attempt++;

      // 更換按鈕文字
      const messageIndex = Math.min(attempt - 1, noMessages.length - 1);
      noBtn.textContent = noMessages[messageIndex];

      // 強制將按鈕改為固定定位並移動
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
