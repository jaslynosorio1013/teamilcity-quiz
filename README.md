# teamilcity-quiz
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Teamilcity Quiz</title>
<style>
  body { font-family: Arial, sans-serif; background: #f0f8ff; color: #333; max-width: 600px; margin: 30px auto; padding: 20px; border-radius: 8px; box-shadow: 0 0 10px #aaa; }
  h1 { color: #3a6ea5; }
  .question { margin-bottom: 15px; }
  button { background: #3a6ea5; color: white; border: none; padding: 10px 15px; margin-top: 10px; border-radius: 5px; cursor: pointer; }
  button:hover { background: #335a84; }
  .feedback { margin-top: 10px; font-weight: bold; }
  .correct { color: green; }
  .incorrect { color: red; }
  #score { font-size: 1.2em; margin-top: 20px; }
</style>
</head>
<body>

<h1>Test Your Knowledge: Teamilcity, Goddess of Teamwork</h1>

<div id="quiz-container">
  <div id="question-container"></div>
  <button id="next-btn" style="display:none;">Next</button>
</div>

<div id="score" style="display:none;"></div>

<script>
const quizData = [
  {
    question: "Who created Teamilcity?",
    choices: [
      "Zeus alone",
      "Primorion and Harmonia together",
      "Ares and Zeus",
      "Hera and Athena"
    ],
    answer: 1
  },
  {
    question: "What is Teamilcity's main role?",
    choices: [
      "To lead battles with strength",
      "To bring unity and teamwork",
      "To control the seasons",
      "To rule over the seas"
    ],
    answer: 1
  },
  {
    question: "Which symbol does Teamilcity carry?",
    choices: [
      "A sword of fire",
      "A banner with five hands joined in a circle",
      "A lightning bolt",
      "A shield with a star"
    ],
    answer: 1
  },
  {
    question: "What power helps Teamilcity boost team strength?",
    choices: [
      "Shared Strength",
      "Voice of Harmony",
      "Clone of Collaboration",
      "Link of Minds"
    ],
    answer: 0
  },
  {
    question: "What happened when the gods fought alone?",
    choices: [
      "They won every battle",
      "The world below suffered and chaos grew",
      "They created peace",
      "Teamilcity was defeated"
    ],
    answer: 1
  }
];

const questionContainer = document.getElementById('question-container');
const nextBtn = document.getElementById('next-btn');
const scoreDiv = document.getElementById('score');

let currentQuestion = 0;
let score = 0;

function showQuestion() {
  nextBtn.style.display = 'none';
  scoreDiv.style.display = 'none';
  questionContainer.innerHTML = '';

  const q = quizData[currentQuestion];

  const questionElem = document.createElement('div');
  questionElem.className = 'question';
  questionElem.textContent = `Q${currentQuestion + 1}: ${q.question}`;
  questionContainer.appendChild(questionElem);

  q.choices.forEach((choice, index) => {
    const btn = document.createElement('button');
    btn.textContent = choice;
    btn.onclick = () => selectAnswer(index);
    questionContainer.appendChild(btn);
  });

  const feedback = document.createElement('div');
  feedback.id = 'feedback';
  feedback.className = 'feedback';
  questionContainer.appendChild(feedback);
}

function selectAnswer(selected) {
  const q = quizData[currentQuestion];
  const feedback = document.getElementById('feedback');

  // Disable all buttons
  const buttons = questionContainer.querySelectorAll('button');
  buttons.forEach(btn => btn.disabled = true);

  if (selected === q.answer) {
    feedback.textContent = 'Correct! 🎉';
    feedback.className = 'feedback correct';
    score++;
  } else {
    feedback.textContent = `Incorrect. The right answer is: "${q.choices[q.answer]}".`;
    feedback.className = 'feedback incorrect';
  }
  nextBtn.style.display = 'inline-block';
}

nextBtn.onclick = () => {
  currentQuestion++;
  if (currentQuestion < quizData.length) {
    showQuestion();
  } else {
    showScore();
  }
};

function showScore() {
  questionContainer.innerHTML = '';
  nextBtn.style.display = 'none';
  scoreDiv.style.display = 'block';
  scoreDiv.textContent = `You scored ${score} out of ${quizData.length}! Thanks for playing.`;
}

showQuestion();
</script>

</body>
</html>