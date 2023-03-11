<div style="position: relative; height: 200px; overflow: hidden;">
  <div style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
    <canvas id="background"></canvas>
  </div>
</div>

<style>
  canvas {
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
  }
</style>

<script>
  const canvas = document.getElementById('background');
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  const ctx = canvas.getContext('2d');

  const particles = [];
  for (let i = 0; i < 100; i++) {
    particles.push({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      radius: Math.random() * 2 + 1,
      vx: Math.random() * 0.5 - 0.25,
      vy: Math.random() * 0.5 - 0.25
    });
  }

  function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = 'rgba(255, 255, 255, 0.8)';

    particles.forEach(p => {
      ctx.beginPath();
      ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
      ctx.fill();

      p.x += p.vx;
      p.y += p.vy;

      if (p.x < -50) {
        p.x = canvas.width + 50;
      }
      if (p.y < -50) {
        p.y = canvas.height + 50;
      }
      if (p.x > canvas.width + 50) {
        p.x = -50;
      }
      if (p.y > canvas.height + 50) {
        p.y = -50;
      }
    });

    requestAnimationFrame(draw);
  }

  draw();
</script>
