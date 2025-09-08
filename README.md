<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>PROF RON ALL THE WAYYYYYYY</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f9f9f9;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    header {
      background: #2d6cdf;
      color: white;
      width: 100%;
      padding: 20px;
      text-align: center;
    }
    .container {
      max-width: 900px;
      margin: 20px;
      padding: 20px;
      background: white;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    h1 {
      margin: 0;
    }
    .question {
      margin-bottom: 20px;
      padding: 10px;
      border-bottom: 1px solid #ddd;
    }
    .options button {
      display: block;
      width: 100%;
      margin: 8px 0;
      padding: 10px;
      border: 2px solid #2d6cdf;
      border-radius: 8px;
      background: white;
      cursor: pointer;
      transition: 0.3s;
    }
    .options button:hover {
      background: #2d6cdf;
      color: white;
    }
    #result {
      margin-top: 20px;
      font-size: 20px;
      font-weight: bold;
      text-align: center;
    }
    #submitBtn {
      margin-top: 20px;
      padding: 12px 20px;
      font-size: 16px;
      border: none;
      border-radius: 8px;
      background: #2d6cdf;
      color: white;
      cursor: pointer;
    }
    #submitBtn:hover {
      background: #1a4cad;
    }
  </style>
</head>
<body>
  <header>
    <h1>GALINGAN NYO -PROF RON</h1>
    <p>Hard Level: Combined Domain & Range Questions</p>
  </header>
  <div class="container">
    <p><strong>Reminder:</strong> You’ll get 30 random questions each time. At the end, your score and percentage will be shown.</p>

    <div id="quiz"></div>
    <button id="submitBtn">Submit Quiz</button>
    <p id="result"></p>
  </div>

  <script>
    const allQuestions = [
      { q: "Find the domain and range of f(x) = 1/(x^2+1).", opts: [
          "A. Domain: all real x; Range: (0,1]",
          "B. Domain: x ≠ 0; Range: (0,∞)",
          "C. Domain: all real x; Range: (-∞,∞)",
          "D. Domain: x > 0; Range: [0,∞)"], ans: 0 },
      { q: "Find the domain and range of f(x) = √(x-2).", opts: [
          "A. Domain: x ≥ 2; Range: [0,∞)",
          "B. Domain: x > 2; Range: (0,∞)",
          "C. Domain: all real x; Range: all real x",
          "D. Domain: x ≤ 2; Range: [0,∞)"], ans: 0 },
      { q: "Find the domain and range of f(x) = √((x-1)/(x+2)).", opts: [
          "A. Domain: x ≥ 1 or x < -2; Range: [0,∞)",
          "B. Domain: x > -2; Range: (0,1]",
          "C. Domain: all real x; Range: (-∞,∞)",
          "D. Domain: x > 1; Range: [1,∞)"], ans: 0 },
      { q: "Find the domain and range of f(x) = ln(x-3).", opts: [
          "A. Domain: x > 3; Range: (-∞,∞)",
          "B. Domain: x ≥ 3; Range: [0,∞)",
          "C. Domain: x > 0; Range: (-∞,∞)",
          "D. Domain: all real x; Range: all real x"], ans: 0 },
      { q: "Find the domain and range of f(x) = e^(1/x).", opts: [
          "A. Domain: x ≠ 0; Range: (0,∞)",
          "B. Domain: all real x; Range: (0,∞)",
          "C. Domain: x > 0; Range: (0,1]",
          "D. Domain: x < 0; Range: (-∞,0)"], ans: 0 },
      { q: "Find the domain and range of f(x) = (x^2-4)/(x^2+1).", opts: [
          "A. Domain: all real x; Range: (-∞,1)",
          "B. Domain: all real x; Range: (-∞,∞)",
          "C. Domain: all real x; Range: (-1,∞)",
          "D. Domain: all real x; Range: (-∞,1)"], ans: 3 },
      { q: "Find the domain and range of f(x) = √(x^2+4).", opts: [
          "A. Domain: all real x; Range: [2,∞)",
          "B. Domain: x ≥ 0; Range: [0,∞)",
          "C. Domain: all real x; Range: (-∞,∞)",
          "D. Domain: x > 0; Range: (0,∞)"], ans: 0 },
      { q: "Find the domain and range of f(x) = (x+1)/(x-1).", opts: [
          "A. Domain: x ≠ 1; Range: all real y, y ≠ 1",
          "B. Domain: all real x; Range: (-∞,∞)",
          "C. Domain: x > 1; Range: (0,∞)",
          "D. Domain: x ≠ -1; Range: all real y"], ans: 0 },
      { q: "Find the domain and range of f(x) = 1/√(x-5).", opts: [
          "A. Domain: x > 5; Range: (0,∞)",
          "B. Domain: x ≥ 5; Range: [0,∞)",
          "C. Domain: x ≠ 5; Range: (0,∞)",
          "D. Domain: all real x; Range: (-∞,∞)"], ans: 0 },
      { q: "Find the domain and range of f(x) = log(x^2-1).", opts: [
          "A. Domain: x > 1 or x < -1; Range: (-∞,∞)",
          "B. Domain: x ≥ 1; Range: [0,∞)",
          "C. Domain: all real x; Range: (-∞,∞)",
          "D. Domain: x > 0; Range: (-∞,∞)"], ans: 0 },
    ];

    // Shuffle and pick 30
    function getRandomQuestions(arr, num) {
      return arr.sort(() => Math.random() - 0.5).slice(0, num);
    }

    const quizData = getRandomQuestions(allQuestions, Math.min(30, allQuestions.length));
    const quizContainer = document.getElementById("quiz");
    let userAnswers = new Array(quizData.length).fill(null);

    quizData.forEach((q, index) => {
      const questionDiv = document.createElement("div");
      questionDiv.classList.add("question");

      const questionText = document.createElement("p");
      questionText.textContent = (index+1) + ". " + q.q;

      const optionsDiv = document.createElement("div");
      optionsDiv.classList.add("options");

      q.opts.forEach((opt, i) => {
        const button = document.createElement("button");
        button.textContent = opt;
        button.onclick = () => {
          userAnswers[index] = i;
          Array.from(optionsDiv.children).forEach(btn => btn.style.background = "white");
          button.style.background = "#d0e2ff";
        };
        optionsDiv.appendChild(button);
      });

      questionDiv.appendChild(questionText);
      questionDiv.appendChild(optionsDiv);
      quizContainer.appendChild(questionDiv);
    });

    document.getElementById("submitBtn").onclick = () => {
      let score = 0;
      quizData.forEach((q, i) => {
        if (userAnswers[i] === q.ans) score++;
      });
      let percent = ((score/quizData.length)*100).toFixed(2);
      document.getElementById("result").textContent = `Score: ${score}/${quizData.length}  (${percent}%)`;
    };
  </script>
</body>
</html>
