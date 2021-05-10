# drawingApp
Application built using HTML, CSS, and JS which allows for the creation of art on a digital canvas.

Constructing this project has helped me to better practice and understand the following:
1) Working with HTML <canvas> element.
2) Using ctx. for canvasArc().
3) Using requestAnimationFrame().
4) Drawing methods.

This project is baseline - it can be restyled as needed. An extra function could be a save button which would keep specified works stored inside of the local storage.

A general walkthrough of the JavaScript is given below.

First, select the DOM elements to be manipulated. Then construct the drawCircle() function.
```JavaScript
const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');
const increaseBtn = document.getElementById('increase');
const decreaseBtn = document.getElementById('decrease');

function drawCircle(x,y) {
    ctx.beginPath();
    ctx.arc(x, y, size, 0, Math.PI * 2);
    ctx.fillStyle = color;
    ctx.fill();
}
```

Add event listeners to the canvas to enable drawing.
```JavaScript
canvas.addEventListener('mousedown', () => {
    isPressed = true;
    x = e.offsetX;
    y = e.offsetY;
});

canvas.addEventListener('mouseup', () => {
    isPressed = false;

    x = undefined;
    y = undefined;
});

canvas.addEventListener('mousemove', (e) => {
    if(isPressed){

        const x2 = e.offsetX;
        const y2 = e.offsetY;
        
        drawCircle(x2,y2);
        drawLine(x,y, x2, y2);
        x = x2;
        y = y2;
    }
});
```

Add event listeners to each of the buttons to change the size of the 'brush'.
```JavaScript
increaseBtn.addEventListener('click', () => {
    size += 5;

    if(size > 50) {
        size = 50;
    }
    updateSizeOnScreen();
});

decreaseBtn.addEventListener('click', () => {
    size -= 5;
    if(size < 5){
        size = 5;
    }
    updateSizeOnScreen();
});
```

Construct the updateSizeOnScreen() function to register the changes in brush size to the UI.
```JavaScript
function updateSizeOnScreen(){
    sizeEl.innerText = size;
}
```

Add an event listener on the colorEl to allow for different colors to be chosen and applied.
```JavaScript
colorEl.addEventListener('change', (e) => {
    color = e.target.value;
})
```

Construct the line() function to allow for smoother painting strokes.
```JavaScript
let x = undefined;
let y = undefined;

function drawLine(x1, y1, x2, y2){
    ctx.beginPath();
    ctx.moveTo(x1,y1);
    ctx.lineTo(x2,y2);
    ctx.strokeStyle = color;
    ctx.lineWidth = size * 2;
    ctx.stroke();
}
```

Add in the clear canvas functionality.
```JavaScript
clearEl.addEventListener('click', () => {
    ctx.clearRect(0,0, canvas.width, canvas.height);
});
```

***End walkthrough
