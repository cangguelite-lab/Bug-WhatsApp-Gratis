```html
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>WA Number Checker</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      background:
        radial-gradient(circle at 50% 30%, #102020 0%, #050707 45%, #000 100%);
      color: #00ffcc;
      font-family: Arial, sans-serif;
      overflow: hidden;
    }

    /* Scanline */
    body::before {
      content: "";
      position: fixed;
      inset: 0;
      pointer-events: none;
      background: repeating-linear-gradient(
        to bottom,
        rgba(0,255,200,.035) 0px,
        rgba(0,255,200,.035) 1px,
        transparent 2px,
        transparent 5px
      );
      animation: scan 7s linear infinite;
    }

    .container {
      width: min(92%, 430px);
      position: relative;
      padding: 32px 25px;
      border: 1px solid #00ffcc;
      border-radius: 18px;
      background: rgba(2, 12, 12, .92);
      box-shadow:
        0 0 12px #00ffcc,
        0 0 40px rgba(0,255,204,.18),
        inset 0 0 25px rgba(0,255,204,.05);
      text-align: center;
      animation: float 4s ease-in-out infinite;
    }

    .glitch {
      position: relative;
      display: inline-block;
      font-size: 29px;
      font-weight: 900;
      letter-spacing: 3px;
      margin-bottom: 8px;
      text-shadow:
        2px 0 #ff0055,
        -2px 0 #00ffff,
        0 0 15px #00ffcc;
      animation: glitch 2.5s infinite;
    }

    .subtitle {
      color: #8aaaa5;
      font-size: 13px;
      margin-bottom: 28px;
    }

    .input-box {
      width: 100%;
      padding: 14px;
      border: 1px solid #00ffcc;
      border-radius: 10px;
      outline: none;
      background: #020707;
      color: #00ffcc;
      font-size: 16px;
      text-align: center;
      box-shadow: inset 0 0 12px rgba(0,255,204,.08);
    }

    .input-box:focus {
      box-shadow:
        0 0 10px #00ffcc,
        inset 0 0 12px rgba(0,255,204,.1);
    }

    .btn {
      width: 100%;
      margin-top: 15px;
      padding: 14px;
      border: none;
      border-radius: 10px;
      background: #00ffcc;
      color: #00100d;
      font-size: 15px;
      font-weight: 900;
      cursor: pointer;
      letter-spacing: 1px;
      transition: .2s;
      box-shadow: 0 0 15px rgba(0,255,204,.6);
    }

    .btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 0 28px #00ffcc;
    }

    .result {
      display: none;
      margin-top: 22px;
      padding: 15px;
      border-radius: 10px;
      border: 1px solid #00ffcc;
      background: rgba(0,255,204,.05);
      line-height: 1.7;
      font-size: 14px;
    }

    .safe {
      color: #00ff99;
    }

    .invalid {
      color: #ff3864;
    }

    .footer {
      margin-top: 22px;
      color: #526b66;
      font-size: 11px;
    }

    @keyframes glitch {
      0%, 90%, 100% {
        transform: translate(0);
      }
      92% {
        transform: translate(-3px, 2px);
      }
      94% {
        transform: translate(3px, -2px);
      }
      96% {
        transform: translate(-2px, -1px);
      }
    }

    @keyframes float {
      0%, 100% {
        transform: translateY(0);
      }
      50% {
        transform: translateY(-7px);
      }
    }

    @keyframes scan {
      from {
        transform: translateY(-10%);
      }
      to {
        transform: translateY(10%);
      }
    }
  </style>
</head>

<body>

  <main class="container">

    <div class="glitch">WA CHECKER</div>

    <p class="subtitle">
      NEON GLITCH • LOCAL NUMBER VALIDATOR
    </p>

    <input
      id="number"
      class="input-box"
      type="text"
      inputmode="numeric"
      placeholder="Contoh: 628123456789"
      autocomplete="off"
    >

    <button class="btn" onclick="checkNumber()">
      CHECK NUMBER
    </button>

    <div id="result" class="result"></div>

    <div class="footer">
      Pemeriksaan dilakukan secara lokal • Tidak mengirim pesan
    </div>

  </main>

  <script>
    function checkNumber() {
      const input = document.getElementById("number");
      const result = document.getElementById("result");

      let number = input.value.trim();

      // Hanya angka
      number = number.replace(/\D/g, "");

      result.style.display = "block";

      if (!number) {
        result.innerHTML =
          '<span class="invalid">✖ Masukkan nomor terlebih dahulu.</span>';
        return;
      }

      // Validasi sederhana nomor internasional
      if (/^62\d{8,13}$/.test(number)) {
        result.innerHTML = `
          <span class="safe">✔ FORMAT VALID</span><br>
          Nomor: +${number}<br>
          Status: Format nomor terlihat benar.
        `;
      } else {
        result.innerHTML = `
          <span class="invalid">✖ FORMAT TIDAK VALID</span><br>
          Gunakan format internasional.<br>
          Contoh: 628123456789
        `;
      }
    }

    document.getElementById("number").addEventListener("keydown", function(e) {
      if (e.key === "Enter") {
        checkNumber();
      }
    });
  </script>

</body>
</html>
```