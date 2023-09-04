 ## Real-time Character Counter

This is a simple real-time character counter that counts the number of characters in a textarea and displays the total number of characters and the number of remaining characters.
# Hosted Link

### Step-by-Step Explanation

#### HTML

The HTML code creates a simple webpage with a textarea and two paragraphs to display the total number of characters and the number of remaining characters.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Stopwatch</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <div id="timer">00:00:00</div>
    <div id="buttons">
      <button id="start">Start</button>
      <button id="stop">Stop</button>
      <button id="reset">Reset</button>
    </div>
    <script src="index.js"></script>
  </body>
</html>

```

#### CSS

The CSS code styles the textarea and the counter container.

```css

body {
  background-color: #f0f0f0;
  font-family: "Poppins", sans-serif;
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-height: 100vh;
  overflow: hidden;
  align-items: center;
}

#timer {
  font-size: 7rem;
  font-weight: 700;
  text-shadow: 2px 2px #f8a5c2;
  color: black;
  width: 600px;
  text-align: center;
  margin: 40px auto;
}

#buttons {
  display: flex;
  justify-content: center;
}

button {
  background-color: #f92672;
  color: white;
  border: none;
  font-size: 2rem;
  font-weight: bold;
  padding: 1.5rem 4rem;
  margin: 1rem;
  border-radius: 30px;
  cursor: pointer;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.3);
  transition: all 0.2s;
}

button:hover {
  background-color: #f44583;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.5);
}

button[disabled] {
  opacity: 0.5;
  cursor: default;
}

@media (max-width: 800px) {
  #timer {
    font-size: 4rem;
    width: 350px;
  }

  button {
    font-size: 1.5rem;
    padding: 1rem 2rem;
  }
}



```

#### JavaScript
```
const timerEl = document.getElementById("timer");
const startButtonEl = document.getElementById("start");
const stopButtonEl = document.getElementById("stop");
const resetButtonEl = document.getElementById("reset");

let startTime = 0;
let elapsedTime = 0;
let timerInterval;

function startTimer() {
  startTime = Date.now() - elapsedTime;

  timerInterval = setInterval(() => {
    elapsedTime = Date.now() - startTime;
    timerEl.textContent = formatTime(elapsedTime);
  }, 10);

  startButtonEl.disabled = true;
  stopButtonEl.disabled = false;
}

function formatTime(elapsedTime) {
  const milliseconds = Math.floor((elapsedTime % 1000) / 10);
  const seconds = Math.floor((elapsedTime % (1000 * 60)) / 1000);
  const minutes = Math.floor((elapsedTime % (1000 * 60 * 60)) / (1000 * 60));
  const hours = Math.floor(elapsedTime / (1000 * 60 * 60));
  return (
    (hours ? (hours > 9 ? hours : "0" + hours) : "00") +
    ":" +
    (minutes ? (minutes > 9 ? minutes : "0" + minutes) : "00") +
    ":" +
    (seconds ? (seconds > 9 ? seconds : "0" + seconds) : "00") +
    "." +
    (milliseconds > 9 ? milliseconds : "0" + milliseconds)
  );
}
function stopTimer() {
  clearInterval(timerInterval);
  startButtonEl.disabled = false;
  stopButtonEl.disabled = true;
}
function resetTimer() {
  clearInterval(timerInterval);

  elapsedTime = 0;
  timerEl.textContent = "00:00:00";

  startButtonEl.disabled = false;
  stopButtonEl.disabled = true;
}

startButtonEl.addEventListener("click", startTimer);
stopButtonEl.addEventListener("click", stopTimer);
resetButtonEl.addEventListener("click", resetTimer);

```
