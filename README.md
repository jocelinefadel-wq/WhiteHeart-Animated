<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>White Heart with A</title>
  <style>
    body {
      margin: 0;
      background: black;
      display: flex;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      font-family: Arial, sans-serif;
      overflow: hidden;
    }

    .container {
      position: relative;
      width: 100vw;
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    canvas {
      display: block;
      background: black;
    }

    .text {
      position: absolute;
      bottom: 60px;
      left: 50%;
      transform: translateX(-50%);
      color: white;
      font-weight: bold;
      font-size: clamp(18px, 2vw, 26px);
      text-align: center;
      letter-spacing: 0.5px;
    }
  </style>
</head>
<body>
  <div class="container">
    <canvas id="heartCanvas" width="900" height="900"></canvas>
    <div class="text">you're doin' well </div>
  </div>

  <script>
    const canvas = document.getElementById("heartCanvas");
    const ctx = canvas.getContext("2d");
    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2 + 20;

    const heartPoints = [];
    const totalPoints = 240;
    const scale = 28;

    for (let i = 0; i <= totalPoints; i++) {
      const angle = (i / totalPoints) * (Math.PI * 2);
      const x = 16 * Math.pow(Math.sin(angle), 3) * scale;
      const y = (
        13 * Math.cos(angle) -
        5 * Math.cos(2 * angle) -
        2 * Math.cos(3 * angle) -
        Math.cos(4 * angle)
      ) * scale;

      heartPoints.push({ x, y });
    }

    const drawHeartSlowly = async () => {
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      ctx.lineWidth = 3;
      ctx.strokeStyle = "white";
      ctx.fillStyle = "white";
      ctx.beginPath();

      for (let i = 0; i < heartPoints.length; i++) {
        const p = heartPoints[i];
        const x = centerX + p.x;
        const y = centerY - p.y;

        if (i === 0) {
          ctx.moveTo(x, y);
        } else {
          ctx.lineTo(x, y);
        }

        ctx.stroke();
        await new Promise(r => setTimeout(r, 12));
      }

      ctx.closePath();
      ctx.fill();
      ctx.stroke();

      // Blue A inside the heart
      ctx.fillStyle = "#A5D9FD";
      ctx.font = "bold 52px Arial";
      ctx.textAlign = "center";
      ctx.textBaseline = "middle";
      ctx.fillText("A", centerX, centerY - 8);
    };

    drawHeartSlowly();
  </script>
</body>
</html>
