---
comments: false
layout: post
title: Calculator
description: Calculator for Basic Math
type: ccc
courses: { csse: { week: 4 } }
---

<style>
  .calculator-output {
    /* calulator output 
      top bar shows the results of the calculator;
      result to take up the entirety of the first row;
      span defines 4 columns and 1 row
    */
    grid-column: span 4;
    grid-row: span 1;
    border-style: solid;
    border-width: 1px;
    border-color: currentColor;

  
    padding: 0.25em;
    font-size: 20px;
  
    display: flex;
    align-items: center;
  }
</style>

<!-- Add a container for the animation -->
<div id="animation">
  <div class="calculator-container grid">
      <!--result-->
      <div class="calculator-output" id="output">0</div>
      <!--row 1-->
      <div class="calculator-number btn btn-outline">1</div>
      <div class="calculator-number btn btn-outline">2</div>
      <div class="calculator-number btn btn-outline">3</div>
      <div class="calculator-operation btn btn-outline btn-accent">+</div>
      <!--row 2-->
      <div class="calculator-number btn btn-outline">4</div>
      <div class="calculator-number btn btn-outline">5</div>
      <div class="calculator-number btn btn-outline">6</div>
      <div class="calculator-operation btn btn-outline btn-accent">-</div>
      <!--row 3-->
      <div class="calculator-number btn btn-outline">7</div>
      <div class="calculator-number btn btn-outline">8</div>
      <div class="calculator-number btn btn-outline">9</div>
      <div class="calculator-operation btn btn-outline btn-accent">*</div>
      <!--row 4-->
      <div class="calculator-clear btn btn-primary">A/C</div>
      <div class="calculator-number btn btn-outline">0</div>
      <div class="calculator-number btn btn-outline">.</div>
      <div class="calculator-operation btn btn-outline btn-accent">/</div>
      <!--row 5-->
      <div class="calculator-operation btn btn-outline btn-accent">√</div>
      <div class="calculator-operation btn btn-outline btn-accent">^</div>
      <div></div>      
      <div class="calculator-equals btn btn-primary">=</div>
  </div>
</div>

<!-- JavaScript (JS) implementation of the calculator. -->
<script>
  // initialize important variables to manage calculations
  var firstNumber = null;
  var operator = null;
  var nextReady = true;
  // build objects containing key elements
  const output = document.getElementById("output");
  const numbers = document.querySelectorAll(".calculator-number");
  const operations = document.querySelectorAll(".calculator-operation");
  const clear = document.querySelectorAll(".calculator-clear");
  const equals = document.querySelectorAll(".calculator-equals");

  // Number buttons listener
  numbers.forEach(button => {
    button.addEventListener("click", function() {
      number(button.textContent);
    });
  });

  // Number action
  function number (value) { // function to input numbers into the calculator
      if (value != ".") {
          if (nextReady == true) { // nextReady is used to tell the computer when the user is going to input a completely new number
              output.innerHTML = value;
              // first number
              if (value != "0") { // if statement to ensure that there are no multiple leading zeroes
                  nextReady = false;
              }
          } else {
              // second number
              output.innerHTML = output.innerHTML + value; // concatenation is used to add the numbers to the end of the input
          }
      } else { // special case for adding a decimal; can not have two decimals
          if (output.innerHTML.indexOf(".") == -1) {
              output.innerHTML = output.innerHTML + value;
              nextReady = false;
          }
      }
  }

  // Operation buttons listener
  operations.forEach(button => {
    button.addEventListener("click", function() {
      operation(button.textContent);
    });
  });

  // Operator action
  function operation (choice) { // function to input operations into the calculator
      if (firstNumber == null) { // once the operation is chosen, the displayed number is stored into the variable firstNumber
          firstNumber = parseFloat(output.innerHTML);
          nextReady = true;
          operator = choice;
          return; // exits function
      }
      if (nextReady == false) {
        equal()
      }
      // occurs if there is already a number stored in the calculator
      operator = choice;
      output.innerHTML = firstNumber.toString();
      nextReady = true;
  }

  // Calculator
  function calculate (first, second) { // function to calculate the result of the equation
      let result = 0;
      switch (operator) {
          case "+":
              result = first + second;
              break;
          case "-":
              result = first - second;
              break;
          case "*":
              result = first * second;
              break;
          case "/":
              result = first / second;
              break;
          case "√":
            result = Math.pow(first, 1/second);
            break;
          case "^":
            result = Math.pow(first, second);
            break;
          case null:
            return first
            break;
          default: 
              break;
      }
      return result;
  }

  // Equals button listener
  equals.forEach(button => {
    button.addEventListener("click", function() {
      equal();
    });
  });

  // Equal action
  function equal () { // function used when the equals button is clicked; calculates equation and displays it
      firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
      output.innerHTML = firstNumber.toString();
      operator = null;
      nextReady = true;
  }

  // Clear button listener
  clear.forEach(button => {
    button.addEventListener("click", function() {
      clearCalc();
    });
  });

  // A/C action
  function clearCalc () { // clears calculator
      firstNumber = null;
      output.innerHTML = "0";
      nextReady = true;
  }

  const eventMap = {
    "1": 1,
    "2": 2,
    "3": 3,
    "4": 4,
    "5": 5,
    "6": 6,
    "7": 7,
    "8": 8,
    "9": 9,
    "0": 0,
    ".": ".",
    "+": "+",
    "-": "-",
    "*": "*",
    "/": "/",
    "^": "^",
    "c": "clear",
    "Enter": "=",
  };

  window.addEventListener("keypress", (event) => {
    const key = eventMap[event.key];
    if (key === undefined) {
      return;
    }

    if (key === "clear") {
      clearCalc();
      return;
    }

    if (key === "=") {
      equal();
      return; 
    }

    if (["+", "-", "*", "/", "^"].includes(key)) {
      operation(key);
      return; 
    }

    number(key)
  })

</script>