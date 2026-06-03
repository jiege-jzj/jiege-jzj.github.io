<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>智慧饭堂预约系统</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:"Microsoft YaHei",sans-serif;
}

body{
    background:#f5f7fa;
    padding:20px;
}

.container{
    max-width:900px;
    margin:auto;
}

h1{
    text-align:center;
    color:#2c3e50;
    margin-bottom:20px;
}

.card{
    background:white;
    border-radius:12px;
    padding:20px;
    margin-bottom:20px;
    box-shadow:0 2px 10px rgba(0,0,0,0.08);
}

.food-item{
    display:flex;
    justify-content:space-between;
    align-items:center;
    margin:15px 0;
    padding:15px;
    background:#f8f9fb;
    border-radius:10px;
}

button{
    background:#27ae60;
    color:white;
    border:none;
    padding:8px 16px;
    border-radius:6px;
    cursor:pointer;
}

button:hover{
    background:#219150;
}

.time-select{
    width:100%;
    padding:10px;
    margin-top:10px;
    border:1px solid #ddd;
    border-radius:6px;
}

.progress{
    width:100%;
    background:#e0e0e0;
    height:18px;
    border-radius:10px;
    overflow:hidden;
    margin-top:8px;
}

.progress-bar{
    height:100%;
    background:#3498db;
}

.high{
    background:#e74c3c;
}

.medium{
    background:#f39c12;
}

.low{
    background:#2ecc71;
}

.status{
    margin-top:5px;
    font-size:14px;
    color:#666;
}
</style>
</head>

<body>

<div class="container">

<h1>🍱 智慧饭堂预约系统</h1>

<div class="card">
<h2>选择就餐时间</h2>

<select id="time" class="time-select">
<option>11:30-12:00</option>
<option>12:00-12:30</option>
<option>12:30-13:00</option>
<option>13:00-13:30</option>
</select>
</div>

<div class="card">
<h2>今日菜品</h2>

<div class="food-item">
<span>🍗 黄焖鸡米饭</span>
<button onclick="reserve('黄焖鸡米饭')">预约</button>
</div>

<div class="food-item">
<span>🥩 红烧排骨饭</span>
<button onclick="reserve('红烧排骨饭')">预约</button>
</div>

<div class="food-item">
<span>🍜 牛肉面</span>
<button onclick="reserve('牛肉面')">预约</button>
</div>

<div class="food-item">
<span>🍛 咖喱鸡饭</span>
<button onclick="reserve('咖喱鸡饭')">预约</button>
</div>

</div>

<div class="card">
<h2>各时间段预约人数</h2>

<div>
11:30-12:00
<div class="progress">
<div id="p1" class="progress-bar low" style="width:20%"></div>
</div>
<div class="status" id="s1">20人（推荐）</div>
</div>

<br>

<div>
12:00-12:30
<div class="progress">
<div id="p2" class="progress-bar medium" style="width:55%"></div>
</div>
<div class="status" id="s2">55人（较拥挤）</div>
</div>

<br>

<div>
12:30-13:00
<div class="progress">
<div id="p3" class="progress-bar high" style="width:90%"></div>
</div>
<div class="status" id="s3">90人（高峰期）</div>
</div>

<br>

<div>
13:00-13:30
<div class="progress">
<div id="p4" class="progress-bar low" style="width:35%"></div>
</div>
<div class="status" id="s4">35人（推荐）</div>
</div>

</div>

</div>

<script>

let count = {
    "11:30-12:00":20,
    "12:00-12:30":55,
    "12:30-13:00":90,
    "13:00-13:30":35
};

function reserve(food){

    let time = document.getElementById("time").value;

    count[time]++;

    updateDisplay();

    alert(
        "预约成功！\n\n菜品："+food+
        "\n时间："+time
    );
}

function updateDisplay(){

    let times = Object.keys(count);

    times.forEach((t,index)=>{

        let value = count[t];

        let bar = document.getElementById("p"+(index+1));
        let text = document.getElementById("s"+(index+1));

        let width = Math.min(value,100);

        bar.style.width = width+"%";

        if(value<40){
            bar.className="progress-bar low";
            text.innerHTML=value+"人（推荐）";
        }
        else if(value<70){
            bar.className="progress-bar medium";
            text.innerHTML=value+"人（较拥挤）";
        }
        else{
            bar.className="progress-bar high";
            text.innerHTML=value+"人（高峰期）";
        }

    });
}

</script>

</body>
</html>
