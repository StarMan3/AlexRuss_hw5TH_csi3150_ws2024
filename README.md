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

- 