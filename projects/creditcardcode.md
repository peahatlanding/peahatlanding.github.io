---
layout: projects
comments: false
title:  "Credit Card Validator"
anchor: #creditcard
---


# Credit Card Validator

Here's the code I wrote for the Credit Card Validator. [You can try the validator here](/projects/creditcard.html).

Our final assignment for a Javascript course was to code this validator which made sure the input passed a number of rules.
Once the course was over, I took it home and added an HTML interface and a bunch of reaction images. This was pretty fun!

```
<html>
<head>
  <meta charset="utf-8" />
  <title>Credit Card Validator</title>
  <!-- Bootstrap core CSS -->
   <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
   <!-- Custom styles for this template -->
   <link href="val.css" rel="stylesheet">

   <!--fonts-->
   <link href="https://fonts.googleapis.com/css?family=Bungee+Shade|Fascinate|Shrikhand" rel="stylesheet">
</head>
<body>
  <div class="container">
    <div class="row">
      <div class="panel">
        <div class="panel-body">
          <div class="panel-heading">
          </div>

          <div class="panel val col-md-6"><!-- Val's panel-->
            <div class="panel-body">
              <div class="panel-heading">
                <h1>Credit Card Validator</h1>
                <img src="/images/neutral.png" id="reaction">
              </div><!--end Val's heading-->
              <img src="/images/tail.png">
              <div class="panel speech-bubble">
                <div class="panel-body">
                <p>
                  <span id="response">Hi, I'm a Credit Card Validator! Enter a credit card number that follows the rules to my right!</span>
                </p>
              </div>
              </div><!--end speech bubble-->
              <p>Enter your number: <input type="text" id="number"></p>
              <button id="validate-button">Validate!</button>
            </div><!--end Val's panel-body-->
          </div><!--end Val's panel-->
          <div class="panel col-md-6"><!--rules panel-->
            <div class="panel-body">
              <h2>Rules</h2>
              <p>Your credit card must follow these rules to pass validation:</p>
              <ul>
                <li>Must be 16 digits!.</li>
                <li>Must be all numbers.</li>
                <li>Must have at least two different digits.</li>
                <li>Final digit must be even.</li>
                <li>The sum of all the digits must be greater than 16.</li>
                <li>DO NOT enter real credit card numbers! You can try the ones below.</li>
              </ul>
              <p>If you want, use these numbers to test the validator:</p>
              <h3>Pass</h3>
              <ul>
                <li>6111-6222-6333-1444</li>
                <li>1111-2222-3333-4444</li>
              </ul>
              <h3>Fail</h3>
              <ul>
                <li>1111-1111-1111-1110</li>
                <li>6111-6222-6333-14446111-6222-6333-1444</li>
                <li>a923-3211-9c01-1112</li>
                <li>4444-4444-4444-4444</li>
              </ul>
            </div><!--end rules body-->
          </div><!--end rules-->
        </div> <!-- end panel body -->
      </div> <!-- end panel -->
    </div> <!-- end row -->
  </div><!-- end container -->


</body>
</html>
<script>
var button = document.getElementById("validate-button");

//Removes any hyphens and turns the string into an array
function arrayify (creditCardString){
  creditCardString = creditCardString.split("-").join("");
  var creditCardArray = [];
  for (i=0; i<creditCardString.length; i++) {
    var digit = parseInt(creditCardString[i]);
    creditCardArray.push(digit);
  }
  return creditCardArray;
}
//Checks the type of each item in creditCardArray and returns false if they're not all numbers.
function checkTypeOf (creditCardArray){
  for (i=0; i<creditCardArray.length; i++) {
    var flag = typeof 4;
    if (isNaN(creditCardArray[i]) || typeof creditCardArray[i] != flag){
      console.log("Failed checkTypeOf");
      return false;
    }
    else{
    }
  }
}

//Checks length and returns false if it's not 16.
function checkLength (creditCardArray){
  var creditCardLength = creditCardArray.length;
  if (creditCardLength == 16) {
  }
  else {
    return false;
  }
}

//Checks to see if there are at least two different numbers in creditCardArray. If not, returns false.
function checkTwoDiff (creditCardArray){
  var diffFlag= false;
  for (i=0; i<creditCardArray.length; i++){
      if (creditCardArray[i] != creditCardArray[0]) {
        diffFlag = true;
      }
      else {
      }
  }
  if (diffFlag === false) {
    return false;
  }
  else {
  }
}

//Checks if the final digit is evenly divisible by 2. If not, returns false.
function checkLastDigit (creditCardArray){
  if (creditCardArray[creditCardArray.length-1] % 2 !== 0) {
    return false;
  }
  else {

  }
}

//Adds all the digits. If the sum is less than 16, returns false.
function checkSum (creditCardArray){
  var sumAllDigits = 1;

  for (i=0; i<creditCardArray.length; i++){
    var sumAllDigits = sumAllDigits + creditCardArray[i];
  }
  if (sumAllDigits <= 16) {
    return false;
  }
  else {
  }
}

//init fail counters
var checkTypeOfCounter = 0;
var checkLengthCounter = 0;
var checkTwoDiffCounter = 0;
var checkLastDigitCounter = 0;
var checkSumCounter = 0;
var failureCounter = 0;
var successCounter = 0;


//Takes the creditCardString and calls all the other functions to see if it passes all the rules.
function validateCreditCard(creditCardString){
  //arrayify their creditCardString
  var creditCardString = document.getElementById("number").value;
  var creditCardArray = arrayify(document.getElementById("number").value);


  //FIRST CHECK: Number must be 16 digits, all of them must be numbers
  if (checkTypeOf(creditCardArray) == false) {
    checkTypeOfCounter += 1;
    console.log("checkTypeOf: " + checkTypeOfCounter);

    //if statement that figures out what response to give.
    if (checkLengthCounter == 1) {
      document.getElementById("response").innerHTML = "Oops! You've got a letter in there. It needs to be all numbers.";
      document.getElementById("reaction").src = "/images/oops.png"
    }
    else if (checkLengthCounter == 2) {
      document.getElementById("response").innerHTML = "It needs to be all numbers, remember??";
      document.getElementById("reaction").src = "/images/oops.png"
    }
    else if (checkLengthCounter == 3) {
      document.getElementById("response").innerHTML = "....";
      document.getElementById("reaction").src = "/images/really1.png"
    }
    else if (checkLengthCounter == 4){
      document.getElementById("response").innerHTML = "Numbers! I'm a credit card NUMBER validator! Numbers only!!";
      document.getElementById("reaction").src = "/images/angry1.png"
    }
    else {
      document.getElementById("response").innerHTML = "You have made this mistake " + checkLengthCounter + " times now!! PLEASE!!!!";
      document.getElementById("reaction").src = "/images/angry2.png"
    }
    //+1 if the # of digits is wrong
    failureCounter += 1;
  }

  else if (checkLength(creditCardArray) == false) {
    checkLengthCounter += 1;
    console.log("checkLengthCounter: " + checkLengthCounter);

    //if statement that figures out what response to give.
    if (checkLengthCounter == 0) {
      document.getElementById("response").innerHTML = "OOPZ! It needs to be 16 digits.";
      document.getElementById("reaction").src = "/images/oops.png"
    }
    else if (checkLengthCounter == 1) {
      document.getElementById("response").innerHTML = "OOPZ! It needs to be 16 digits.";
      document.getElementById("reaction").src = "/images/oops.png"
    }
    else if (checkLengthCounter == 2) {
      document.getElementById("response").innerHTML = "It needs to be 16 digits, remember??";
      document.getElementById("reaction").src = "/images/really2.png"
    }
    else if (checkLengthCounter == 3) {
      document.getElementById("response").innerHTML = "....";
      document.getElementById("reaction").src = "/images/really1.png"
    }
    else if (checkLengthCounter == 4){
      document.getElementById("response").innerHTML = "16 digits! SIXTEEN! Try again and get it right!";
      document.getElementById("reaction").src = "/images/angry1.png"
    }
    else {
      document.getElementById("response").innerHTML = "You have made this mistake " + checkLengthCounter + " times now!! PLEASE!!!!";
      document.getElementById("reaction").src = "/images/angry2.png"
    }
    //+1 if the # of digits is wrong
    failureCounter += 1;

  }

  //SECOND CHECK: Sum of digits must be greater than 16
  else if (checkTwoDiff(creditCardArray) == false) {
    checkTwoDiffCounter += 1;
    console.log("checkTwoDiffCounter: " + checkTwoDiffCounter);

    //if statement that figures out checktwoDiff error message to give.
    if (checkTwoDiffCounter == 1) {
      document.getElementById("response").innerHTML = "Oops! Your credit card number can't be all the same number.";
      document.getElementById("reaction").src = "/images/oops.png"
    }
    else if (checkTwoDiffCounter == 2) {
      document.getElementById("response").innerHTML = "Oops! It needs at least two numbers.";
      document.getElementById("reaction").src = "/images/oops.png"
    }
    else if (checkTwoDiffCounter == 3) {
      document.getElementById("response").innerHTML = "....";
      document.getElementById("reaction").src = "/images/really1.png"
    }
    else {
      document.getElementById("response").innerHTML = "Wrong!!! It needs at least two types of numbers.";
      document.getElementById("reaction").src = "/images/really3.png"
    }
    //+1 if it's all the same number
    failureCounter += 1;

  }//end of SECOND CHECK

  //THIRD CHECK: The final digit must be even.
  else if (checkLastDigit(creditCardArray) == false) {
    checkLastDigitCounter += 1;
    console.log("checkLastDigitCounter: " + checkLastDigit);

    //if statement that figures out checktwoDiff error message to give.
    if (checkLastDigitCounter == 1) {
      document.getElementById("response").innerHTML = "Oops! The last digit needs to be an even number.";
      document.getElementById("reaction").src = "/images/oops.png"
    }
    else if (checkLastDigitCounter == 2) {
      document.getElementById("response").innerHTML = "Oops! The last digit needs to be an even number, remember?";
      document.getElementById("reaction").src = "/images/oops.png"
    }
    else if (checkLastDigitCounter == 3) {
      document.getElementById("response").innerHTML = "....";
      document.getElementById("reaction").src = "/images/really1.png"
    }
    else {
      document.getElementById("response").innerHTML = "StOP!! The last digit needs to be an even number. You faker.";
      document.getElementById("reaction").src = "/images/really3.png"
    }
    //+1 if the last digit is even.
    failureCounter += 1;

  }//end of THIRD CHECK

  //FOURTH CHECK: The sum of all the digits must be greater than 16
  else if (checkSum(creditCardArray) == false) {
    checkSumCounter += 1;
    console.log("checkSumCounter: " + checkSumCounter);
    //+1 if the sum of all digits is >= 16
    failureCounter += 1;
    console.log("failure: " + failureCounter);


    //if statement that figures out checktwoDiff error message to give.
    if (checkSumCounter == 1) {
      document.getElementById("response").innerHTML = "Oops! The sum of all your digits needs to be more than 16.";
      document.getElementById("reaction").src = "/images/oops.png"
    }
    else if (checkSumCounter == 2) {
      document.getElementById("response").innerHTML = "Oops! The sum of all your digits needs to be more than 16, remember? It's one of the ways we can tell if it's a fake number.";
      document.getElementById("reaction").src = "/images/oops.png"
    }
    else if (checkSumCounter == 3) {
      document.getElementById("response").innerHTML = "....";
      document.getElementById("reaction").src = "/images/really1.png"
    }
    else {
      document.getElementById("response").innerHTML = "NO!!! The sum of all the digits needs to be more than 16. Did you just put a bunch of 1's and 0's?? Why???";
      document.getElementById("reaction").src = "/images/angry1.png"
    }
  }//end of FOURTH CHECK

  else {
    successCounter += 1;
    console.log("successCounter: " + successCounter);
    document.getElementById("response").innerHTML = "Nice credit card number!";
    if (failureCounter < 3) {
          document.getElementById("reaction").src = "/images/success.png"
    }
    else {
          document.getElementById("reaction").src = "/images/relief.png"
    }


  };

} // end of validateCreditCard function

//response variable
var response = document.getElementById("response").innerHTML;

//runs validateCreditCard when the user clicks Validate!
button.addEventListener("click", validateCreditCard);

</script>
```
