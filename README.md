<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>A Special Surprise For You ❤️</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 99%, #feada6 100%);
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      overflow: hidden;
      perspective: 1000px;
    }

    /* Floating Hearts Background */
    .heart-bg {
      position: absolute;
      top: -10vh;
      color: rgba(255, 255, 255, 0.6);
      font-size: 20px;
      animation: fall 6s linear infinite;
      user-select: none;
      z-index: 1;
    }

    @keyframes fall {
      0% {
        transform: translateY(0) rotate(0deg);
        opacity: 1;
      }
      100% {
        transform: translateY(110vh) rotate(360deg);
        opacity: 0;
      }
    }

    /* Envelope & Card Container */
    .card-container {
      width: 340px;
      height: 480px;
      position: relative;
      transform-style: preserve-3d;
      transition: transform 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
      cursor: pointer;
      z-index: 10;
    }

    .card-container.flipped {
      transform: rotateY(180deg);
      cursor: default;
    }

    .card-face {
      position: absolute;
      width: 100%;
      height: 100%;
      backface-visibility: hidden;
      border-radius: 20px;
      box-shadow: 0 15px 35px rgba(0,0,0,0.2);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 30px;
      text-align: center;
    }

    /* Front of Card (Unrevealing Cover) */
    .card-front {
      background: #ffffff;
      border: 3px solid #ff4b2b;
    }

    .gift-icon {
      font-size: 70px;
      margin-bottom: 20px;
      animation: pulse 1.5s infinite;
    }

    @keyframes pulse {
      0% { transform: scale(1); }
      50% { transform: scale(1.1); }
      100% { transform: scale(1); }
    }

    .card-front h2 {
      color: #333;
      font-size: 24px;
      margin-bottom: 10px;
    }

    .card-front p {
      color: #777;
      font-size: 14px;
    }

    .click-hint {
      margin-top: 25px;
      background: #ff4b2b;
      color: white;
      padding: 10px 20px;
      border-radius: 25px;
      font-size: 14px;
      font-weight: bold;
    }

    /* Back of Card (The Proposal) */
    .card-back {
      background: #ffffff;
      transform: rotateY(180deg);
      border: 3px solid #ff416c;
      justify-content: space-between;
    }

    .card-back h1 {
      color: #ff416c;
      font-size: 26px;
      margin-top: 10px;
    }

    .monkey-emoji {
      font-size: 60px;
      margin: 10px 0;
    }

    .proposal-text {
      color: #444;
      font-size: 18px;
      line-height: 1.4;
      font-weight: 600;
    }

    .btn-group {
      display: flex;
      gap: 15px;
      width: 100%;
      justify-content: center;
      position: relative;
      min-height: 50px;
      margin-bottom: 10px;
    }

    button {
      padding: 12px 25px;
      font-size: 16px;
      font-weight: bold;
      border: none;
      border-radius: 25px;
      cursor: pointer;
      transition: transform 0.2s, background-color 0.2s;
    }

    .btn-yes {
      background: linear-gradient(to right, #ff416c, #ff4b2b);
      color: white;
      box-shadow: 0 4px 15px rgba(255, 65, 108, 0.4);
    }

    .btn-yes:hover {
      transform: scale(1.1);
    }

    .btn-no {
      background: #e0e0e0;
      color: #555;
      position: absolute;
    }

    /* Celebration Screen */
    .celebration {
      display: none;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    .celebration h1 {
      font-size: 32px;
      color: #ff416c;
      margin-bottom: 15px;
    }

    .celebration p {
      font-size: 18px;
      color: #333;
    }
  </style>
</head>
<body>

  <div class="card-container" id="cardContainer" onclick="revealCard()">
    <!-- Front Face (Unrevealing Surprise) -->
    <div class="card-face card-front">
      <div class="gift-icon">🎁</div>
      <h2>You Have 1 New Secret Message</h2>
      <p>Someone special sent you a private card...</p>
      <div class="click-hint">Tap to Reveal</div>
    </div>

    <!-- Back Face (Proposal Message) -->
    <div class="card-face card-back" id="cardBack">
      <div id="proposalContent" style="display: flex; flex-direction: column; align-items: center; height: 100%; justify-content: space-between; width: 100%;">
        <h1>Hey Sweetheart! 🙈</h1>
        <div class="monkey-emoji">🐒❤️</div>
        <p class="proposal-text">Will you marry your Bandar?</p>
        
        <div class="btn-group" id="btnGroup">
          <button class="btn-yes" onclick="acceptProposal(event)">YES! 💖</button>
          <button class="btn-no" id="noBtn" onmouseover="moveButton()" onclick="moveButton()">No 😜</button>
        </div>
      </div>

      <!-- Final Celebration Content -->
      <div class="celebration" id="celebrationContent">
        <div style="font-size: 70px; margin-bottom: 10px;">💍🐒✨</div>
        <h1>Woohoo! 🎉</h1>
        <p>You made your Bandar the happiest in the world! ❤️</p>
      </div>
    </div>
  </div>

  <script>
    let isFlipped = false;

    // Reveal the card on click
    function revealCard() {
      if (!isFlipped) {
        document.getElementById('cardContainer').classList.add('flipped');
        isFlipped = true;
      }
    }

    // Playful runaway "No" button
    function moveButton() {
      const noBtn = document.getElementById('noBtn');
      const btnGroup = document.getElementById('btnGroup');
      
      const groupRect = btnGroup.getBoundingClientRect();
      const maxX = groupRect.width - noBtn.offsetWidth;
      const maxY = groupRect.height - noBtn.offsetHeight;
      
      // Calculate random positions within the button area
      const randomX = (Math.random() - 0.5) * 200;
      const randomY = (Math.random() - 0.5) * 100;
      
      noBtn.style.transform = `translate(${randomX}px, ${randomY}px)`;
    }

    // Handle "Yes" acceptance
    function acceptProposal(event) {
      event.stopPropagation(); // Prevents card interaction issues
      document.getElementById('proposalContent').style.display = 'none';
      document.getElementById('celebrationContent').style.display = 'flex';
      createBurstHearts();
    }

    // Create falling background hearts
    function createHeart() {
      const heart = document.createElement('div');
      heart.classList.add('heart-bg');
      heart.innerHTML = '❤️';
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.animationDuration = Math.random() * 3 + 3 + 's';
      heart.style.fontSize = Math.random() * 15 + 15 + 'px';
      document.body.appendChild(heart);

      setTimeout(() => {
        heart.remove();
      }, 6000);
    }

    setInterval(createHeart, 300);

    // Heart explosion effect when clicking "Yes"
    function createBurstHearts() {
      for (let i = 0; i < 30; i++) {
        setTimeout(createHeart, i * 50);
      }
    }
  </script>
</body>
</html>
