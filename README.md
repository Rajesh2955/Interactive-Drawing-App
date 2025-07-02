# Interactive-Drawing-App using JS
An interactive drawing app that lets users draw freely on a canvas using customizable brush size and color.
import IPython.display as display

html_content = """
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Interactive Drawing App</title>
  <style>
    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin: 0;
      background: #f0f0f0;
    }
    canvas {
      border: 2px solid #000;
      background: #fff;
      margin-top: 20px;
      cursor: crosshair;
    }
    .controls {
      margin-top: 20px;
    }
    .controls input {
      margin: 0 5px;
    }
  </style>
</head>
<body>

  <h2>Interactive Drawing App</h2>
  <div class="controls">
    <label>Choose Color: <input type="color" id="colorPicker" value="#000000"></label>
    <button onclick="clearCanvas()">Clear</button>
  </div>
  <canvas id="drawCanvas" width="800" height="500"></canvas>

  <script>
    const canvas = document.getElementById('drawCanvas');
    const ctx = canvas.getContext('2d');
    const colorPicker = document.getElementById('colorPicker');
    let drawing = false;

    canvas.addEventListener('mousedown', () => drawing = true);
    canvas.addEventListener('mouseup', () => drawing = false);
    canvas.addEventListener('mouseleave', () => drawing = false);

    canvas.addEventListener('mousemove', draw);

    function draw(e) {
      if (!drawing) return;

      ctx.lineWidth = 2;
      ctx.lineCap = 'round';
      ctx.strokeStyle = colorPicker.value;

      ctx.lineTo(e.offsetX, e.offsetY);
      ctx.stroke();
      ctx.beginPath();
      ctx.moveTo(e.offsetX, e.offsetY);
    }
    function clearCanvas() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.beginPath();
    } // Added closing brace

  </script>

</body>
</html>
"""

display.display(display.HTML(html_content))
