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
- The first group of lines is used to declare the variables used throughout the application. 
- The following lines of code are for when the user clicks a button in the application:
```js
// if startQuiz button clicked
start_btn.addEventListener("click", (e) => {
  info_box.classList.add("activeInfo"); //show info box
});

// if exitQuiz button clicked
exit_btn.addEventListener("click", (e) => {
  info_box.classList.remove("activeInfo"); //hide info box
});

// if continueQuiz button clicked
continue_btn.addEventListener("click", (e) => {
  info_box.classList.remove("activeInfo"); //hide info box
  quiz_box.classList.add("activeQuiz"); //show quiz box
  showQuetions(0); //calling showQestions function
  queCounter(1); //passing 1 parameter to queCounter
  startTimer(15); //calling startTimer function
  startTimerLine(0); //calling startTimerLine function
});
```

- If the user presses the Restart Quiz button, the following code is executed:
```js
// if restartQuiz button clicked
restart_quiz.addEventListener("click", (e) => {
  quiz_box.classList.add("activeQuiz"); //show quiz box
  result_box.classList.remove("activeResult"); //hide result box
  timeValue = 15;
  que_count = 0;
  que_numb = 1;
  userScore = 0;
  widthValue = 0;
  showQuetions(que_count); //calling showQestions function
  queCounter(que_numb); //passing que_numb value to queCounter
  clearInterval(counter); //clear counter
  clearInterval(counterLine); //clear counterLine
  startTimer(timeValue); //calling startTimer function
  startTimerLine(widthValue); //calling startTimerLine function
  timeText.textContent = "Time Left"; //change the text of timeText to Time Left
  next_btn.classList.remove("show"); //hide the next button
});
```

- The next button is used to move to the next question in the quiz. If the user is on the final question, the button will instead show the user's score.
The following code is executed when the user clicks the Next Question button:
```js
// if Next Question button is clicked
next_btn.addEventListener("click", (e) => {
  //check if it does not exceed max questions
  if (que_count < questions.length - 1) {
    que_count++; //increment the que_count value
    que_numb++; //increment the que_numb value
    showQuetions(que_count); //calling showQestions function
    queCounter(que_numb); //passing que_numb value to queCounter
    clearInterval(counter); //clear counter
    clearInterval(counterLine); //clear counterLine
    startTimer(timeValue); //calling startTimer function
    startTimerLine(widthValue); //calling startTimerLine function
    timeText.textContent = "Time Left"; //change the timeText to Time Left
    next_btn.classList.remove("show"); //hide the next button
  } else {
    clearInterval(counter); //clear counter
    clearInterval(counterLine); //clear counterLine
    showResult(); //calling showResult function
  }
});
```

- The showQuestions function takes all of the questions from the questions.js file and makes a HTML element to display it to the user.
```js
// getting questions and options from array
// If you have lesser or more number of options you need to change this code
function showQuetions(index) {
  const que_text = document.querySelector(".que_text");

  //creating a new span and div tag for question and option and passing the value using array index
  // self exercise: re-write the following using backtick syntax for string in JS instead of concatenation operator
  let que_tag =
    "<span>" +
    questions[index].numb +
    ". " +
    questions[index].question +
    "</span>";
  let option_tag =
    '<div class="option"><span>' +
    questions[index].options[0] +
    "</span></div>" +
    '<div class="option"><span>' +
    questions[index].options[1] +
    "</span></div>" +
    '<div class="option"><span>' +
    questions[index].options[2] +
    "</span></div>" +
    '<div class="option"><span>' +
    questions[index].options[3] +
    "</span></div>";
  que_text.innerHTML = que_tag; //adding new (child) span tag inside que_tag
  option_list.innerHTML = option_tag; //adding new (child) div tag inside option_tag

  const option = option_list.querySelectorAll(".option");

  // set onclick attribute to all available options
  for (i = 0; i < option.length; i++) {
    option[i].setAttribute("onclick", "optionSelected(this)");
  }
}
```

- The optionsSelected function is used to check if the user's answer is correct or not. If the user's answer is correct, the user's score is incremented. If the user's answer is incorrect, the correct answer is displayed to the user.
```js
//if user clicked on option
function optionSelected(answer) {
  clearInterval(counter); //clear counter
  clearInterval(counterLine); //clear counterLine
  let userAns = answer.textContent; //getting user selected option
  let correcAns = questions[que_count].answer; //getting correct answer from array
  const allOptions = option_list.children.length; //getting all option items

  //if user selected option is equal to array's correct answer
  if (userAns == correcAns) {
    userScore += 1; //update total score value increment by 1
    answer.classList.add("correct"); //add green color to correct selected option
    answer.insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to correct selected option
    console.log("Correct Answer");
    console.log("Your correct answers = " + userScore);
  } else {
    answer.classList.add("incorrect"); //add red color to correct selected option
    answer.insertAdjacentHTML("beforeend", crossIconTag); //add cross icon to correct selected option
    console.log("Wrong Answer");

    for (i = 0; i < allOptions; i++) {
      if (option_list.children[i].textContent == correcAns) {
        //if there is an option which is matched to an array answer
        option_list.children[i].setAttribute("class", "option correct"); //add green color to matched option
        option_list.children[i].insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to matched option
        console.log("Auto selected correct answer.");
      }
    }
  }
  for (i = 0; i < allOptions; i++) {
    option_list.children[i].classList.add("disabled"); //once user select an option, disable all options
  }
  next_btn.classList.add("show"); //show the next button if user selected any option
}
```

- The showResult function is used to display the user's score and a message based on their performance. If the user scored more than 3, they are congratulated. If the user scored more than 1, they are told "nice". If the user scored less than 1, they are told "sorry".
```js
// display for result box based on user performance
function showResult() {
  info_box.classList.remove("activeInfo"); //hide info box
  quiz_box.classList.remove("activeQuiz"); //hide quiz box
  result_box.classList.add("activeResult"); //show result box
  const scoreText = result_box.querySelector(".score_text");
  if (userScore > 3) {
    // if user scored more than 3
    //create a new span tag and pass the user score number and total question number
    let scoreTag =
      "<span>and congrats! , You got <p>" +
      userScore +
      "</p> out of <p>" +
      questions.length +
      "</p></span>";
    scoreText.innerHTML = scoreTag; //add new span tag inside score_Text
  } else if (userScore > 1) {
    // if user scored more than 1
    let scoreTag =
      "<span>and nice , You got <p>" +
      userScore +
      "</p> out of <p>" +
      questions.length +
      "</p></span>";
    scoreText.innerHTML = scoreTag;
  } else {
    // if user scored less than 1
    let scoreTag =
      "<span>and sorry , You got only <p>" +
      userScore +
      "</p> out of <p>" +
      questions.length +
      "</p></span>";
    scoreText.innerHTML = scoreTag;
  }
}
```


- The following functions, `startTimer`, `startTimerLine`, and `queCounter` are used to control the timer and actions associated with it. The `startTimer` function is used to start the timer, the `startTimerLine` function is used to show a progress bar mirroring the timer value left, and the `queCounter` function is used to create a new span tag and pass the question number and total question.
```js
// control the timer and actions associated to it
function startTimer(time) {
  counter = setInterval(timer, 1000);
  function timer() {
    timeCount.textContent = time; //change the value of timeCount with time value
    time--; //decrement the time value
    if (time < 9) {
      //if timer is less than 9
      let addZero = timeCount.textContent;
      timeCount.textContent = "0" + addZero; //add a 0 before time value
    }
    if (time < 0) {
      //if timer is less than 0
      clearInterval(counter); //clear counter
      timeText.textContent = "Time Off"; //change the time text to time off
      const allOptions = option_list.children.length; //get all option items
      let correcAns = questions[que_count].answer; //get correct answer from array
      for (i = 0; i < allOptions; i++) {
        if (option_list.children[i].textContent == correcAns) {
          //if there is an option which is matched to an array answer
          option_list.children[i].setAttribute("class", "option correct"); //add green color to matched option
          option_list.children[i].insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to matched option
          console.log("Time Off: Auto selected correct answer.");
        }
      }
      for (i = 0; i < allOptions; i++) {
        option_list.children[i].classList.add("disabled"); //once user select an option then disabled all options
      }
      next_btn.classList.add("show"); //show the next button if user selected any option
    }
  }
}

// Shows a progress bar mirroring timer value left
function startTimerLine(time) {
  counterLine = setInterval(timer, 29);
  function timer() {
    time += 1; //upgrading time value with 1
    time_line.style.width = time + "px"; //increasing width of time_line with px by time value
    if (time > 549) {
      //if time value is greater than 549
      clearInterval(counterLine); //clear counterLine
    }
  }
}

function queCounter(index) {
  //creating a new span tag and passing the question number and total question
  let totalQueCounTag =
    "<span><p>" +
    index +
    "</p> of <p>" +
    questions.length +
    "</p> Questions</span>";
  bottom_ques_counter.innerHTML = totalQueCounTag; //adding new span tag inside bottom_ques_counter
}
```