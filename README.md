# business-loan-calculator
Сайт-калькулятор для розрахунку бізнес-кредиту. Дозволяє визначити щомісячний платіж, загальну переплату, а також переглянути графік погашення кредиту.
/project
  index.html
  calculator.html
  about.html
  contacts.html
  style.css
  <!-- Сайт розроблено студентом Марією Уманською, група ФЕМП 4-14 -->
<!DOCTYPE html>
<html lang="uk">
<head>
<meta charset="UTF-8">
<title>Business Loan Calculator</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<header>
<h1>Business Loan Calculator</h1>
<nav>
<a href="index.html">Головна</a>
<a href="calculator.html">Калькулятор</a>
<a href="about.html">Про проєкт</a>
<a href="contacts.html">Контакти</a>
</nav>
</header>

<main class="container">
<div class="card">
<h2>Ласкаво просимо</h2>
<p>Сайт допоможе розрахувати бізнес-кредит, щомісячні платежі та переплату.</p>
<p>Використовуйте калькулятор для фінансового планування.</p>
</div>
</main>

<footer>
<p>Уманська Марія | ФЕМП 4-14</p>
</footer>

</body>
</html>
<!-- Сайт розроблено студентом Марією Уманською, група ФЕМП 4-14 -->
<!DOCTYPE html>
<html lang="uk">
<head>
<meta charset="UTF-8">
<title>Калькулятор</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<header>
<h1>Калькулятор кредиту</h1>
<nav>
<a href="index.html">Головна</a>
<a href="calculator.html">Калькулятор</a>
<a href="about.html">Про проєкт</a>
<a href="contacts.html">Контакти</a>
</nav>
</header>

<main class="container">

<div class="card">
<h2>Розрахунок</h2>

<input type="number" id="amount" placeholder="Сума (грн)">
<input type="number" id="months" placeholder="Термін (місяці)">
<input type="number" id="rate" placeholder="Ставка (%)">

<button onclick="calculate()">Розрахувати</button>

<h3 id="result"></h3>
</div>

<div class="card">
<h2>Графік платежів</h2>
<table id="table">
<tr>
<th>Місяць</th>
<th>Платіж</th>
<th>Залишок</th>
</tr>
</table>
</div>

<div class="card">
<h2>Графік</h2>
<canvas id="chart" height="200"></canvas>
</div>

</main>

<footer>
<p>Уманська Марія | ФЕМП 4-14</p>
</footer>

<script>
function calculate() {
let amount = +document.getElementById("amount").value;
let months = +document.getElementById("months").value;
let rate = +document.getElementById("rate").value / 100 / 12;

if (!amount || !months || !rate) {
document.getElementById("result").innerText = "Введіть всі дані!";
return;
}

let payment = (amount * rate) / (1 - Math.pow(1 + rate, -months));
let total = payment * months;
let overpay = total - amount;

document.getElementById("result").innerHTML =
"Щомісячний платіж: " + payment.toFixed(2) + " грн<br>" +
"Переплата: " + overpay.toFixed(2) + " грн";

// таблиця
let table = document.getElementById("table");
table.innerHTML = "<tr><th>Місяць</th><th>Платіж</th><th>Залишок</th></tr>";

let balance = amount;
let data = [];

for (let i = 1; i <= months; i++) {
let interest = balance * rate;
let principal = payment - interest;
balance -= principal;

table.innerHTML += `
<tr>
<td>${i}</td>
<td>${payment.toFixed(2)}</td>
<td>${Math.abs(balance).toFixed(2)}</td>
</tr>`;

data.push(balance);
}

drawChart(data);
}

function drawChart(data) {
let canvas = document.getElementById("chart");
let ctx = canvas.getContext("2d");

ctx.clearRect(0, 0, canvas.width, canvas.height);

let max = Math.max(...data);
let stepX = canvas.width / data.length;

ctx.beginPath();

data.forEach((v, i) => {
let x = i * stepX;
let y = canvas.height - (v / max * canvas.height);

if (i === 0) ctx.moveTo(x, y);
else ctx.lineTo(x, y);
});

ctx.strokeStyle = "#26a69a";
ctx.lineWidth = 2;
ctx.stroke();
}
</script>

</body>
</html>
<!-- Сайт розроблено студентом Марією Уманською, група ФЕМП 4-14 -->
<!DOCTYPE html>
<html lang="uk">
<head>
<meta charset="UTF-8">
<title>Про проєкт</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<header>
<h1>Про проєкт</h1>
<nav>
<a href="index.html">Головна</a>
<a href="calculator.html">Калькулятор</a>
<a href="about.html">Про проєкт</a>
<a href="contacts.html">Контакти</a>
</nav>
</header>

<main class="container">
<div class="card">
<p>Це веб-застосунок для розрахунку бізнес-кредитів.</p>
<p>Реалізований на HTML, CSS та JavaScript без серверу.</p>
</div>
</main>

<footer>
<p>Уманська Марія | ФЕМП 4-14</p>
</footer>

</body>
</html>
<!-- Сайт розроблено студентом Марією Уманською, група ФЕМП 4-14 -->
<!DOCTYPE html>
<html lang="uk">
<head>
<meta charset="UTF-8">
<title>Контакти</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<header>
<h1>Контакти</h1>
<nav>
<a href="index.html">Головна</a>
<a href="calculator.html">Калькулятор</a>
<a href="about.html">Про проєкт</a>
<a href="contacts.html">Контакти</a>
</nav>
</header>

<main class="container">
<div class="card">
<p>Email: business-loan-calculator@gmail.com</p>
<p>Телефон: +380123456789</p>
</div>
</main>

<footer>
<p>Уманська Марія | ФЕМП 4-14</p>
</footer>

</body>
</html>
body {
margin: 0;
font-family: Arial;
background: linear-gradient(135deg, #e0f7fa, #e8f5e9);
}

header {
background: linear-gradient(90deg, #009688, #26a69a);
color: green;
padding: 15px;
text-align: center;
}

nav a {
color: green;
margin: 10px;
text-decoration: none;
font-weight: bold;
}

.container {
padding: 20px;
display: grid;
gap: 20px;
}

.card {
background: white;
padding: 20px;
border-radius: 15px;
box-shadow: 0 5px 15px rgba(0,0,0,0.1);
border-left: 5px solid #26a69a;
}

input {
width: 100%;
padding: 10px;
margin: 10px 0;
border-radius: 8px;
border: 1px solid #ccc;
}

button {
width: 100%;
padding: 10px;
background: linear-gradient(90deg, #43a047, #26a69a);
color: green;
border: none;
cursor: pointer;
}

table {
width: 100%;
border-collapse: collapse;
}

td, th {
border: 1px solid #ddd;
padding: 8px;
text-align: center;
}

th {
background: #26a69a;
color: green;
}

footer {
background: #004d40;
color: green;
text-align: center;
padding: 10px;
margin-top: 20px;
}
