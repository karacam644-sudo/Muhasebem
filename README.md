# Muhasebem
index.html
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Muhasebe</title>
<style>
body { font-family: Arial; background:#f4f4f4; margin:10px; }
h2 { text-align:center; }
.card { background:white; padding:10px; margin:10px 0; border-radius:8px; }
input, button { width:100%; padding:8px; margin-top:5px; }
button { background:#1565c0; color:white; border:none; border-radius:5px; }
</style>
</head>
<body>

<h2>📒 Muhasebe</h2>

<div class="card">
<h3>Çalışan Ekle</h3>
<input id="name" placeholder="Ad Soyad">
<input id="salary" type="number" placeholder="Aylık Maaş (TL)">
<button onclick="addEmployee()">Ekle</button>
</div>

<div id="list"></div>

<script>
let employees = JSON.parse(localStorage.getItem("employees") || "[]");

function save() {
  localStorage.setItem("employees", JSON.stringify(employees));
  render();
}

function addEmployee() {
  if(!name.value || !salary.value) return alert("Bilgileri gir");
  employees.push({
    name: name.value,
    salary: Number(salary.value),
    advances: []
  });
  name.value = salary.value = "";
  save();
}

function addAdvance(i) {
  let amt = prompt("Avans (TL)");
  if (!amt) return;
  employees[i].advances.push(Number(amt));
  save();
}

function render() {
  list.innerHTML = "";
  employees.forEach((e,i)=>{
    let adv = e.advances.reduce((a,b)=>a+b,0);
    list.innerHTML += `
    <div class="card">
      <b>${e.name}</b><br>
      Maaş: ${e.salary} ₺<br>
      Avans: ${adv} ₺<br>
      <b>Net: ${e.salary - adv} ₺</b><br><br>
      <button onclick="addAdvance(${i})">Günlük Avans Ekle</button>
    </div>`;
  });
}
render();
</script>

</body>
</html>
