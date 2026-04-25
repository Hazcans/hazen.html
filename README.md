<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<title>Klavye Piyano</title>
<style>
:root {
  --bg: #0a0a0f;
  --white: #ffffff;
  --black: #111;
  --accent: #7c6af7;
}

body {
  background: var(--bg);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  font-family: sans-serif;
}

/* piyano */
.piano {
  display: flex;
  gap: 4px;
}

.key {
  width: 60px;
  height: 220px;
  background: var(--white);
  border-radius: 6px;
  border: 2px solid #ccc;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  padding-bottom: 10px;
  cursor: pointer;
  transition: .1s;
  user-select: none;
}

.key.active {
  background: var(--accent);
  color: #fff;
  transform: scale(0.95);
}

.label {
  font-size: 14px;
}
</style>
</head>
<body>

<div class="piano">
  <div class="key" data-key="f">F</div>
  <div class="key" data-key="g">G</div>
  <div class="key" data-key="h">H</div>
  <div class="key" data-key="j">J</div>
  <div class="key" data-key="k">K</div>
  <div class="key" data-key="l">L</div>
  <div class="key" data-key="ş">Ş</div>
  <div class="key" data-key="i">İ</div>
</div>

<script>
const sounds = {
  f: "https://www.soundjay.com/piano/piano-do.wav",
  g: "https://www.soundjay.com/piano/piano-re.wav",
  h: "https://www.soundjay.com/piano/piano-mi.wav",
  j: "https://www.soundjay.com/piano/piano-fa.wav",
  k: "https://www.soundjay.com/piano/piano-sol.wav",
  l: "https://www.soundjay.com/piano/piano-la.wav",
  "ş": "https://www.soundjay.com/piano/piano-ti.wav",
  i: "https://www.soundjay.com/piano/piano-do.wav"
};

function playSound(key) {
  const audio = new Audio(sounds[key]);
  audio.play();

  const el = document.querySelector(`[data-key="${key}"]`);
  if (el) {
    el.classList.add("active");
    setTimeout(() => el.classList.remove("active"), 150);
  }
}

/* klavye */
document.addEventListener("keydown", e => {
  const key = e.key.toLowerCase();
  if (sounds[key]) playSound(key);
});

/* mouse */
document.querySelectorAll(".key").forEach(k => {
  k.addEventListener("click", () => {
    playSound(k.dataset.key);
  });
});
</script>

</body>
</html>
