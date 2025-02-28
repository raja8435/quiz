
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Application</title>
    <style>
        /* styles.css */
        body {
            font-family: Arial, sans-serif;
            background: #f4f4f9;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .quiz-container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            width: 400px;
            text-align: center;
        }

        h1 {
            margin-bottom: 20px;
            color: #333;
        }

        .question-container {
            margin-bottom: 20px;
        }

        .options-list {
            list-style: none;
            padding: 0;
        }

        .options-list li {
            background: #f9f9f9;
            margin: 10px 0;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            cursor: pointer;
            transition: background 0.3s;
        }

        .options-list li:hover {
            background: #ddd;
        }

        .btn {
            background: #007bff;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background 0.3s;
        }

        .btn:hover {
            background: #0056b3;
        }

        .hidden {
            display: none;
        }
    </style>
</head>

<body>
    <div class="quiz-container">
        <h1>Quiz Application</h1>
        <div id="quiz">
            <div class="question-container">
                <h3 id="question">Question will appear here</h3>
                <ul id="options" class="options-list">
                    <!-- Options will be inserted dynamically here -->
                </ul>
            </div>
            <button id="next-btn" class="btn">Next</button>
        </div>
        <div id="result" class="hidden">
            <h2>Your Score: <span id="score">0</span></h2>
            <button id="restart-btn" class="btn">Restart</button>
        </div>
    </div>
    <script>

        const quizData = [
            {
                question: "What is the capital of France?",
                options: ["Berlin", "Madrid", "Paris", "Lisbon"],
                correct: "Paris",
            },
            {
                question: "Which programming language is used for web development?",
                options: ["Python", "C++", "JavaScript", "Java"],
                correct: "JavaScript",
            },
            {
                question: "Which year did India get independence?",
                options: ["1945", "1947", "1950", "1952"],
                correct: "1947",
            },
            {
                question: "Who is the leader of opposition in 2024",
                options: ["Nanerdra Modi","Rahul Gandhi","Alvish Yadav","Salman Khan"],
                correct: "Rahul Gandhi",
            }
        ];

        let currentQuestionIndex = 0;
        let score = 0;

        const questionElement = document.getElementById("question");
        const optionsElement = document.getElementById("options");
        const nextButton = document.getElementById("next-btn");
        const resultContainer = document.getElementById("result");
        const scoreElement = document.getElementById("score");
        const restartButton = document.getElementById("restart-btn");

        function loadQuestion() {
            const currentQuestion = quizData[currentQuestionIndex];
            questionElement.textContent = currentQuestion.question;

            optionsElement.innerHTML = "";
            currentQuestion.options.forEach((option) => {
                const li = document.createElement("li");
                li.textContent = option;
                li.addEventListener("click", () => handleOptionClick(li, currentQuestion.correct));
                optionsElement.appendChild(li);
            });
        }

        function handleOptionClick(selectedOption, correctAnswer) {
            const options = optionsElement.querySelectorAll("li");
            options.forEach((option) => (option.style.pointerEvents = "none"));

            if (selectedOption.textContent === correctAnswer) {
                selectedOption.style.backgroundColor = "#c8e6c9"; // Green for correct
                score++;
            } else {
                selectedOption.style.backgroundColor = "#ffcdd2"; // Red for incorrect
            }
        }

        function nextQuestion() {
            currentQuestionIndex++;
            if (currentQuestionIndex < quizData.length) {
                loadQuestion();
            } else {
                showResult();
            }
        }

        function showResult() {
            document.getElementById("quiz").classList.add("hidden");
            resultContainer.classList.remove("hidden");
            scoreElement.textContent = score;
        }

        function restartQuiz() {
            currentQuestionIndex = 0;
            score = 0;
            resultContainer.classList.add("hidden");
            document.getElementById("quiz").classList.remove("hidden");
            loadQuestion();
        }

        nextButton.addEventListener("click", nextQuestion);
        restartButton.addEventListener("click", restartQuiz);

        // Initial load
        loadQuestion();</script>
</body>

</html>
