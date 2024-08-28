<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mesajlaşma Sitesi</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .container {
            width: 80%;
            max-width: 600px;
            margin-top: 20px;
            background: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
        }
        .message-box {
            width: calc(100% - 20px);
            margin-bottom: 10px;
        }
        .message-list {
            max-height: 300px;
            overflow-y: auto;
            margin-bottom: 10px;
            border: 1px solid #ddd;
            padding: 10px;
            background-color: #fafafa;
        }
        .message-item {
            padding: 5px;
            border-bottom: 1px solid #ddd;
        }
        .message-item:last-child {
            border-bottom: none;
        }
        input[type="text"] {
            width: calc(100% - 100px);
            padding: 10px;
            margin-right: 10px;
        }
        input[type="file"] {
            margin-right: 10px;
        }
        button {
            padding: 10px;
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="message-list" id="messageList"></div>
        <input type="text" id="messageInput" placeholder="Mesajınızı yazın...">
        <input type="file" id="fileInput">
        <button onclick="sendMessage()">Gönder</button>
    </div>

    <script>
        function sendMessage() {
            const messageInput = document.getElementById('messageInput');
            const fileInput = document.getElementById('fileInput');
            const messageList = document.getElementById('messageList');

            const message = messageInput.value;
            const file = fileInput.files[0];

            if (message.trim() === '' && !file) {
                alert('Mesaj yazın veya dosya seçin.');
                return;
            }

            const messageItem = document.createElement('div');
            messageItem.classList.add('message-item');
            messageItem.textContent = message;

            if (file) {
                const fileUrl = URL.createObjectURL(file);
                const fileLink = document.createElement('a');
                fileLink.href = fileUrl;
                fileLink.textContent = `Dosya: ${file.name}`;
                fileLink.download = file.name;
                messageItem.appendChild(document.createElement('br'));
                messageItem.appendChild(fileLink);
            }

            messageList.appendChild(messageItem);
            messageInput.value = '';
            fileInput.value = '';
        }
    </script>
</body>
</html>
