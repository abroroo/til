### What is the Canvas API?
The [Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) is a part of the HTML5 specification, providing a means to draw graphics, shapes, text, and images dynamically within an HTML `<canvas>` element using JavaScript.

The Canvas API provides a 2D drawing context `CanvasRenderingContext2D` , It's a primary interface to use JavaScript with the canvas.  
You obtain the 2D context using the `getContext('2d')` method on the `<canvas>` element.

#### Basic Usage:
1. Set Up Canvas Element `<canvas id="myCanvas" width="500" height="500"></canvas>`
2. Obtaining 2D Context:
   
   ```
   const canvas = document.getElementById('myCanvas');
   const ctx = canvas.getContext('2d');
   ```
3. Drawing Shapes:

   ```
    // Draw a rectangle
      ctx.fillStyle = 'red'; // Set fill color
      ctx.fillRect(50, 50, 100, 100); // (x, y, width, height)
      
    // Draw a circle
      ctx.beginPath();
      ctx.arc(250, 250, 50, 0, 2 * Math.PI); // (x, y, radius, startAngle, endAngle)
      ctx.fillStyle = 'blue';
      ctx.fill();


   ```

4. You can also draw text, text will be an image

   ```
   ctx.font = '30px Arial';
   ctx.fillStyle = 'green';
   ctx.fillText('Hello Canvas!', 200, 200); // (text, x, y)

   ```
5. Working with images:

   ```
    const img = new Image();
    img.src = 'path/to/image.png';
    img.onload = function() {
      ctx.drawImage(img, 50, 50); // Draw image at (x, y)
    };


   ```
   > Drawing Images: Load and draw images onto the canvas using methods like `drawImage()`, supporting various formats and transformations.
   > 
   > Image Data: Access and manipulate individual pixels of the canvas using `getImageData()`, `putImageData()`, enabling advanced image processing and effects.
