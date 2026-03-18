<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Investment Loss Recovery Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #eef2f3;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .box {
            background: #fff;
            padding: 25px;
            width: 430px;
            border-radius: 10px;
            box-shadow: 0 0 10px #999;
        }

        h2 {
            text-align: center;
        }

        label {
            font-weight: bold;
        }

        input, button {
            width: 100%;
            padding: 8px;
            margin: 8px 0;
            font-size: 16px;
        }

        .btn-group {
            display: flex;
            gap: 10px;
        }

        button {
            border: none;
            cursor: pointer;
            color: white;
        }

        .calc-btn {
            background: #007bff;
        }

        .clear-btn {
            background: #dc3545;
        }

        .result {
            background: #f1f1f1;
            padding: 10px;
            border-radius: 5px;
            margin-top: 10px;
        }
    </style>
</head>
<body>

<div class="box">
    <h2>Investment Loss & Recovery</h2>

    <label>High Price (Buy Price)</label>
    <input type="text" id="highPrice" placeholder="e.g. 1,250.50"
           oninput="formatAmount(this)">

    <label>Low Price (Current Price)</label>
    <input type="text" id="lowPrice" placeholder="e.g. 875.25"
           oninput="formatAmount(this)">

    <div class="btn-group">
        <button class="calc-btn" onclick="calculateLoss()">Calculate</button>
        <button class="clear-btn" onclick="clearAll()">Clear</button>
    </div>

    <div class="result">
        <p>Loss Amount: ₹ <span id="lossAmt">0.00</span></p>
        <p>Loss Percentage: <span id="lossPer">0.0000</span> %</p>
        <hr>
        <p><b>Recovery Required</b></p>
        <p>Price must go UP by: <span id="recoveryPer">0.0000</span> %</p>
        <p>Target Price to Recover: ₹ <span id="targetPrice">0.00</span></p>
    </div>
</div>

<script>
    // Auto comma + decimal support (Indian format)
    function formatAmount(input) {
        let value = input.value.replace(/,/g, "");

        if (value === "") return;

        // allow only digits and one decimal point
        if (!/^\d*\.?\d*$/.test(value)) {
            input.value = input.value.slice(0, -1);
            return;
        }

        let parts = value.split(".");
        let intPart = parts[0];
        let decPart = parts.length > 1 ? "." + parts[1] : "";

        let formattedInt = Number(intPart).toLocaleString("en-IN");
        input.value = formattedInt + decPart;
    }

    function calculateLoss() {
        let high = parseFloat(
            document.getElementById("highPrice").value.replace(/,/g, "")
        );
        let low = parseFloat(
            document.getElementById("lowPrice").value.replace(/,/g, "")
        );

        if (isNaN(high) || isNaN(low) || high <= 0 || low <= 0) {
            alert("Please enter valid prices");
            return;
        }

        if (low > high) {
            alert("Low price should be less than High price");
            return;
        }

        let lossAmount = high - low;
        let lossPercent = (lossAmount / high) * 100;
        let recoveryPercent = (lossAmount / low) * 100;

        document.getElementById("lossAmt").innerText =
            lossAmount.toLocaleString("en-IN", { minimumFractionDigits: 2 });

        document.getElementById("lossPer").innerText =
            lossPercent.toFixed(4);

        document.getElementById("recoveryPer").innerText =
            recoveryPercent.toFixed(4);

        document.getElementById("targetPrice").innerText =
            high.toLocaleString("en-IN", { minimumFractionDigits: 2 });
    }

    function clearAll() {
        document.getElementById("highPrice").value = "";
        document.getElementById("lowPrice").value = "";

        document.getElementById("lossAmt").innerText = "0.00";
        document.getElementById("lossPer").innerText = "0.0000";
        document.getElementById("recoveryPer").innerText = "0.0000";
        document.getElementById("targetPrice").innerText = "0.00";
    }
</script>

</body>
</html>
