<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Práctica Primer Parcial Filosofía</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      background-color: #f5f5f5;
    }
    .container {
      background-color: white;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }
    h1 {
      text-align: center;
      color: #333;
      margin-bottom: 30px;
    }
    .start-screen, .question-screen, .results-screen {
      text-align: center;
    }
    .question-screen, .results-screen {
      display: none;
    }
    .question {
      font-size: 18px;
      margin-bottom: 20px;
      text-align: left;
    }
    .options {
      display: flex;
      flex-direction: column;
      gap: 10px;
      margin-bottom: 20px;
      text-align: left;
    }
    .option {
      padding: 10px 15px;
      border: 1px solid #ddd;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    .option:hover {
      background-color: #f0f0f0;
    }
    .feedback {
      margin: 20px 0;
      padding: 15px;
      border-radius: 5px;
      display: none;
    }
    .correct {
      background-color: rgba(76, 175, 80, 0.2);
      color: #2e7d32;
    }
    .incorrect {
      background-color: rgba(244, 67, 54, 0.2);
      color: #c62828;
    }
    button {
      background-color: #4caf50;
      color: white;
      border: none;
      padding: 12px 24px;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #388e3c;
    }
    .progress {
      margin-top: 20px;
      color: #666;
    }
    .score {
      font-size: 24px;
      margin-bottom: 20px;
    }
    .recommendations {
      text-align: left;
      background-color: #e3f2fd;
      padding: 15px;
      border-radius: 5px;
      margin-top: 20px;
    }
    .recommendations h3 {
      margin-top: 0;
    }
    .progress-bar {
      width: 100%;
      background-color: #e0e0e0;
      border-radius: 5px;
      margin-bottom: 20px;
    }
    .progress-bar-inner {
      height: 10px;
      background-color: #4caf50;
      border-radius: 5px;
      width: 0%;
      transition: width 0.3s ease;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Práctica Primer Parcial Filosofía</h1>
    
    <div class="start-screen">
      <p>Este es un examen de práctica para el primer parcial de Filosofía.</p>
      <p>Consta de 27 preguntas sobre diferentes autores y conceptos filosóficos.</p>
      <button id="start-btn">Comenzar Examen</button>
    </div>
    
    <div class="question-screen">
      <div class="progress-bar">
        <div class="progress-bar-inner" id="progress-bar"></div>
      </div>
      <div class="question" id="question-text"></div>
      <div class="options" id="options-container"></div>
      <div class="feedback" id="feedback"></div>
      <div class="progress" id="progress-text"></div>
    </div>
    
    <div class="results-screen">
      <h2>Resultados del Examen</h2>
      <div class="score" id="final-score"></div>
      <div class="recommendations" id="recommendations"></div>
      <button id="restart-btn">Volver a Intentar</button>
    </div>
  </div>

  <script>
    // Preguntas del examen con opciones en diferentes órdenes
    const questions = [
      {
        text: "Según Winner, las centrales nucleares de energía son un ejemplo de tecnologías:",
        options: [
          "Inherentemente políticas",
          "Como forma de orden"
        ],
        correctIndex: 0,
        author: "Winner"
      },
      {
        text: "Según Winner, la energía nuclear sería inherentemente política porque puede ser usada en las guerras:",
        options: [
          "Falso",
          "Verdadero"
        ],
        correctIndex: 0,
        author: "Winner"
      },
      {
        text: "Según Marcuse, el precondicionamiento del individuo comienza con anterioridad a la emisión masiva de la radio y la televisión:",
        options: [
          "Verdadero",
          "Falso"
        ],
        correctIndex: 0,
        author: "Marcuse"
      },
      {
        text: "Según Marcuse, las sociedades democráticas son totalitarias si su organización tecnológica no da lugar a la oposición:",
        options: [
          "Falso",
          "Verdadero"
        ],
        correctIndex: 1,
        author: "Marcuse"
      },
      {
        text: "Según Winner, los pasos bajos de Long Island son un ejemplo de tecnología:",
        options: [
          "Inherentemente políticas",
          "Como forma de orden"
        ],
        correctIndex: 1,
        author: "Winner"
      },
      {
        text: "Según Winner la introducción de máquinas forjadoras Cyrus McCormick puede verse como un ejemplo de tecnología:",
        options: [
          "Como forma de orden",
          "Inherentemente política"
        ],
        correctIndex: 0,
        author: "Winner"
      },
      {
        text: "Según Winner, las tecnologías como forma de orden no siempre tienen un origen intencional.",
        options: [
          "Falso",
          "Verdadero"
        ],
        correctIndex: 1,
        author: "Winner"
      },
      {
        text: "Según Heidegger, la 'serenidad para las cosas' implica abandonar el pensamiento calculador.",
        options: [
          "Falso",
          "Verdadero"
        ],
        correctIndex: 0,
        author: "Heidegger"
      },
      {
        text: "Según Heidegger, el pensar meditativo se aplica únicamente a cosas elevadas y es solo incumbencia de expertos.",
        options: [
          "Verdadero",
          "Falso"
        ],
        correctIndex: 1,
        author: "Heidegger"
      },
      {
        text: "Según Heidegger, en la época actual, el hombre huye el pensar:",
        options: [
          "Calculador",
          "Reflexivo"
        ],
        correctIndex: 1,
        author: "Heidegger"
      },
      {
        text: "Según Kant, por la propia naturaleza humana es:",
        options: [
          "Posible frenar el progreso hacia la ilustración",
          "Imposible frenar el progreso hacia la ilustración"
        ],
        correctIndex: 1,
        author: "Kant"
      },
      {
        text: "Según Kant, razonar libremente y obedecer son actitudes incompatibles.",
        options: [
          "Falso",
          "Verdadero"
        ],
        correctIndex: 0,
        author: "Kant"
      },
      {
        text: "Según Foucault, lo que plantea como novedoso el texto de Kant es:",
        options: [
          "La indagación sobre el pasado",
          "La reflexión sobre el presente"
        ],
        correctIndex: 1,
        author: "Foucault"
      },
      {
        text: "Según Marcuse, las necesidades humanas son:",
        options: [
          "Universales",
          "Históricas"
        ],
        correctIndex: 1,
        author: "Marcuse"
      },
      {
        text: "Según Marcuse, el progreso unidimensional de la sociedad industrial conduce hacia:",
        options: [
          "La perpetuación de la explotación",
          "La pacificación de la existencia"
        ],
        correctIndex: 0,
        author: "Marcuse"
      },
      {
        text: "Según Marcuse, uno de los aspectos más perturbadores de la civilización industrial es el carácter:",
        options: [
          "Racional de su irracionalidad",
          "Irracional de su racionalidad"
        ],
        correctIndex: 0,
        author: "Marcuse"
      },
      {
        text: "Según Foucault, la crítica de nuestro ser histórico es el motor del progreso de la humanidad.",
        options: [
          "Falso",
          "Verdadero"
        ],
        correctIndex: 1,
        author: "Foucault"
      },
      {
        text: "Según Foucault, el ethos de la modernidad implica necesariamente hacer una crítica de nuestro ser histórico.",
        options: [
          "Verdadero",
          "Falso"
        ],
        correctIndex: 0,
        author: "Foucault"
      },
      {
        text: "Según Foucault, Kant define la ilustración como una modificación de la relación preexistente entre la voluntad, la autoridad y el uso de la razón.",
        options: [
          "Falso",
          "Verdadero"
        ],
        correctIndex: 1,
        author: "Foucault"
      },
      {
        text: "Según Kant, cuando se actúa como funcionario se hace un uso de la razón:",
        options: [
          "Público",
          "Privado"
        ],
        correctIndex: 1,
        author: "Kant"
      },
      {
        text: "Según Kant, cuando se actúa y piensa libremente se hace un uso de la razón:",
        options: [
          "Privado",
          "Público"
        ],
        correctIndex: 1,
        author: "Kant"
      },
      {
        text: "Según Kant, el uso privado de la razón obstaculiza el progreso de la ilustración.",
        options: [
          "Falso",
          "Verdadero"
        ],
        correctIndex: 0,
        author: "Kant"
      },
      {
        text: "Según Foucault, la actitud de modernidad es una actitud límite porque busca comprender los límites de lo esencialmente humano.",
        options: [
          "Verdadero",
          "Falso"
        ],
        correctIndex: 1,
        author: "Foucault"
      },
      {
        text: "Según Heidegger, el hombre se encuentra en una situación de peligro porque:",
        options: [
          "La tecnología atómica puede generar la destrucción de la tierra",
          "La tecnología puede llegar a cambiar la esencia del hombre"
        ],
        correctIndex: 1,
        author: "Heidegger"
      },
      {
        text: "Según Heidegger el arraigo del hombre se encuentra hoy amenazado por la negligencia y la superficialidad del modo de la vida de los hombres.",
        options: [
          "Verdadero",
          "Falso"
        ],
        correctIndex: 1,
        author: "Heidegger"
      },
      {
        text: "Según Winner, el constructivismo social identifica la totalidad de los grupos sociales relevantes referidos a un artefacto.",
        options: [
          "Falso",
          "Verdadero"
        ],
        correctIndex: 0,
        author: "Winner"
      },
      {
        text: "Según Winner, el conocimiento social sufre de indiferencia moral y política.",
        options: [
          "Verdadero",
          "Falso"
        ],
        correctIndex: 0,
        author: "Winner"
      }
    ];

    // Variables de estado
    let currentQuestions = [];
    let currentQuestionIndex = 0;
    let score = 0;
    let incorrectAnswers = [];

    // Elementos DOM
    const startScreen = document.querySelector('.start-screen');
    const questionScreen = document.querySelector('.question-screen');
    const resultsScreen = document.querySelector('.results-screen');
    const questionText = document.getElementById('question-text');
    const optionsContainer = document.getElementById('options-container');
    const feedback = document.getElementById('feedback');
    const progressText = document.getElementById('progress-text');
    const progressBar = document.getElementById('progress-bar');
    const finalScore = document.getElementById('final-score');
    const recommendations = document.getElementById('recommendations');
    const startButton = document.getElementById('start-btn');
    const restartButton = document.getElementById('restart-btn');

    // Función para barajar el array de preguntas
    function shuffleArray(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
      return array;
    }

    // Iniciar el examen
    function startExam() {
      startScreen.style.display = 'none';
      questionScreen.style.display = 'block';
      
      // Barajar las preguntas
      currentQuestions = shuffleArray([...questions]);
      currentQuestionIndex = 0;
      score = 0;
      incorrectAnswers = [];
      
      displayQuestion();
    }

    // Mostrar la pregunta actual
    function displayQuestion() {
      const currentQuestion = currentQuestions[currentQuestionIndex];
      questionText.textContent = currentQuestion.text;
      
      // Limpiar opciones anteriores
      optionsContainer.innerHTML = '';
      
      // Crear opciones
      currentQuestion.options.forEach((option, index) => {
        const optionButton = document.createElement('div');
        optionButton.classList.add('option');
        optionButton.textContent = option;
        optionButton.addEventListener('click', () => checkAnswer(index));
        optionsContainer.appendChild(optionButton);
      });
      
      // Actualizar progreso
      progressText.textContent = `Pregunta ${currentQuestionIndex + 1} de ${currentQuestions.length}`;
      progressBar.style.width = `${((currentQuestionIndex + 1) / currentQuestions.length) * 100}%`;
      
      // Ocultar feedback
      feedback.style.display = 'none';
    }

    // Verificar respuesta
    function checkAnswer(selectedIndex) {
      const currentQuestion = currentQuestions[currentQuestionIndex];
      const isCorrect = selectedIndex === currentQuestion.correctIndex;
      
      // Mostrar feedback
      feedback.textContent = isCorrect 
        ? '¡Correcto!' 
        : `Incorrecto. La respuesta correcta es: ${currentQuestion.options[currentQuestion.correctIndex]}`;
      feedback.className = 'feedback ' + (isCorrect ? 'correct' : 'incorrect');
      feedback.style.display = 'block';
      
      // Actualizar puntuación
      if (isCorrect) {
        score++;
      } else {
        incorrectAnswers.push(currentQuestion);
      }
      
      // Deshabilitar opciones
      const options = document.querySelectorAll('.option');
      options.forEach((option, index) => {
        option.style.pointerEvents = 'none';
        if (index === currentQuestion.correctIndex) {
          option.style.backgroundColor = 'rgba(76, 175, 80, 0.2)';
          option.style.borderColor = '#2e7d32';
        } else if (index === selectedIndex && !isCorrect) {
          option.style.backgroundColor = 'rgba(244, 67, 54, 0.2)';
          option.style.borderColor = '#c62828';
        }
      });
      
      // Pasar a la siguiente pregunta después de un breve retraso
      setTimeout(() => {
        currentQuestionIndex++;
        if (currentQuestionIndex < currentQuestions.length) {
          displayQuestion();
        } else {
          showResults();
        }
      }, 1500);
    }

    // Mostrar resultados
    function showResults() {
      questionScreen.style.display = 'none';
      resultsScreen.style.display = 'block';
      
      // Calcular puntaje final (sobre 10)
      const finalScoreValue = Math.round((score / currentQuestions.length) * 10 * 100) / 100;
      finalScore.textContent = `Tu puntaje: ${finalScoreValue.toFixed(2)} / 10`;
      
      // Generar recomendaciones
      generateRecommendations();
    }

    // Generar recomendaciones basadas en respuestas incorrectas
    function generateRecommendations() {
      if (incorrectAnswers.length === 0) {
        recommendations.innerHTML = '<h3>¡Felicitaciones!</h3><p>Has respondido todas las preguntas correctamente.</p>';
        return;
      }
      
      // Contar errores por autor
      const authorErrors = {};
      incorrectAnswers.forEach(question => {
        if (!authorErrors[question.author]) {
          authorErrors[question.author] = 0;
        }
        authorErrors[question.author]++;
      });
      
      // Ordenar autores por cantidad de errores
      const sortedAuthors = Object.entries(authorErrors)
        .sort((a, b) => b[1] - a[1])
        .map(entry => ({ author: entry[0], errors: entry[1] }));
      
      // Crear recomendaciones HTML
      let recommendationsHTML = '<h3>Recomendaciones para mejorar:</h3>';
      recommendationsHTML += '<ul>';
      
      sortedAuthors.forEach(({ author, errors }) => {
        const totalQuestionsForAuthor = questions.filter(q => q.author === author).length;
        const errorPercentage = Math.round((errors / totalQuestionsForAuthor) * 100);
        
        recommendationsHTML += `<li>
          <strong>${author}:</strong> Necesitas reforzar este autor (${errors} errores de ${totalQuestionsForAuthor} preguntas, ${errorPercentage}% de error)
        </li>`;
      });
      
      recommendationsHTML += '</ul>';
      
      // Mostrar temas específicos a reforzar
      if (incorrectAnswers.length > 0) {
        recommendationsHTML += '<h3>Temas específicos a reforzar:</h3>';
        recommendationsHTML += '<ul>';
        
        // Agrupar preguntas incorrectas por autor
        const authorQuestions = {};
        incorrectAnswers.forEach(question => {
          if (!authorQuestions[question.author]) {
            authorQuestions[question.author] = [];
          }
          authorQuestions[question.author].push(question.text);
        });
        
        // Mostrar hasta 3 preguntas por autor
        Object.entries(authorQuestions).forEach(([author, questions]) => {
          recommendationsHTML += `<li><strong>${author}:</strong><ul>`;
          questions.slice(0, 3).forEach(question => {
            recommendationsHTML += `<li>${question}</li>`;
          });
          recommendationsHTML += '</ul></li>';
        });
        
        recommendationsHTML += '</ul>';
      }
      
      recommendations.innerHTML = recommendationsHTML;
    }

    // Event listeners
    startButton.addEventListener('click', startExam);
    restartButton.addEventListener('click', startExam);
  </script>
</body>
</html>
