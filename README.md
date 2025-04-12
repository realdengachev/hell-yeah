<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Сюзе - Платформа курсов</title>
    <style>
        body {
            font-family: 'Segoe UI', sans-serif;
            margin: 0;
            padding: 0;
            background: #f9f9f9;
            color: #333;
        }
        .container {
            padding: 16px;
        }
        .header {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
        }
        .avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            margin-right: 10px;
        }
        .tabs {
            display: flex;
            margin-bottom: 16px;
        }
        .tab {
            padding: 8px 16px;
            cursor: pointer;
        }
        .tab.active {
            border-bottom: 2px solid #007bff;
        }
        .course-card {
            background: white;
            border-radius: 8px;
            padding: 16px;
            margin-bottom: 12px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .progress-bar {
            height: 4px;
            background: #e0e0e0;
            border-radius: 2px;
            margin-top: 8px;
        }
        .progress {
            height: 100%;
            background: #007bff;
            border-radius: 2px;
            width: 50%;  /* Динамически меняется */
        }
        .role-card {
            background: white;
            border-radius: 8px;
            padding: 16px;
            margin-bottom: 12px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container" id="loginScreen">
        <h1>Выбери свою роль на платформе</h1>
        <p>Вы можете стать автором собственного курса или же его студентом</p>
        <div class="role-card" onclick="setRole('author')">
            <h3>Я автор курса</h3>
            <p>Создавайте уникальный и полезный контент для ваших студентов</p>
        </div>
            <div class="role-card" onclick="setRole('student')">
            <h3>Я студент курса</h3>
            <p>Проходите курсы и получайте знания в удобном для вас формате</p>
        </div>
    </div>

 <div class="container" id="mainScreen" style="display: none;">
        <div class="header">
            <img src="https://via.placeholder.com/40" class="avatar" alt="Аватар">
            <div>
                <h2>Кирилл</h2>
                <p>@realdengachev</p>
            </div>
        </div>

  <h1>Мои курсы</h1>
        
  <div class="tabs">
            <div class="tab active">Все</div>
            <div class="tab">Закрепленное</div>
            <div class="tab">Недавнее</div>
        </div>
        
  <h3>Закрепленное</h3>
        
   <div class="course-card">
            <h4>Онлайн-курс</h4>
            <p>Как данные помогают нам разгадывать тайны мозга</p>
            <div class="progress-bar">
                <div class="progress" style="width: 38%;"></div> <!-- 5/13 -->
            </div>
        </div>
        
   <div class="course-card">
            <h4>Онлайн-курс</h4>
            <p>Нам нужны лидеры, которые смело выступают за инклюзивность</p>
            <div class="progress-bar">
                <div class="progress" style="width: 62%;"></div> <!-- 8/13 -->
            </div>
        </div>
    </div>

   <script>
        function setRole(role) {
            // Отправляем роль на бэкенд
            fetch("http://localhost:8000/set_role", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ telegram_id: Telegram.WebApp.initDataUnsafe.user.id, role })
            }).then(() => {
                if (role === "student") {
                    document.getElementById("loginScreen").style.display = "none";
                    document.getElementById("mainScreen").style.display = "block";
                } else {
                    alert("Режим автора в разработке!");
                }
            });
        }

        // Инициализация Telegram WebApp
        window.Telegram.WebApp.expand();
    </script>
</body>
</html>
