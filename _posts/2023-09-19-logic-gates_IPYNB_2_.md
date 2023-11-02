---
layout: post
title: Logic Gates
description: Lesson on boolean expressions and if statements!
comments: True
courses: {'csa': {'week': 1}}
type: hacks
---

# Logic Gates

Logic gates are the fundamental building blocks of digital circuits, and are critical to the functioning of basic computer functions. They are responsible for processing binary data in a computer by performing Boolean logic operations such as AND, OR, NOT, and XOR. By combining multiple logic gates, complex digital circuits can be created that can perform a wide range of operations, from basic arithmetic to complex decision-making processes.

### AND
Boolean multiplication corresponds to the logical function of an “AND” gate, as well as to series switch contacts:

![]({{ site.baseurl }}/images/and.png)

### OR
Boolean addition corresponds to the logical function of an “OR” gate, as well as to parallel switch contacts:

![]({{ site.baseurl }}/images/or.png)


### NOT
Boolean complementation finds equivalency in the form of the NOT gate, or a normally-closed switch or relay contact:

![]({{ site.baseurl }}/images/nor.png)

## Half-Adder Circuit
A half-adder circuit is used to add two bits of data together and is based on the following Truth Table.


<table width="50%">
    <col style="width:25%">
	<col style="width:25%">
    <col style="width:25%">
	<col style="width:25%">
  <tr>
    <th>A</th>
    <th>B</th>
    <th>Sum</th>
    <th>Carry</th>
  </tr>
  <tr>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
  </tr>
  <tr>
    <td>0</td>
    <td><html>
<head>
	<style>
        input {font-size: 18px}
        p {font-size: 18px}
	</style>
</head>
<body>
	<input type="text" id="input-box" size="4">
	<button onclick="checkInput()">Check</button>
	<div id="correct">
    <p>Correct!</p>
    </div>
	<script>
    document.getElementById("correct").style.display = "none";
		function checkInput() {
			var inputValue = document.getElementById("input-box").value;
			if (inputValue === "1") {
				document.getElementById("correct").style.display = "block";
			} else {
				document.getElementById("correct").style.display = "none";
			}
		}
	</script>
</body>
</html></td>
    <td>1</td>
    <td>0</td>
  </tr>
  <tr>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td><html>
<head>
	<style>
        input {font-size: 18px}
        p {font-size: 18px}
	</style>
</head>
<body>
	<input type="text" id="input-box1" size="4">
	<button onclick="checkInput1()">Check</button>
	<div id="correct1">
    <p>Correct!</p>
    </div>
	<script>
    document.getElementById("correct1").style.display = "none";
		function checkInput1() {
			var inputValue1 = document.getElementById("input-box1").value;
			if (inputValue1 === "1") {
				document.getElementById("correct1").style.display = "block";
			} else {
				document.getElementById("correct1").style.display = "none";
			}
		}
	</script>
</body>
</html></td>
  </tr>
</table>

A half-adder circuit consists of two logic gates as follows:

![]({{ site.baseurl }}/images/Half-Adder.png)

## Full-Adder Circuit
A full-adder circuit is used to add three bits of data together and is based on the following Truth Table.

<table width="50%">
    <col style="width:20%">
	<col style="width:20%">
    <col style="width:20%">
	<col style="width:20%">
    <col style="width:20%">
  <tr>
    <th>A</th>
    <th>B</th>
    <th>C in</th>
    <th>Sum</th>
    <th>Cout</th>
  </tr>
  <tr>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
    <td>0</td>
  </tr>
  <tr>
    <td>1</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
  </tr>
  <tr>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
  </tr>
  <tr>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td><html>
<head>
	<style>
        input {font-size: 18px}
        p {font-size: 18px}
	</style>
</head>
<body>
	<input type="text" id="input-box2" size="4">
	<button onclick="checkInput2()">Check</button>
	<div id="correct2">
    <p>Correct!</p>
    </div>
	<script>
    document.getElementById("correct2").style.display = "none";
		function checkInput2() {
			var inputValue2 = document.getElementById("input-box2").value;
			if (inputValue2 === "0") {
				document.getElementById("correct2").style.display = "block";
			} else {
				document.getElementById("correct2").style.display = "none";
			}
		}
	</script>
</body>
</html></td>
    <td>1</td>
  </tr>
  <tr>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
  </tr>
  <tr>
    <td>1</td>
    <td>0</td>
    <td><html>
<head>
	<style>
        input {font-size: 18px}
        p {font-size: 18px}
	</style>
</head>
<body>
	<input type="text" id="input-box3" size="4">
	<button onclick="checkInput3()">Check</button>
	<div id="correct3">
    <p>Correct!</p>
    </div>
	<script>
    document.getElementById("correct3").style.display = "none";
		function checkInput3() {
			var inputValue3 = document.getElementById("input-box3").value;
			if (inputValue3 === "1") {
				document.getElementById("correct3").style.display = "block";
			} else {
				document.getElementById("correct3").style.display = "none";
			}
		}
	</script>
</body>
</html></td>
    <td>0</td>
    <td>1</td>
  </tr>
  <tr>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>0</td>
    <td>1</td>
  </tr>
  <tr>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td>1</td>
    <td><html>
<head>
	<style>
        input {font-size: 18px}
        p {font-size: 18px}
	</style>
</head>
<body>
	<input type="text" id="input-box4" size="4">
	<button onclick="checkInput4()">Check</button>
	<div id="correct4">
    <p>Correct!</p>
    </div>
	<script>
    document.getElementById("correct4").style.display = "none";
		function checkInput4() {
			var inputValue4 = document.getElementById("input-box4").value;
			if (inputValue4 === "1") {
				document.getElementById("correct4").style.display = "block";
			} else {
				document.getElementById("correct4").style.display = "none";
			}
		}
	</script>
</body>
</html></td>
  </tr>
</table>

A full-adder circuit consists of two half-adder circuits and an OR gate connected as follows:

![]({{ site.baseurl }}/images/Full-Adder.png)

# Hacks
Answer these questions in your blog:

1. How can logic gates be used to execute basic computer functions?(1-2 sentences)

2. What is the difference between boolean operations and logic gates?(1-2 sentences)

3. Go to this link and complete the following game. Take a screenshot of when you've completed it. Talk about how each logic gate works with one another.
