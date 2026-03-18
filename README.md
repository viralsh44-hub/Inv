<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Investment Pro</title>

<style>
body {
    font-family: Arial;
    background: #f2f4f7;
    margin: 0;
    transition: 0.3s;
}

.dark {
    background: #121212;
    color: white;
}

.container {
    max-width: 420px;
    margin: 15px auto;
    background: white;
    padding: 15px;
    border-radius: 12px;
}

.dark .container { background: #1e1e1e; }

h2 { text-align:center; }

input {
    width: 100%;
    padding: 10px;
    margin: 6px 0;
    border-radius: 6px;
    border: 1px solid #ccc;
    font-size: 16px;
}

button {
    width: 100%;
    padding: 10px;
    margin-top: 6px;
    border: none;
    border-radius: 6px;
    color: white;
    font-size: 15px;
    cursor: pointer;
}

.calc { background: #28a745; }
.clear { background: #dc3545; }
.share { background: #007bff; }
.darkbtn { background: #333; }

.result {
    background: #eee;
    padding: 10px;
    margin-top: 10px;
    border-radius: 8px;
}

.dark .result { background: #333; }

.history-box { margin-top: 10px; }

.history-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.icon-btn {
    cursor: pointer;
    font-size: 18px;
    margin-left: 10px;
}

.history {
    max-height: 150px;
    overflow-y: auto;
    margin-top: 5px;
}

.history div {
    background: #eef;
    padding: 6px;
    margin: 3px 0;
    border-radius: 5px;
}

.dark .history div { background: #444; }

.small {
    font-size: 12px;
    opacity: 0.7;
}
</style>
</head>

<body>

<div class="container">

<h2>📊 Investment Pro</h2>

<button class="darkbtn" onclick="toggleDark()">🌙 Night Mode</button>

<input type="text" id="name" placeholder="Investment Name">

<input type="tel" id="high" placeholder="High Price" oninput="format(this)">
<input type="tel" id="low" placeholder="Low Price" oninput="format(this)">

<button class="calc" onclick="calc()">Calculate</button>
<button class="clear" onclick="clearAll()">Clear</button>
<button class="share" onclick="share()">Share</button>

<div class="result">
<p>Loss: ₹ <span id="loss">0</span></p>
<p>Loss %: <span id="lossPer">0</span></p>
<p>Recovery %: <span id="rec">0</span></p>
</div>

<div class="history-box">

<div class="history-header">
<h3>History</h3>
<div>
<span class="icon-btn" onclick="exportExcel()">📥</span>
<span class="icon-btn" onclick="clearHistory()">❌</span>
</div>
</div>

<div class="history" id="history"></div>
<div class="small">* Saved automatically</div>

</div>

</div>

<script>

// LOAD
let historyData = JSON.parse(localStorage.getItem("hist")) || [];
renderHistory();

// FORMAT NUMBER
function format(input){
    let v = input.value.replace(/,/g,'');
    if(!/^\d*\.?\d*$/.test(v)){
        input.value = input.value.slice(0,-1);
        return;
    }
    let parts = v.split('.');
    input.value = Number(parts[0] || 0).toLocaleString("en-IN") + (parts[1] ? "."+parts[1] : "");
}

// CALCULATE
function calc(){
    let name = document.getElementById("name").value.trim();

    let high = parseFloat(document.getElementById("high").value.replace(/,/g,''));
    let low = parseFloat(document.getElementById("low").value.replace(/,/g,''));

    if(isNaN(high) || isNaN(low) || low > high){
        alert("Enter valid values");
        return;
    }

    let loss = high - low;
    let lossPer = (loss/high)*100;
    let rec = (loss/low)*100;

    document.getElementById("loss").innerText = loss.toFixed(2);
    document.getElementById("lossPer").innerText = lossPer.toFixed(2);
    document.getElementById("rec").innerText = rec.toFixed(2);

    let record = {
        name: name || "No Name",
        high, low, loss
    };

    historyData.unshift(record);
    localStorage.setItem("hist", JSON.stringify(historyData));

    renderHistory();
}

// RENDER HISTORY
function renderHistory(){
    let html = "";
    historyData.forEach((item, i)=>{
        html += `<div>${i+1}. ${item.name} | ₹${item.high} → ₹${item.low} | Loss ₹${item.loss.toFixed(2)}</div>`;
    });
    document.getElementById("history").innerHTML = html;
}

// CLEAR INPUT
function clearAll(){
    document.getElementById("name").value="";
    document.getElementById("high").value="";
    document.getElementById("low").value="";
    document.getElementById("loss").innerText="0";
    document.getElementById("lossPer").innerText="0";
    document.getElementById("rec").innerText="0";
}

// CLEAR HISTORY
function clearHistory(){
    if(confirm("Delete all history?")){
        historyData = [];
        localStorage.removeItem("hist");
        renderHistory();
    }
}

// DARK MODE
function toggleDark(){
    document.body.classList.toggle("dark");
}

// SHARE (FULL FIX)
function share(){
    if(historyData.length === 0){
        alert("No data to share");
        return;
    }

    let text = historyData.map((item,i)=>
        `${i+1}. ${item.name} ₹${item.high}→₹${item.low} Loss ₹${item.loss.toFixed(2)}`
    ).join("\n");

    if(navigator.share){
        navigator.share({text}).catch(()=>fallback(text));
    } else {
        fallback(text);
    }

    function fallback(text){
        if(navigator.clipboard){
            navigator.clipboard.writeText(text);
            alert("Copied! Paste anywhere");
        } else {
            prompt("Copy this:", text);
        }
    }
}

// EXPORT CSV
function exportExcel(){
    let csv = "No,Name,High,Low,Loss\n";
    historyData.forEach((item,i)=>{
        csv += `${i+1},${item.name},${item.high},${item.low},${item.loss}\n`;
    });

    let blob = new Blob([csv], {type:'text/csv'});
    let a = document.createElement("a");
    a.href = URL.createObjectURL(blob);
    a.download = "investment_history.csv";
    a.click();
}

</script>

</body>
</html>
