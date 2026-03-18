<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Hacker Movie Prank</title>
<style>
  body {
    margin: 0;
    background: black;
    color: lime;
    font-family: monospace;
    overflow: hidden;
    transition: background 1s;
  }

  #battery-container {
    position: fixed;
    top: 10px;
    left: 50%;
    transform: translateX(-50%);
    width: 300px;
    height: 30px;
    border: 2px solid lime;
  }

  #battery {
    width: 100%;
    height: 100%;
    background: lime;
    transition: width 0.2s;
  }

  #terminal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    z-index: 1;
  }

  .line {
    white-space: pre;
    line-height: 1.2em;
  }

  .warning {
    color: red;
    font-weight: bold;
  }

  #countdown {
    position: fixed;
    top: 50px;
    left: 50%;
    transform: translateX(-50%);
    font-size: 30px;
    font-weight: bold;
    color: red;
    z-index: 2;
  }
</style>
</head>
<body>

<div id="battery-container"><div id="battery"></div></div>
<div id="terminal"></div>
<div id="countdown"></div>

<script>
const terminal = document.getElementById("terminal");
const batteryBar = document.getElementById("battery");
const countdownDiv = document.getElementById("countdown");

let battery = 100;
const warnings = [
  "!!! BATTERY CRITICAL !!!",
  "!!! SYSTEM OVERLOAD DETECTED !!!",
  "!!! EMERGENCY SHUTDOWN INITIATED !!!",
  "!!! VIRUS IN PROGRESS !!!",
  "!!! SECURITY BREACH DETECTED !!!"
];

// Matrix-style random line
function randomMatrixLine() {
  let line = "";
  const len = Math.floor(Math.random() * 80) + 20;
  for (let i = 0; i < len; i++) {
    line += String.fromCharCode(Math.floor(Math.random() * (126 - 33) + 33));
  }
  return line;
}

// Full-screen hacker scroll
function hackerScroll() {
  const div = document.createElement("div");
  div.className = "line";
  // Random red warning or green line
  if (Math.random() < 0.12) {
    div.textContent = warnings[Math.floor(Math.random() * warnings.length)];
    div.classList.add("warning");
  } else {
    div.textContent = randomMatrixLine();
  }

  terminal.appendChild(div);
  if (terminal.childNodes.length > 80) terminal.removeChild(terminal.firstChild);

  requestAnimationFrame(hackerScroll);
}

// 10-second countdown
let countdown = 10;
function startCountdown() {
  if (countdown >= 0) {
    countdownDiv.textContent = `!!! SYSTEM VIRUS COUNTDOWN: ${countdown}s !!!`;
    countdown--;
    setTimeout(startCountdown, 1000);
  } else {
    countdownDiv.textContent = "";
    startBatteryDrain();
  }
}

// Battery drain animation
function startBatteryDrain() {
  function batteryFrame() {
    const div = document.createElement("div");
    div.className = "line";

    if (Math.random() < 0.15) {
      div.textContent = warnings[Math.floor(Math.random() * warnings.length)];
      div.classList.add("warning");
      battery -= Math.floor(Math.random() * 5) + 1;
      if (battery < 0) battery = 0;
      batteryBar.style.width = battery + "%";
    } else {
      div.textContent = randomMatrixLine();
    }

    terminal.appendChild(div);
    if (terminal.childNodes.length > 80) terminal.removeChild(terminal.firstChild);

    if (battery > 0) requestAnimationFrame(batteryFrame);
    else {
      // Battery reaches 0 → screen blackout
      document.body.style.background = "black";
      terminal.innerHTML = "";
      countdownDiv.innerHTML = "";
      batteryBar.style.width = "0%";
      alert("SYSTEM OFFLINE "); // optional dramatic prank
    }
  }
  batteryFrame();
}

// Start prank
hackerScroll();
startCountdown();
</script>

</body>
</html>
