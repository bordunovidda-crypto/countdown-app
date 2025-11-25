
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Пиксельный Таймер</title>

<style>
    body {
        margin: 0;
        padding: 0;
        font-family: 'Courier New', monospace;
        background: radial-gradient(circle, #001020, #000000);
        color: #b8d7ff;
        text-align: center;
    }

    .container {
        width: 90%;
        max-width: 480px;
        margin: 40px auto;
        padding: 20px;
        border: 1px solid #3d5b80;
        border-radius: 12px;
        background: rgba(0, 40, 80, 0.25);
        backdrop-filter: blur(3px);
    }

    h1 {
        font-size: 28px;
        margin-bottom: 25px;
        letter-spacing: 2px;
    }

    label {
        display: block;
        text-align: left;
        margin: 12px 0 5px;
        font-size: 18px;
    }

    input {
        width: 100%;
        padding: 12px;
        font-size: 18px;
        border-radius: 8px;
        border: 1px solid #4d7bb5;
        background: rgba(0,0,0,0.4);
        color: #d0e6ff;
    }

    button {
        width: 100%;
        margin-top: 22px;
        padding: 14px;
        font-size: 20px;
        background: #b9d7ff;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        font-weight: bold;
        transition: 0.2s;
    }

    button:hover {
        background: #dff0ff;
    }

    .hidden {
        display: none;
    }

    .timer {
        font-size: 42px;
        margin: 25px 0;
        letter-spacing: 3px;
    }

    .segment {
        font-size: 18px;
        margin-top: 20px;
        opacity: 0.8;
    }
</style>

</head>
<body>

<!-- СТРАНИЦА 1 -->
<div id="page1" class="container">
    <h1>Таймер</h1>

    <label>Ваше имя:</label>
    <input id="nameInput" type="text" placeholder="Введите имя">

    <label>Событие:</label>
    <input id="eventInput" type="text" placeholder="Например: День рождения">

    <label>Дата события:</label>
    <input id="dateInput" type="date">

    <button id="nextBtn">Продолжить</button>

    <p class="info">Ваши данные хранятся только на устройстве.</p>
</div>

<!-- СТРАНИЦА 2 -->
<div id="page2" class="container hidden">
    <h1 id="eventTitle">Обратный отсчёт</h1>
    <div id="timer" class="timer">00:00:00</div>
    <div id="segments" class="segment">Ожидание даты…</div>
</div>

<script>
document.getElementById("nextBtn").addEventListener("click", function () {

    const name = document.getElementById("nameInput").value.trim();
    const eventName = document.getElementById("eventInput").value.trim();
    const date = document.getElementById("dateInput").value;

    if (!name  !eventName  !date) {
        alert("Заполни все поля!");
        return;
    }

    // Показываем вторую страницу
    document.getElementById("page1").classList.add("hidden");
    document.getElementById("page2").classList.remove("hidden");

    document.getElementById("eventTitle").innerText = eventName;

    startTimer(date);
});

function startTimer(targetDate) {
    const target = new Date(targetDate).getTime();

    setInterval(() => {
        const now = new Date().getTime();
        const diff = target - now;

        if (diff <= 0) {
            document.getElementById("timer").innerText = "00:00:00";
            document.getElementById("segments").innerText = "Событие наступило!";
            return;
        }

        const days = Math.floor(diff / (1000 * 60 * 60 * 24));
        const hours = Math.floor((diff / (1000 * 60 * 60)) % 24);
        const minutes = Math.floor((diff / (1000 * 60)) % 60);
        const seconds = Math.floor((diff / 1000) % 60);

        document.getElementById("timer").innerText =
            ${String(hours).padStart(2,'0')}:${String(minutes).padStart(2,'0')}:${String(seconds).padStart(2,'0')};

        document.getElementById("segments").innerHTML =
            Дней: <b>${days}</b><br>Часов: <b>${hours}</b><br>Минут: <b>${minutes}</b><br>Секунд: <b>${seconds}</b>;
    }, 1000);
}
</script>

</body>
</html>
