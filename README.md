<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>pat's christmas tree!</title>
  <link rel="icon" href="media3/icon.png">
  <style>
    body {
      font-family: Arial, sans-serif;
      background: radial-gradient(circle at top, #2e2e5e, #0f0f1f);
      min-height: 100vh;
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      color: white;
    }

    .container {
      width: 100%;
      max-width: 420px;
      background: white;
      color: black;
      padding: 25px;
      border-radius: 18px;
      box-shadow: 0 20px 40px rgba(0,0,0,0.4);
      text-align: center;
    }

    h2 {
      margin-bottom: 18px;
      font-weight: bold;
    }

    /* ✅ PORTRAIT PHOTO STYLE */
    .photo-box {
      width: 180px;
      height: 240px; /* portrait ratio */
      margin: 0 auto 20px;
      border-radius: 14px;
      background: #ddd;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
      color: #666;
      font-size: 14px;
    }

    .photo-box img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    /* ✅ FIXED TEXT BOX */
    textarea {
      width: 100%;
      height: 110px;
      padding: 14px;
      border-radius: 10px;
      border: 1px solid #ccc;
      resize: none;
      font-size: 15px;
      box-sizing: border-box;
      outline: none;
    }

    textarea:focus {
      border-color: #4a4aff;
    }

    button {
      margin-top: 14px;
      width: 100%;
      padding: 12px;
      border: none;
      border-radius: 10px;
      background: pink;
      color: white;
      font-size: 16px;
      cursor: pointer;
      transition: 0.2s;
    }

    button:hover {
      background: light pink;
    }

    .status {
      margin-top: 12px;
      font-size: 14px;
      min-height: 18px;
    }
  </style>
</head>
<body>

  <div class="container">
    <h2>pat's christmas tree</h2>

    <!-- ✅ PORTRAIT PHOTO -->
    <div class="photo-box">
      <span>photo</span>
      <!-- Replace with:
      <img src="myphoto.jpg">
      -->
    </div>

    <!-- ✅ FIXED MESSAGE INPUT -->
    <textarea id="messageInput" placeholder="Type in your message..."></textarea>
    <button onclick="sendMessage()">send!</button>

    <div class="status" id="status"></div>
  </div>

  <!-- ✅ FIREBASE -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.23.0/firebase-app.js";
    import { getFirestore, collection, addDoc, serverTimestamp } from "https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore.js";

    const firebaseConfig = {
      apiKey: "AIzaSyDhJz9lNXeOZILHJ2uz3IH7LhadYA7STZ4",
      authDomain: "anon-messages-382ec.firebaseapp.com",
      projectId: "anon-messages-382ec",
      storageBucket: "anon-messages-382ec.firebasestorage.app",
      messagingSenderId: "751775572552",
      appId: "1:751775572552:web:3ee2c9771a6dd79aa82e7d",
      measurementId: "G-4B0B19P7JV"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    window.sendMessage = async function () {
      const input = document.getElementById("messageInput");
      const status = document.getElementById("status");
      const text = input.value.trim();

      if (text === "") {
        status.textContent = "message is empty bruh";
        return;
      }

      try {
        await addDoc(collection(db, "messages"), {
          text: text,
          createdAt: serverTimestamp()
        });

        input.value = "";
        status.textContent = "message sent anonymously thank u!";
      } catch (error) {
        console.error(error);
        status.textContent = "failed to send message :c";
      }
    };
  </script>

</body>
</html>
