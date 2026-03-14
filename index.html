let currentInstrument = null;

const popup = document.getElementById("popup");
const instrumentMenu = document.getElementById("instrument-menu");
const tunerBar = document.getElementById("tuner-bar");
const cursor = document.getElementById("tuner-cursor");
const noteDisplay = document.getElementById("note-display");

// Notes pour tous les instruments
const guitarNotes = [
  { note: "E", freq: 82.41 },
  { note: "A", freq: 110 },
  { note: "D", freq: 146.83 },
  { note: "G", freq: 196 },
  { note: "B", freq: 246.94 },
  { note: "E", freq: 329.63 }
];

const ukuleleNotes = [
  { note: "G", freq: 196 },
  { note: "C", freq: 261.63 },
  { note: "E", freq: 329.63 },
  { note: "A", freq: 440 }
];

const bassNotes = [
  { note: "E", freq: 41.20 },
  { note: "A", freq: 55.00 },
  { note: "D", freq: 73.42 },
  { note: "G", freq: 98.00 }
];

const violinNotes = [
  { note: "G", freq: 196 },
  { note: "D", freq: 293.66 },
  { note: "A", freq: 440 },
  { note: "E", freq: 659.25 }
];

const mandolinNotes = [
  { note: "G", freq: 196 },
  { note: "D", freq: 293.66 },
  { note: "A", freq: 440 },
  { note: "E", freq: 659.25 }
];

// Son bing
let audioCtx;
let stableCount = 0;
const requiredStable = 5;
let lastCorrect = false;

// Affichage des notes
function renderNotes(instrument) {
  noteDisplay.innerHTML = "";
  let notes;

  switch(instrument) {
    case "ukulele": notes = ukuleleNotes; break;
    case "basse": notes = bassNotes; break;
    case "violon": notes = violinNotes; break;
    case "mandoline": notes = mandolinNotes; break;
    default: notes = guitarNotes; break;
  }

  notes.forEach(n => {
    let el = document.createElement("span");
    el.className = "note";
    el.textContent = n.note;
    noteDisplay.appendChild(el);
  });
}

// Bouton commencer
document.getElementById("btn-start").onclick = () => {
  popup.style.display = "none";
  instrumentMenu.style.display = "block";

  if (!audioCtx) {
    audioCtx = new (window.AudioContext || window.webkitAudioContext)();
  }
};

// Boutons instruments
document.getElementById("btn-guitare").onclick = () => selectInstrument("guitare");
document.getElementById("btn-ukulele").onclick = () => selectInstrument("ukulele");

// Nouveaux instruments
document.getElementById("btn-basse").onclick = () => selectInstrument("basse");
document.getElementById("btn-violon").onclick = () => selectInstrument("violon");
document.getElementById("btn-mandoline").onclick = () => selectInstrument("mandoline");

// Fonction commune
function selectInstrument(instrument) {
  currentInstrument = instrument;
  instrumentMenu.style.display = "none";
  tunerBar.style.display = "block";
  renderNotes(instrument);
  startTuner();
}

// Tuner
let audioContext;
let analyser;
let dataArray;

async function startTuner() {
  if (audioContext) return;
  try {
    audioContext = new (window.AudioContext || window.webkitAudioContext)();
    const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
    const source = audioContext.createMediaStreamSource(stream);
    analyser = audioContext.createAnalyser();
    analyser.fftSize = 2048;
    source.connect(analyser);
    dataArray = new Float32Array(analyser.fftSize);
    update();
  } catch (err) {
    alert("Microphone refusé ou non disponible.");
  }
}

// Son "bing"
function playCorrectTone() {
  if (!audioCtx) return;
  let oscillator = audioCtx.createOscillator();
  let gainNode = audioCtx.createGain();
  oscillator.connect(gainNode);
  gainNode.connect(audioCtx.destination);
  oscillator.type = "sine";
  oscillator.frequency.value = 880; // A5
  gainNode.gain.value = 0.2;
  oscillator.start();
  oscillator.stop(audioCtx.currentTime + 0.15);
}

// Mise à jour du tuner
function update() {
  analyser.getFloatTimeDomainData(dataArray);
  let freq = autoCorrelate(dataArray, audioContext.sampleRate);

  if (freq !== -1) {
    let notes;
    switch(currentInstrument) {
      case "ukulele": notes = ukuleleNotes; break;
      case "basse": notes = bassNotes; break;
      case "violon": notes = violinNotes; break;
      case "mandoline": notes = mandolinNotes; break;
      default: notes = guitarNotes; break;
    }

    let closest = notes.reduce((a, b) => Math.abs(b.freq - freq) < Math.abs(a.freq - freq) ? b : a);
    let diff = freq - closest.freq;
    let percent = Math.max(-1, Math.min(1, diff / closest.freq));
    cursor.style.left = (50 + percent * 50) + "%";

    // Détection stabilité
    if (Math.abs(percent) < 0.02) {
      cursor.style.background = "#4CAF50";
      stableCount++;
      if (stableCount >= requiredStable) {
        if (!lastCorrect) {
          playCorrectTone();
          lastCorrect = true;
        }
      }
    } else {
      stableCount = 0;
      lastCorrect = false;
      cursor.style.background = percent < 0 ? "#2196F3" : "#ff4444";
    }

    // Notes affichées
    const noteEls = document.querySelectorAll(".note");
    noteEls.forEach(n => {
      n.classList.remove("active");
      n.classList.remove("correct");
      if (n.textContent === closest.note) {
        n.classList.add("active");
        if (Math.abs(percent) < 0.02 && stableCount >= requiredStable) {
          n.classList.add("correct");
        }
      }
    });
  }

  requestAnimationFrame(update);
}

// Auto-corrélation pour fréquence
function autoCorrelate(buf, sampleRate) {
  let SIZE = buf.length;
  let rms = 0;
  for (let i = 0; i < SIZE; i++) rms += buf[i] * buf[i];
  rms = Math.sqrt(rms / SIZE);
  if (rms < 0.01) return -1;

  let r = new Array(SIZE).fill(0);
  for (let i = 0; i < SIZE; i++)
    for (let j = 0; j < SIZE - i; j++)
      r[i] += buf[j] * buf[j + i];

  let d = 0;
  while (r[d] > r[d + 1]) d++;
  let maxval = -1, maxpos = -1;
  for (let i = d; i < SIZE; i++) {
    if (r[i] > maxval) { maxval = r[i]; maxpos = i; }
  }
  if (maxpos === -1) return -1;
  return sampleRate / maxpos;
}
