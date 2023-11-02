---
toc: True
layout: default
title: About Me
type: hacks
courses: {'csa': {'week': 0}}

---

<style>
  @font-face {
  font-family: "Supreme V1";
  src: url("https://db.onlinewebfonts.com/t/f462af0a8168d0a315da1c8d3fcf419b.eot");
  src: url("https://db.onlinewebfonts.com/t/f462af0a8168d0a315da1c8d3fcf419b.eot?#iefix")format("embedded-opentype"),
  url("https://db.onlinewebfonts.com/t/f462af0a8168d0a315da1c8d3fcf419b.woff2")format("woff2"),
  url("https://db.onlinewebfonts.com/t/f462af0a8168d0a315da1c8d3fcf419b.woff")format("woff"),
  url("https://db.onlinewebfonts.com/t/f462af0a8168d0a315da1c8d3fcf419b.ttf")format("truetype"),
  url("https://db.onlinewebfonts.com/t/f462af0a8168d0a315da1c8d3fcf419b.svg#Supreme V1")format("svg");
}
  body {
      font-family: Arial, sans-serif;
      line-height: 1.6;
      background-color: white;
  }

  h1 {
      color: black;
  }
  .custom-font {
      font-family: "Supreme V1";
      color: black;
  }
  table {
    border-collapse: collapse;
    width: 100%;
    border: 1px solid black;
  }
  th, td {
      padding: 8px;
      text-align: left;
      border-bottom: 1px solid black;
  }
  th {
      background-color: white;
  }
  p {
    font-size: 11px;
    color: black;
  }
  body {
      font-family: Arial, sans-serif;
      line-height: 1.6;
      background-color: white;
  }

  h1 {
      font-size: 24px;
      color: black;
  }
  .custom-font {
      font-family: "Supreme V1";
      color: black;
  }
  	#calculator {
    margin: 0 auto;
    padding: 20px;
  }

  #result {
    width: 100%;
    margin-bottom: 10px;
    padding: 5px;
    font-size: 20px;
    border: 2px solid #000;
    border-radius: 2px;
  }

  button {
    width: 50px;
    height: 50px;
    font-size: 20px;
    border: 2px solid #000;
    border-radius: 5px;
    margin: 5px;
    cursor: pointer;
    background-color: #f0f0f0;
  }

  button:hover {
    background-color: #d0d0d0;
  }
  .alt {
    background-color: rgb(44, 45, 48);
    color: white;
  }

  .revert {
    background-color: white;
    color: black;
  }
</style>

<h1 class="custom-font" font-size="25px">Ethan Tran's Website</h1>

<button class="alt" onClick="altTheme()">Alt</button>
<button class="revert" onClick="revertColor()">OG</button>

<script>
    function altTheme() {
        document.body.style.backgroundColor =  "rgb(44, 45, 48)";
        document.querySelectorAll(".custom-font").forEach(element => {
            element.style.color = "white"; 
         document.querySelectorAll(".h1").forEach(element => {
            element.style.color = "rgb(247, 247, 247)"; 
            });
        });
    }
    function revertColor() {
        document.body.style.backgroundColor = "white";
        document.querySelectorAll(".custom-font").forEach(element => {
        element.style.color = "black"; 

    });
    }
</script>

### My Freeform Drawing

<p>I can't wait to code, code, code!</p>

<img src="https://github.com/nighthawkcoders/student/assets/109186517/3a8cec44-415a-4821-8c2d-88bea49f75c6" height="275px">
<img src="https://github.com/rachit-j/Rackets-Blog/assets/109186517/0936df9f-efa9-4a72-b37e-ca09fa3a41b1" height ="275px">
<img src="https://github.com/realethantran/ethan_student/assets/109186517/b1ad8fc5-6588-47f5-9e4e-c4e0653ddcb5" height="275px">
<head>
</head>
<body>
    <table>
        <thead>
            <tr>
                <th>Period</th>
                <th>Class</th>
                <th>Teacher</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>AP Computer Science A</td>
                <td>Mr. Mortensen</td>
            </tr>
            <tr>
                <td>2</td>
                <td>AP English Language</td>
                <td>Mrs. Jenkins</td>
            </tr>
            <tr>
                <td>3</td>
                <td>AP U.S. History</td>
                <td>Mr. Swanson</td>
                </tr>
                       <tr>
                <td>4</td>
                <td>AP Calculus AB</td>
                <td>Mr. Froom</td>
            </tr>

<div></div>
  <h1 class="custom-font">Basic Calculator</h1>
  <div id="calculator">
    <input type="text" id="result" readonly>
    <br>
    <button onclick="addToResult('1')">1</button>
    <button onclick="addToResult('2')">2</button>
    <button onclick="addToResult('3')">3</button>
    <button onclick="addToResult('+')">+</button>
    <br>
    <button onclick="addToResult('4')">4</button>
    <button onclick="addToResult('5')">5</button>
    <button onclick="addToResult('6')">6</button>
    <button onclick="addToResult('-')">-</button>
    <br>
    <button onclick="addToResult('7')">7</button>
    <button onclick="addToResult('8')">8</button>
    <button onclick="addToResult('9')">9</button>
    <button onclick="addToResult('*')">*</button>
    <br>
    <button onclick="addToResult('0')">0</button>
    <button onclick="calculate()">=</button>
    <button onclick="clearResult()">A/C</button>
    <button onclick="addToResult('/')">/</button>
  </div>
  
  <script>
    function addToResult(value) {
      document.getElementById('result').value += value;
    }

    function clearResult() {
      document.getElementById('result').value = '';
    }

    function calculate() {
      try {
        const resultField = document.getElementById('result');
        const expression = resultField.value;
        const calculatedValue = eval(expression);
        resultField.value = calculatedValue;
      } catch (error) {
        resultField.value = 'Error';
      }
    }
  </script>