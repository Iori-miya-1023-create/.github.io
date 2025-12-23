# .github.io
抽選
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<title>スマホ用パチンコ抽選</title>
<style>
  body {
    font-family: sans-serif;
    text-align: center;
    background: #111;
    color: #fff;
    margin: 0;
    padding: 20px;
  }

  #number {
    font-size: 18vw;
    font-weight: bold;
    margin: 20px 0;
    transition: transform 0.1s ease, color 0.2s;
  }

  .flash {
    animation: flash 0.2s alternate infinite;
  }

  @keyframes flash {
    from { color: #fff; }
    to { color: #ffeb3b; }
  }

  .shake {
    animation: shake 0.1s infinite;
  }

  @keyframes shake {
    0% { transform: translateX(0); }
    25% { transform: translateX(-10px); }
    50% { transform: translateX(10px); }
    75% { transform: translateX(-10px); }
    100% { transform: translateX(0); }
  }

  button {
    font-size: 8vw;
    padding: 20px 40px;
    margin-top: 20px;
    border-radius: 12px;
    border: none;
    background: #ff4444;
    color: #fff;
    font-weight: bold;
    width: 80%;
  }
</style>
</head>
<body>

<h1 style="font-size: 7vw;">🎰 パチンコ抽選（1〜11・重複なし）</h1>

<div id="number">---</div>

<button onclick="startLottery()">抽選スタート</button>

<audio id="kyuin" src="https://soundeffect-lab.info/sound/anime/mp3/decision1.mp3"></audio>

<script>
let numbers = [];

function resetNumbers() {
  numbers = [];
  for (let i = 1; i <= 11; i++) numbers.push(i);
  numbers = numbers.sort(() => Math.random() - 0.5);
}

resetNumbers();

function startLottery() {
  const numberEl = document.getElementById("number");
  const kyuin = document.getElementById("kyuin");

  numberEl.classList.add("flash", "shake");

  if (numbers.length === 0) resetNumbers();
  const finalNumber = numbers.pop();

  let interval = 80;
  let count = 0;

  const roller = setInterval(() => {
    numberEl.textContent = Math.floor(Math.random() * 11) + 1;
    count++;

    if (count === 10) interval = 40;
    if (count === 20) interval = 20;
    if (count === 40) interval = 40;
    if (count === 50) interval = 80;

  }, interval);

  setTimeout(() => {
    clearInterval(roller);

    numberEl.textContent = finalNumber;

    numberEl.classList.remove("shake");
    setTimeout(() => numberEl.classList.remove("flash"), 500);

    if (finalNumber <= 3) {
      kyuin.currentTime = 0;
      kyuin.play();
    }

  }, 2500);
}
</script>

</body>
</html>
