<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Sorry Card for Arthy</title>
    <style>
      body {
        font-family: "Arial", sans-serif;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
        background: linear-gradient(135deg, #ffdde1, #ee9ca7);
        overflow: hidden;
      }

      .card {
        width: 90%;
        max-width: 350px;
        height: 200px;
        background: rgba(255, 255, 255, 0.363);
        border-radius: 20px;
        box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
        position: relative;
        overflow: hidden;
        transform-style: preserve-3d;
        transition: transform 1s;
        user-select: none;
      }

      .card-front,
      .card-back {
        position: absolute;
        width: 100%;
        height: 100%;
        backface-visibility: hidden;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        font-size: 1.2rem;
        text-align: center;
      }

      .card-front {
        background: #ffdee97a;
        color: #333;
      }

      .card-front .blink {
        animation: blink 1.5s infinite;
      }

      .card-back {
        background: #ffdee9;
        color: #555;
        transform: rotateY(180deg);
      }

      @keyframes blink {
        0%,
        50%,
        100% {
          opacity: 1;
        }
        25%,
        75% {
          opacity: 0.5;
        }
      }

      .floating-hearts {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        pointer-events: none;
        z-index: -1;
      }

      .heart {
        /* position: absolute; */
        /* font-size: 24px; */
        color: #ff3366;
        animation: float 7s linear infinite;
        opacity: 0;
      }

      @keyframes float {
        0% {
          transform: translate(0, 100vh) rotate(0deg);
          opacity: 1;
        }
        50% {
          transform: translate(10vw, 50vh) rotate(180deg);
        }
        100% {
          transform: translate(-10vw, -100vh) rotate(360deg);
          opacity: 0;
        }
      }

      .tap-to-change {
        margin-top: 20px;
        font-size: 1rem;
        color: #333;
        text-align: center;
        user-select: none;  
        display: none;
      }

      @media (max-width: 768px) {
        .tap-to-change {
          display: block;
        }
      }
    </style>
  </head>
  <body>
    <div class="card" id="card">
      <div class="card-front" id="card-front">
        <h2 class="blink">Dear Arthy...</h2>
      </div>
      <div class="card-back" id="card-back">
        <p>Message 1</p>
      </div>
    </div>

    <p class="tap-to-change">Tap to change</p>

    <div class="floating-hearts" id="hearts"></div>

    <script>
      const messages = [
        "Dear Arthy...",
        "I hope you can forgive me.",
        "You mean so much to me.",
        "I truly regret my mistake.",
        "I'm sorry from my heart.",
      ];

      let currentMessage = 0;
      let flipState = 0;

      const card = document.getElementById("card");
      const front = document.getElementById("card-front");
      const back = document.getElementById("card-back");

      function updateMessage() {
        if (flipState === 0) {
          back.innerHTML = `<p>${messages[currentMessage]}</p>`;
        } else {
          front.innerHTML = `<p>${messages[currentMessage]}</p>`;
        }
      }

      function flipCard() {
        card.style.transform =
          flipState % 2 === 0
            ? "perspective(1000px) rotateY(360deg)"
            : "perspective(1000px) rotateY(0deg)";
        flipState++;
        currentMessage = (currentMessage + 1) % messages.length;

        // console.log(currentMessage, flipState);
        setTimeout(updateMessage, 200);
      }

      card.addEventListener("click", flipCard);
      card.setAttribute("tabindex", "0");
      card.addEventListener("keypress", (e) => {
        if (e.key === "Enter") flipCard();
      });

      // Floating hearts generator
      function createHearts() {
        const heartsContainer = document.getElementById("hearts");
        for (let i = 0; i < 15; i++) {
          const heart = document.createElement("div");
          heart.className = "heart";
          heart.style.left = Math.random() * 100 + "vw";
          heart.style.animationDelay = Math.random() * 7 + "s";
          heart.innerHTML = "❤";
          heartsContainer.appendChild(heart);
        }
      }

      createHearts();
    </script>
  </body>
</html>
