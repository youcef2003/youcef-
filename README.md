# youcef-
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Shooting Star Text</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      background: black;
    }
    canvas {
      display: block;
    }
  </style>
</head>
<body>
<canvas id="canvas"></canvas>
<script>
  const canvas = document.getElementById("canvas");
  const ctx = canvas.getContext("2d");
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  const shootingStars = [];
  const text = "I love you a lot youcef";

  function createShootingStar() {
    const startX = Math.random() * canvas.width;
    const startY = Math.random() * canvas.height / 2;

    shootingStars.push({
      x: startX,
      y: startY,
      length: Math.random() * 300 + 100,
      speed: Math.random() * 10 + 6,
      angle: Math.PI / 4,
      opacity: 1,
      textIndex: 0
    });
  }

  function drawShootingStars() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = "rgba(0, 0, 30, 0.3)";
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    shootingStars.forEach((star, index) => {
      const dx = Math.cos(star.angle) * star.speed;
      const dy = Math.sin(star.angle) * star.speed;
      star.x += dx;
      star.y += dy;
      star.opacity -= 0.002;

      ctx.font = "20px Arial";
      ctx.fillStyle = `rgba(255, 0, 0, ${star.opacity})`;

      if (star.textIndex < text.length) {
        ctx.fillText(text[star.textIndex], star.x, star.y);
        star.textIndex++;
      }

      if (star.opacity <= 0 || star.textIndex >= text.length) {
        shootingStars.splice(index, 1);
      }
    });
  }

  function animate() {
    drawShootingStars();
    requestAnimationFrame(animate);
  }

  setInterval(createShootingStar, 3000);
  animate();
</script>
</body>
</html>
