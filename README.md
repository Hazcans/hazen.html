<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<title>Sesli Piyano</title>

<style>
:root {
  --bg: #0a0a0f;
  --white: #ffffff;
  --accent: #7c6af7;
}

body {
  margin: 0;
  background: var(--bg);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  font-family: sans-serif;
}

.piano {
  display: flex;
  gap: 6px;
}

.key {
  width: 70px;
  height: 240px;
  background: var(--white);
  border-radius: 8px;
  border: 2px solid #ccc;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  padding-bottom: 12px;
  font-weight: bold;
  cursor: pointer;
  transition: .1s;
}

.key.active {
  background: var(--accent);
  color: #fff;
  transform: scale(0.95);
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

<!-- Sesler -->
<audio id="f" src="https://cdn.jsdelivr.net/gh/gleitz/midi-js-soundfonts/FluidR3_GM/acoustic_grand_piano-mp3/C4.mp3"></audio>
<audio id="g" src="https://cdn.jsdelivr.net/gh/gleitz/midi-js-soundfonts/FluidR3_GM/acoustic_grand_piano-mp3/D4.mp3"></audio>
<audio id="h" src="https://cdn.jsdelivr.net/gh/gleitz/midi-js-soundfonts/FluidR3_GM/acoustic_grand_piano-mp3/E4.mp3"></audio>
<audio id="j" src="https://cdn.jsdelivr.net/gh/gleitz/midi-js-soundfonts/FluidR3_GM/acoustic_grand_piano-mp3/F4.mp3"></audio>
<audio id="k" src="https://cdn.jsdelivr.net/gh/gleitz/midi-js-soundfonts/FluidR3_GM/acoustic_grand_piano-mp3/G4.mp3"></audio>
<audio id="l" src="https://cdn.jsdelivr.net/gh/gleitz/midi-js-soundfonts/FluidR3_GM/acoustic_grand_piano-mp3/A4.mp3"></audio>
<audio id="ş" src="https://cdn.jsdelivr.net/gh/gleitz/midi-js-soundfonts/FluidR3_GM/acoustic_grand_piano-mp3/B4.mp3"></audio>
<audio id="i" src="https://cdn.jsdelivr.net/gh/gleitz/midi-js-soundfonts/FluidR3_GM/acoustic_grand_piano-mp3/C5.mp3"></audio>

<script>
function play(key) {
  const audio = document.getElementById(key);
  if (!audio) return;

  // aynı sesi üst üste çalabilmek için clone
  const sound = audio.cloneNode();
  sound.play();

  const el = document.querySelector(`[data-key="${key}"]`);
  if (el) {
    el.classList.add("active");
    setTimeout(() => el.classList.remove("active"), 120);
  }
}

/* klavye */
document.addEventListener("keydown", e => {
  let key = e.key.toLowerCase();

  // Türkçe klavye fix
  if (key === "ı") key = "i";

  play(key);
});

/* mouse */
document.querySelectorAll(".key").forEach(k => {
  k.addEventListener("click", () => play(k.dataset.key));
});
</script>

</body>
</html>
