# AlexRuss_hw5TH_csi3150_ws2024

## Problem Statement
QuizAppDemo is a Web Application that brings the user through a set of quiz questions, (5 by default) about Computer Science related topics. Specifically, a handful of different acronyms. The website's landing page presents the user with a button to start the quiz. Once the user clicks the button, they are taken to the first question. The user is presented with a question and a set of multiple choice answers. The user selects an answer and clicks the "Next" button to move to the next question. After the last question, the user is presented with a summary of their answers and a button to restart the quiz or exit.

## Functional Features
- Start Quiz Button on Landing Page that takes the user to a page with the quiz rules
- Rules Pages. Consists of a brief description of the quiz and a button to start the quiz, or exit
- Each question contains a question and a set of multiple choice answers
- 15 second timer for each question, resets on each question
- Progress bar for the timer
- Upon selecting answer, instant feedback on whether the answer was correct or not. Display the correct answer if the user's answer was incorrect.
- Summary page at the end of the quiz that displays the user's score and a button to restart the quiz or exit

## Directory Structure
```
.
├── README.md
├── css
│   └── style.css
├── index.html
└── js
    ├── questions.js
    └── quizApp.js
```
The three main components here are the HTML, CSS, and JavaScript files. If the files are relocated, the file paths in the other files will need to be updated.

## Code Explanation
### index.html
- This head segment in the HTML file contains the links to the CSS file, the font awesome kit, and the JavaScript files. The JavaScript files are deferred to allow the HTML to load first.
```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz App Demo</title>

    <!-- CSS FILE -->
    <link rel="stylesheet" href="css/style.css">
    <!-- This is my personal font awesome kit code. you will have to add your own after you register with email-->
    <script src="https://kit.fontawesome.com/4a4f4b55b0.js" crossorigin="anonymous"></script>

     <!-- Add questions list -->
    <script src="js/questions.js" defer></script>

    <!-- Main logic of the app -->
    <script src="js/quizApp.js" defer></script>
</head>
```

- The first div element contains the start button for the quiz.
```html
<!-- Quiz START Button -->
    <div class="start_btn"><button>Start Quiz</button></div>
```

- Instruction Box Wrapper, contains the pop up box that displays the quiz rules, and the button to begin the quiz.
```html
<!-- Instruction box wrapper -->
<div class="info_box">
    <div class="info-title"><span>Some Rules of this Quiz</span></div>
    <div class="info-list">
        <div class="info">1. You will have only <span>15 seconds</span> per each question.</div>
        <div class="info">2. Once you select your answer, it can't be undone.</div>
        <div class="info">3. You can't select any option once time goes off.</div>
        <div class="info">4. You can't exit from the Quiz while you're playing.</div>
        <div class="info">5. You'll get points on the basis of your correct answers.</div>
    </div>
    <div class="buttons">
        <button class="quit">Exit Quiz</button>
        <button class="restart">Continue</button>
    </div>
</div>
```

- QuizBox includes 3 sections:
    - Header, contains the title, timer, and progress bar
    - Main Section, with the quiz questions. (Taken from `./js/questions.js`)
    - Footer, with the Question number and Next Question button.
```html
<!-- Quiz Box -->
<div class="quiz_box">
    <header>
        <div class="title">Demo Quiz App in JavaScript</div>
        <div class="timer">
            <div class="time_left_txt">Time Left</div>
            <div class="timer_sec">15</div>
        </div>
        <div class="time_line"></div>
    </header>
    <section>
        <div class="que_text">
            <!-- Insert questions from ./js/questions.js -->
        </div>
        <div class="option_list">
            <!-- Insert options to questions from ./js/questions.js -->
        </div>
    </section>

    <!-- footer of Quiz Box -->
    <footer>
        <div class="total_que">
            <!-- insert Question Count Number dynamically from JavaScript App logic -->
        </div>
        <button class="next_btn">Next Que</button>
    </footer>
</div>
```

- Last section of the HTML file is the result box. This section displays the user's score and a button to restart the quiz or exit.
```html
<!-- Result Box -->
<div class="result_box">
    <div class="icon">
        <i class="fas fa-crown"></i>
    </div>
    <div class="complete_text">You've completed the Quiz!</div>
    <div class="score_text">
        <!-- insert dynamic user score as Result from JavaScript -->
    </div>
    <div class="buttons">
        <button class="restart">Replay Quiz</button>
        <button class="quit">Quit Quiz</button>
    </div>
</div>
```

### style.css
The CSS file contains the styling for the entire application. The file is broken down into sections for the landing page, the quiz box, the result box, and the instruction box. Some notable additions in the file may be as follows:
- Importing a font from Google Fonts
```css
/* importing google fonts */
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap");
```

- The following code is used to change the font color and background when the user selects text on the page.
```css
::selection {
  color: #fff;
  background: #a020f0;
}
```


### questions.js
This file is for creating an array of objects that contain the quiz questions and answers. To add more questions, you can add more objects to the array. Each object should contain the question, the options, and the answer.

### quizApp.js
