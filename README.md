<!DOCTYPE html>
<html>
<head>
    <title>FITNESS QUIZ GEN Z</title>
    <style>
        #quiz-popup {
            position: fixed;
            right: 20px;
            bottom: 20px;
            width: 180px;
            background: linear-gradient(45deg, #ff6b6b, #ffa502);
            color: white;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(255, 107, 107, 0.7);
            cursor: pointer;
            font-family: 'Arial', sans-serif;
            text-align: center;
            animation: pulse 2s infinite;
            z-index: 1000;
        }
        
        #quiz-container {
            display: none;
            position: fixed;
            right: 20px;
            bottom: 20px;
            width: 300px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 0 30px rgba(0,0,0,0.2);
            padding: 20px;
            z-index: 1001;
            font-family: 'Arial', sans-serif;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .question {
            font-weight: bold;
            margin-bottom: 10px;
        }
        
        .options {
            display: flex;
            justify-content: space-between;
            margin-top: 15px;
        }
        
        .option-btn {
            padding: 8px 15px;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            font-weight: bold;
            transition: transform 0.2s;
        }
        
        .option-btn:hover {
            transform: scale(1.05);
        }
        
        .yes-btn {
            background: #2ed573;
            color: white;
        }
        
        .no-btn {
            background: #ff4757;
            color: white;
        }
        
        #answer-status {
            margin: 10px 0;
            font-weight: bold;
            font-size: 16px;
            min-height: 24px;
        }
        
        #funny-comment {
            font-style: italic;
            color: #555;
            margin-bottom: 10px;
            min-height: 40px;
        }
        
        #result {
            font-weight: bold;
            margin-top: 15px;
            font-size: 18px;
            color: #ff6b6b;
            min-height: 60px;
        }
        
        #next-btn {
            background: #3498db;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 20px;
            margin-top: 15px;
            cursor: pointer;
            display: none;
            transition: background 0.3s;
        }
        
        #next-btn:hover {
            background: #2980b9;
        }
        
        .grade-SS { 
            color: #ff00aa; 
            text-shadow: 0 0 5px rgba(255,0,170,0.3);
            font-size: 1.2em;
        }
        .grade-S  { 
            color: #ff6600;
            font-size: 1.1em;
        }
        .grade-B  { 
            color: #0095ff;
        }
        .grade-D  { 
            color: #666; 
            font-style: italic;
        }
        
        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #f00;
            border-radius: 50%;
        }
    </style>
</head>
<body>
    <!-- Pulsierendes Popup -->
    <div id="quiz-popup">
        FITNESS QUIZ GEN Z
    </div>
    
    <!-- Quiz Container (versteckt) -->
    <div id="quiz-container">
        <div class="question" id="question">Frage wird geladen...</div>
        <div id="answer-status"></div>
        <div id="funny-comment"></div>
        <div class="options">
            <button class="option-btn yes-btn" id="yes-btn">Ja</button>
            <button class="option-btn no-btn" id="no-btn">Nein</button>
        </div>
        <div id="result"></div>
        <button id="next-btn">Nächste Frage</button>
    </div>

    <script>
        // Witzige Fitness-Fragen für Gen Z (10 Fragen)
        const questions = [
            {
                question: "Ist 'Ich geh später ins Gym' ein akzeptabler Grund, um heute nichts zu machen?",
                answer: false,
                explanation: "Nice try – aber Nein! (Außer 'später' ist in 5 Minuten)"
            },
            {
                question: "Zählt Pizza essen als 'Cheat Day', wenn man dabei Liegestütze macht?",
                answer: false,
                explanation: "1 Liegestütz = 1 Kalorie verbrannt. Reicht nicht für ne ganze Pizza!"
            },
            {
                question: "Kann man Proteinshakes durch einen Big Mac ersetzen wenn man 'Bulking' macht?",
                answer: false,
                explanation: "Big Mac Protein? Nur wenn dein Muskelziel 'Marshmallow-Mode' ist"
            },
            {
                question: "Ist es ok, im Gym Selfies zu machen, wenn man wenigstens 1 Übung macht?",
                answer: true,
                explanation: "1 Übung = 10 Selfies. Das ist Gym-Mathematik!"
            },
            {
                question: "Zählt Schlaf als Recovery, wenn man dabei von Fitness träumt?",
                answer: false,
                explanation: "Träume zählen nur, wenn du im Schlaf tatsächlich Gains machst"
            },
            {
                question: "Darf man stolz auf sein Sixpack sein, wenn es nur vom Hungern kommt?",
                answer: false,
                explanation: "Sixpack durch Hungern? Das nennt man 'Airbag-Mode' 💨"
            },
            {
                question: "Ist ein 10-Minuten-Workout besser als gar keins?",
                answer: true,
                explanation: "10 Minuten > 0 Minuten. Basic Mathe, Bro! ➗"
            },
            {
                question: "Kann man sich als Sportler bezeichnen, wenn man nur FIFA zockt?",
                answer: false,
                explanation: "FIFA zocken trainiert nur deinen Daumen (und dein Ego) 🎮"
            },
            {
                question: "Zählt Treppensteigen als Cardio, wenn man nur zum Kühlschrank geht?",
                answer: false,
                explanation: "Nur wenn dein Kühlschrank im 10. Stock steht 🏢"
            },
            {
                question: "Ist es ein Fortschritt, wenn man wenigstens ans Gym denkt?",
                answer: true,
                explanation: "Gedankengains sind immerhin besser als gar keine Gains! 💭"
            }
        ];

        // Witzige Reaktionen
        const correctReactions = [
            "Newton bist du's? 🧠",
            "Dayuum! 🔥",
            "Let him cook! 👨‍🍳",
            "Big Brain Time! 🧠💡",
            "G.O.A.T. Status! 🐐"
        ];
        
        const wrongReactions = [
            "Dummy! 🤦‍♂️",
            "Stooopid! 🙈",
            "Lightheaded much? 💨",
            "Bruh... 😬",
            "Who hurt you? 🩹"
        ];

        // Benotungssystem (SS, S, B, D+)
        function getGrade(score) {
            if (score >= 9) return { grade: "SS", class: "grade-SS" };
            if (score >= 7) return { grade: "S", class: "grade-S" };
            if (score >= 5) return { grade: "B", class: "grade-B" };
            return { grade: "D+", class: "grade-D" };
        }

        // Witzige Ergebnisse
        const gradeComments = {
            "SS": [
                "SS-RANK! Dein Wissen ist so sharp wie ein Sixpack nach 1 Monat Gym! 💎",
                "SS wie 'Supersaiyajin' – Du hast den Fitness-Code geknackt! 🐉"
            ],
            "S": [
                "S wie 'Stark' – Fast perfekt, aber Pizza ist trotzdem kein Protein! 🍕",
                "S-Rank! Du weißt Bescheid... meistens jedenfalls! 👍"
            ],
            "B": [
                "B wie 'Basic' – Dein Fitness-Wissen ist so mittelmäßig wie dein Gym-Outfit. 🧦",
                "B-Level: Du kennst die Basics, aber Cheat Days kennst du besser. 🍔"
            ],
            "D+": [
                "D+ wie 'Durchgefallen+' – Dein Fitness-Wissen besteht aus Gym-TikToks. 📱",
                "D+ für 'Damn...' – Zeit, weniger zu scrollen, mehr zu lernen! 📚"
            ]
        };

        // Quiz Variablen
        let currentQuestion = 0;
        let score = 0;
        let shuffledQuestions = [];
        
        // DOM Elemente
        const quizPopup = document.getElementById('quiz-popup');
        const quizContainer = document.getElementById('quiz-container');
        const questionElement = document.getElementById('question');
        const answerStatus = document.getElementById('answer-status');
        const funnyComment = document.getElementById('funny-comment');
        const yesBtn = document.getElementById('yes-btn');
        const noBtn = document.getElementById('no-btn');
        const resultElement = document.getElementById('result');
        const nextBtn = document.getElementById('next-btn');
        
        // Quiz starten
        quizPopup.addEventListener('click', startQuiz);
        
        function startQuiz() {
            quizPopup.style.display = 'none';
            quizContainer.style.display = 'block';
            currentQuestion = 0;
            score = 0;
            shuffleQuestions();
            showQuestion();
        }
        
        function shuffleQuestions() {
            // Erstelle eine Kopie aller Fragen und mische sie
            shuffledQuestions = [...questions];
            for (let i = shuffledQuestions.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [shuffledQuestions[i], shuffledQuestions[j]] = [shuffledQuestions[j], shuffledQuestions[i]];
            }
            // Nimm nur die ersten 10 Fragen (falls mehr vorhanden wären)
            shuffledQuestions = shuffledQuestions.slice(0, 10);
        }
        
        function showQuestion() {
            if (currentQuestion < shuffledQuestions.length) {
                const q = shuffledQuestions[currentQuestion];
                questionElement.textContent = `Frage ${currentQuestion + 1}/${shuffledQuestions.length}: ${q.question}`;
                answerStatus.textContent = '';
                funnyComment.textContent = '';
                nextBtn.style.display = 'none';
            } else {
                showResult();
            }
        }
        
        function checkAnswer(userAnswer) {
            const q = shuffledQuestions[currentQuestion];
            const isCorrect = (userAnswer === q.answer);
            
            if (isCorrect) {
                score++;
                answerStatus.textContent = "✅ Richtig!";
                answerStatus.style.color = "#2ed573";
                funnyComment.textContent = correctReactions[Math.floor(Math.random() * correctReactions.length)];
                createConfetti();
            } else {
                answerStatus.textContent = "❌ Falsch!";
                answerStatus.style.color = "#ff4757";
                funnyComment.textContent = wrongReactions[Math.floor(Math.random() * wrongReactions.length)] + " " + q.explanation;
            }
            
            nextBtn.style.display = 'block';
        }
        
        function showResult() {
            const grade = getGrade(score);
            const randomComment = gradeComments[grade.grade][Math.floor(Math.random() * gradeComments[grade.grade].length)];
            
            questionElement.textContent = "Quiz beendet!";
            answerStatus.innerHTML = `Punkte: <span class="${grade.class}">${score}/${shuffledQuestions.length} (${grade.grade})</span>`;
            funnyComment.textContent = '';
            resultElement.innerHTML = `<div class="${grade.class}">${randomComment}</div>`;
            yesBtn.style.display = 'none';
            noBtn.style.display = 'none';
            nextBtn.textContent = 'Quiz neu starten';
            
            if (grade.grade === "SS") {
                createConfetti(true);
            }
        }
        
        function createConfetti(isBig = false) {
            const colors = ['#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff', '#00ffff'];
            const container = document.getElementById('quiz-container');
            const count = isBig ? 50 : 20;
            
            for (let i = 0; i < count; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.left = Math.random() * 280 + 'px';
                confetti.style.top = Math.random() * 300 + 'px';
                confetti.style.width = (Math.random() * 10 + 5) + 'px';
                confetti.style.height = (Math.random() * 10 + 5) + 'px';
                container.appendChild(confetti);
                
                // Entferne Confetti nach der Animation
                setTimeout(() => {
                    confetti.remove();
                }, 1000);
            }
        }
        
        // Event Listener
        yesBtn.addEventListener('click', () => checkAnswer(true));
        noBtn.addEventListener('click', () => checkAnswer(false));
        
        nextBtn.addEventListener('click', () => {
            if (currentQuestion < shuffledQuestions.length - 1) {
                currentQuestion++;
                showQuestion();
            } else if (currentQuestion === shuffledQuestions.length - 1) {
                currentQuestion++;
                showResult();
            } else {
                // Quiz neu starten
                startQuiz();
            }
        });
    </script>
</body>
</html>
