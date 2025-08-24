<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Advanced Styling and JavaScript Actions</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
      background: #f6f9f8;
    }

    h2 {
      margin-top: 30px;
      color: #0d7a5c;
    }

    /* 1. Responsive Design Demo */
    .container {
      display: grid;
      grid-template-columns: 1fr;
      gap: 20px;
    }

    .box {
      padding: 20px;
      background: #e3f7f1;
      border-radius: 10px;
      text-align: center;
      font-size: 16px;
    }

    /* Tablet */
    @media (min-width: 600px) {
      .container {
        grid-template-columns: 1fr 1fr;
      }
      .box {
        background: #c9f0e3;
        font-size: 18px;
      }
    }

    /* Desktop */
    @media (min-width: 900px) {
      .container {
        grid-template-columns: 1fr 1fr 1fr;
      }
      .box {
        background: #a8e4d4;
        font-size: 20px;
      }
    }

    /* 2. Quiz */
    .quiz {
      margin-top: 20px;
      padding: 15px;
      background: #fff;
      border-radius: 10px;
      border: 1px solid #ddd;
    }

    .quiz button {
      margin: 5px 0;
      padding: 10px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      background: #0d7a5c;
      color: #fff;
      display: block;
      width: 100%;
      text-align: left;
    }

    .quiz button:hover {
      background: #0b614a;
    }

    .result {
      margin-top: 10px;
      font-weight: bold;
    }

    /* 3. API Fetch */
    .api {
      margin-top: 20px;
      padding: 15px;
      background: #fff;
      border-radius: 10px;
      border: 1px solid #ddd;
    }

    .api button {
      padding: 10px 15px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      background: #0d7a5c;
      color: #fff;
    }

    .api button:hover {
      background: #0b614a;
    }

    .api p {
      margin-top: 15px;
      padding: 10px;
      background: #f0f0f0;
      border-radius: 8px;
    }
  </style>
</head>
<body>

  <h2>1. Responsive Design Using Media Queries</h2>
  <div class="container">
    <div class="box">Box 1</div>
    <div class="box">Box 2</div>
    <div class="box">Box 3</div>
  </div>

  <h2>2. Interactive Quiz</h2>
  <div class="quiz" id="quiz">
    <div class="q" data-answer="b">
      <p><b>Q1.</b> Which CSS at-rule helps with responsive design?</p>
      <button data-choice="a">@font-face</button>
      <button data-choice="b">@media</button>
      <button data-choice="c">@keyframes</button>
      <p class="result"></p>
    </div>

    <div class="q" data-answer="c">
      <p><b>Q2.</b> Which JavaScript method is used to fetch API data?</p>
      <button data-choice="a">getElementById()</button>
      <button data-choice="b">map()</button>
      <button data-choice="c">fetch()</button>
      <p class="result"></p>
    </div>
  </div>

  <h2>3. Fetch Data from API</h2>
  <div class="api">
    <button onclick="fetchJoke()">Get Random Joke</button>
    <p id="joke">Click the button to fetch a joke.</p>
  </div>

  <script>
    // Quiz Logic
    document.querySelectorAll(".q").forEach(q => {
      const answer = q.dataset.answer;
      const result = q.querySelector(".result");

      q.querySelectorAll("button").forEach(btn => {
        btn.addEventListener("click", () => {
          if (btn.dataset.choice === answer) {
            result.textContent = "✅ Correct!";
            result.style.color = "green";
          } else {
            result.textContent = "❌ Wrong! Try again.";
            result.style.color = "red";
          }
        });
      });
    });

    // Fetch API Logic (Joke)
    async function fetchJoke() {
      const jokeBox = document.getElementById("joke");
      jokeBox.textContent = "Loading...";
      try {
        const response = await fetch("https://official-joke-api.appspot.com/random_joke");
        const data = await response.json();
        jokeBox.textContent = `${data.setup} — ${data.punchline}`;
      } catch (error) {
        jokeBox.textContent = "Error fetching joke. Try again.";
      }
    }
  </script>

</body>
</html>
