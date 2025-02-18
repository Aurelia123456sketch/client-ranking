<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Рейтинг клиентов</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f7fa;
            color: #333;
            margin: 0;
            padding: 0;
        }
        .container {
            width: 80%;
            margin: 30px auto;
            padding: 20px;
            background-color: #fff;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
        }
        h1 {
            text-align: center;
            color: #004085;
            margin-bottom: 30px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            padding: 15px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        th {
            background-color: #004085;
            color: #fff;
        }
        .blurred {
            letter-spacing: 3px;
            color: #bbb;
        }
        .amount {
            color: #007bff;
        }
        .cell {
            font-weight: bold;
        }
        .animate {
            transition: transform 1s ease-in-out;
        }
        .refresh-btn {
            margin: 20px auto;
            display: block;
            padding: 10px 20px;
            background-color: #004085;
            color: white;
            border: none;
            font-size: 16px;
            cursor: pointer;
            border-radius: 5px;
        }
        .refresh-btn:hover {
            background-color: #003366;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Рейтинг клиентов</h1>
    <table id="clientTable">
        <thead>
            <tr>
                <th>ФИО</th>
                <th>Номер телефона</th>
                <th>Адрес</th>
                <th>Сумма перевода (€)</th>
            </tr>
        </thead>
        <tbody>
            <!-- Клиенты будут добавляться сюда с помощью JS -->
        </tbody>
    </table>
    <button class="refresh-btn" onclick="shuffleClients()">Перемешать список</button>
</div>

<script>
    // Массив с клиентами (ФИО, телефон, адрес, сумма перевода)
    const clients = [
        { name: 'Иванов Иван Иванович', phone: '+7 (900) 123-45-67', address: 'г. Москва, ул. Примерная, д. 10', amount: 250000 },
        { name: 'Петрова Мария Александровна', phone: '+7 (900) 234-56-78', address: 'г. Санкт-Петербург, ул. Новая, д. 25', amount: 300000 },
        { name: 'Смирнов Алексей Викторович', phone: '+7 (900) 345-67-89', address: 'г. Екатеринбург, ул. Другая, д. 5', amount: 220000 },
        { name: 'Козлова Наталья Павловна', phone: '+7 (900) 456-78-90', address: 'г. Казань, ул. Старая, д. 30', amount: 400000 },
        { name: 'Дмитриев Дмитрий Сергеевич', phone: '+7 (900) 567-89-01', address: 'г. Новосибирск, ул. Центральная, д. 15', amount: 280000 },
    ];

    // Функция для добавления клиентов в таблицу
    function populateClients() {
        const tbody = document.querySelector('#clientTable tbody');
        tbody.innerHTML = ''; // Очистить таблицу перед добавлением
        clients.forEach(client => {
            const tr = document.createElement('tr');
            tr.classList.add('animate'); // Для анимации

            const tdName = document.createElement('td');
            tdName.textContent = client.name;

            const tdPhone = document.createElement('td');
            tdPhone.textContent = client.phone;

            const tdAddress = document.createElement('td');
            tdAddress.textContent = '****' + client.address.slice(-5); // Заблюренный адрес

            const tdAmount = document.createElement('td');
            tdAmount.classList.add('amount');
            tdAmount.textContent = client.amount.toLocaleString('ru-RU'); // Сумма перевода с форматированием

            tr.appendChild(tdName);
            tr.appendChild(tdPhone);
            tr.appendChild(tdAddress);
            tr.appendChild(tdAmount);

            tbody.appendChild(tr);
        });
    }

    // Функция для перемешивания клиентов
    function shuffleClients() {
        for (let i = clients.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [clients[i], clients[j]] = [clients[j], clients[i]]; // Меняем местами
        }
        populateClients(); // Обновляем таблицу
    }

    // Инициализация
    populateClients();
</script>

</body>
</html>
