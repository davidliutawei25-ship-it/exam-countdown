<!DOCTYPE html>
<html lang="zh">
<head>
<meta charset="UTF-8">
<title>考试倒计时 | Exam Countdown</title>

<style>
body {
    font-family: Arial, sans-serif;
    text-align: center;
    background: #ffffff;
    color: #111827;
    padding: 40px;
}

h1 {
    font-size: 32px;
}

#stressBox {
    margin: 20px auto;
    padding: 16px;
    width: 80%;
    max-width: 650px;
    border-radius: 12px;
    font-size: 18px;
    font-weight: 800;
    background: #fff5f5;
    border: 2px solid #ef4444;
    color: #b91c1c;
}

.exam {
    margin-top: 20px;
    padding: 18px;
    border: 1px solid #e5e7eb;
    border-radius: 12px;
    width: 340px;
    margin-left: auto;
    margin-right: auto;
    background: #ffffff;
}

.title {
    font-size: 20px;
    color: #2563eb;
}

.time {
    font-size: 32px;
    margin-top: 10px;
}

.tag {
    font-size: 12px;
    color: #6b7280;
    margin-bottom: 6px;
}

button {
    margin-top: 25px;
    padding: 10px 18px;
    border-radius: 8px;
    cursor: pointer;
}
</style>
</head>

<body>

<h1 id="mainTitle">考试倒计时</h1>

<div id="stressBox">时间正在逼近，请保持专注。</div>

<!-- 🌱 Chunkao -->
<div class="exam">
    <div class="tag">春考 / Chunkao</div>
    <div class="title" id="springTitle">春考倒计时</div>
    <div class="time" id="spring"></div>
</div>

<!-- 📘 Dengjikao -->
<div class="exam">
    <div class="tag">等级考 / Dengjikao</div>
    <div class="title" id="levelTitle">等级考倒计时</div>
    <div class="time" id="level"></div>
</div>

<!-- 🎯 Gaokao -->
<div class="exam">
    <div class="tag">高考 / Gaokao</div>
    <div class="title" id="gaokaoTitle">高考倒计时</div>
    <div class="time" id="gaokao"></div>
</div>

<button onclick="toggleLang()">English / 中文</button>

<script>
let isChinese = true;

const exams = {
    gaokao: new Date("2027-06-07 09:00:00"),
    level: new Date("2027-05-05 09:00:00"),
    spring: new Date("2027-01-02 09:00:00")
};

// 🚨 紧迫语句
const stressCN = [
    "你高考考不好就完了！",
    "高考决定你一辈子！",
    "你能考上上海公办吗？",
    "你未来能找到工作吗？",
    "别人比你努力多了！",
    "你将来怎么办？",
    "你这点努力还不够！",
    "时间正在逼近，请保持专注。"
];

const stressEN = [
    "If you fail Gaokao, everything is over!",
    "Gaokao decides your entire future!",
    "Can you get into a public university in Shanghai?",
    "Will you be able to find a job in the future?",
    "Others are working much harder than you!",
    "What will you do in the future?",
    "Your effort is still not enough!",
    "Time is closing in. Stay focused."
];

let index = 0;

// ⏱ 倒计时
function format(diff) {
    if (diff <= 0) return isChinese ? "已开始 / 已结束" : "Started / Finished";

    const d = Math.floor(diff / (1000 * 60 * 60 * 24));
    const h = Math.floor((diff / (1000 * 60 * 60)) % 24);
    const m = Math.floor((diff / (1000 * 60)) % 60);
    const s = Math.floor((diff / 1000) % 60);

    return `${d}${isChinese ? "天" : "d"} ${h}${isChinese ? "小时" : "h"} ${m}${isChinese ? "分" : "m"} ${s}${isChinese ? "秒" : "s"}`;
}

// 🔄 更新倒计时
function update() {
    const now = new Date();

    document.getElementById("gaokao").innerHTML = format(exams.gaokao - now);
    document.getElementById("level").innerHTML = format(exams.level - now);
    document.getElementById("spring").innerHTML = format(exams.spring - now);
}

// 🚨 紧迫提示
function updateStress() {
    document.getElementById("stressBox").innerText =
        isChinese ? stressCN[index] : stressEN[index];

    index = (index + 1) % stressCN.length;
}

// 🌍 切换语言
function toggleLang() {
    isChinese = !isChinese;

    document.getElementById("mainTitle").innerText =
        isChinese ? "考试倒计时" : "Exam Countdown";

    document.getElementById("springTitle").innerText =
        isChinese ? "春考倒计时" : "Chunkao Countdown";

    document.getElementById("levelTitle").innerText =
        isChinese ? "等级考倒计时" : "Dengjikao Countdown";

    document.getElementById("gaokaoTitle").innerText =
        isChinese ? "高考倒计时" : "Gaokao Countdown";
}

setInterval(update, 1000);
setInterval(updateStress, 3000);

update();
updateStress();
</script>

</body>
</html>
