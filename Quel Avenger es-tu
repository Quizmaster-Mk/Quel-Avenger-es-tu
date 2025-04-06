<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quel Avenger êtes-vous ?</title>
  <style>
    body {
      font-family: 'Courier New', monospace;
      background-color: #0a1a3f;
      color: #fff;
      margin: 0;
      padding: 20px;
      text-align: center;
    }

    h1 {
      color: #ffcc00;
      text-shadow: 2px 2px 5px #ff5733;
      font-size: 40px;
      margin-bottom: 30px;
      animation: flicker 1s infinite;
    }

    .logo {
      width: 150px;
      margin-bottom: 20px;
    }

    .question {
      margin: 20px 0;
      background-color: #1f3d7a;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(255, 204, 0, 0.7);
      color: white;
    }

    .options button {
      background-color: #4f83ff;
      color: #fff;
      padding: 10px 20px;
      border: none;
      margin: 5px;
      font-size: 18px;
      cursor: pointer;
      border-radius: 5px;
      box-shadow: 0 0 5px #007bff;
      transition: all 0.3s ease;
    }

    .options button:hover {
      background-color: #1a5cff;
      transform: scale(1.1);
    }

    .result {
      background-color: #1f3d7a;
      padding: 20px;
      border-radius: 10px;
      margin-top: 20px;
      display: none;
      box-shadow: 0 0 10px rgba(255, 204, 0, 0.7);
    }

    .score {
      font-size: 18px;
      margin-top: 10px;
      color: #ffcc00;
    }

    @keyframes flicker {
      0% { opacity: 0.8; }
      50% { opacity: 1; }
      100% { opacity: 0.8; }
    }
  </style>
</head>
<body>
  <img src="https://zupimages.net/up/21/41/1ypk.png" alt="Logo Avengers" class="logo">
  <h1>Quel Avenger êtes-vous ?</h1>
  <div id="quiz-container">
    <div class="question" id="question-container">
      <h2 id="question-text"></h2>
      <div class="options" id="options-container"></div>
    </div>
  </div>
  <div class="result" id="result-container">
    <h2>Vous êtes...</h2>
    <p id="result-text"></p>
    <p class="score">Votre résultat est basé sur vos choix !</p>
    <button onclick="startQuiz()">Recommencer le quiz</button>
  </div>
  <script>
    const questions = [
      { question: "Quel est votre plus grand atout ?", options: ["Force", "Intelligence", "Vitesse", "Détermination"], result: [0, 1, 2, 3] },
      { question: "Quelle est votre faiblesse ?", options: ["Trop émotionnel", "Arrogance", "Solitude", "Trop direct"], result: [2, 0, 3, 1] },
      { question: "Quelle est votre arme de prédilection ?", options: ["Un marteau", "Un arc", "Une armure", "Mes poings"], result: [4, 5, 1, 0] },
      { question: "Votre mission idéale ?", options: ["Sauver le monde", "Protéger ma famille", "Vaincre les méchants", "Inspirer les autres"], result: [1, 3, 0, 2] },
      { question: "Votre qualité principale ?", options: ["Leadership", "Courage", "Humour", "Fidélité"], result: [3, 0, 6, 5] },
      { question: "Quel environnement vous décrit le mieux ?", options: ["Un labo", "Le champ de bataille", "Une planète alien", "Un entraînement militaire"], result: [1, 0, 6, 3] },
      { question: "Quel genre d'équipe préférez-vous ?", options: ["Petite mais soudée", "Multinationale", "Céleste et cosmique", "Juste moi"], result: [5, 3, 6, 0] },
      { question: "Quel pouvoir aimeriez-vous avoir ?", options: ["Contrôler les éléments", "Voler", "Lire dans les pensées", "Se régénérer"], result: [4, 1, 2, 0] },
      { question: "Comment réagissez-vous au stress ?", options: ["Je fonce sans réfléchir", "Je plaisante", "Je planifie", "Je me renferme"], result: [0, 6, 1, 2] },
      { question: "Votre ennemi juré serait ?", options: ["Un dieu", "Un tyran galactique", "Un rival d’enfance", "Un clone maléfique"], result: [4, 6, 1, 2] },
    ];

    const characters = [
      { name: "Hulk", description: "Puissance brute et colère incontrôlée, mais un cœur immense." },
      { name: "Iron Man", description: "Génie milliardaire en armure, stratège et visionnaire." },
      { name: "Scarlet Witch", description: "Maîtresse de la réalité, puissante mais émotionnellement fragile." },
      { name: "Captain America", description: "Symbole du courage et du devoir, un vrai leader." },
      { name: "Thor", description: "Dieu du tonnerre, loyal et protecteur." },
      { name: "Hawkeye", description: "Discret mais redoutable, force tranquille de l'équipe." },
      { name: "Star-Lord", description: "Aventurier galactique, drôle et imprévisible." },
      { name: "Black Widow", description: "Espionne redoutable, calme et efficace." },
      { name: "Falcon", description: "Fidèle et loyal, toujours prêt à se battre pour les autres." },
      { name: "Doctor Strange", description: "Maître des arts mystiques, sage et puissant." }
    ];

    let currentQuestion = 0;
    let userAnswers = [];

    function startQuiz() {
      currentQuestion = 0;
      userAnswers = [];
      document.getElementById('result-container').style.display = 'none';
      document.getElementById('quiz-container').style.display = 'block';
      showQuestion();
    }

    function showQuestion() {
      const question = questions[currentQuestion];
      document.getElementById('question-text').innerText = question.question;
      const optionsContainer = document.getElementById('options-container');
      optionsContainer.innerHTML = '';
      question.options.forEach((option, index) => {
        const button = document.createElement('button');
        button.innerText = option;
        button.onclick = () => {
          userAnswers.push(question.result[index]);
          currentQuestion++;
          if (currentQuestion < questions.length) {
            showQuestion();
          } else {
            showResult();
          }
        };
        optionsContainer.appendChild(button);
      });
    }

    function showResult() {
      const counts = Array(characters.length).fill(0);
      userAnswers.forEach(i => counts[i]++);
      const maxIndex = counts.indexOf(Math.max(...counts));
      const result = characters[maxIndex];
      document.getElementById('result-text').innerText = `${result.name} - ${result.description}`;
      document.getElementById('quiz-container').style.display = 'none';
      document.getElementById('result-container').style.display = 'block';
    }

    startQuiz();
  </script>
</body>
</html>
