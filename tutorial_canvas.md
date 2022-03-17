# 1. Canvas - Rectangle
```html
<style>
#c{
	width: 400px;
	height: 200px;
	border: 3px solid black;
}
</style>
<canvas id=c width=400 height=200>Canvas not supported!</canvas>
<script>
window.onload = function(){
	var ctx = c.getContext('2d');
	
	// 1nd rectangle
	ctx.fillStyle = 'red'; // fill color
	ctx.fillRect(100/*x*/,50/*y*/,150/*width*/,75/*height*/);//rectangle
	ctx.clearRect(0,0,400,200); // clear all canvas
	//ctx.clearRect(150,0,400,200); // clear part of canvas
	
	// 2nd rectangle
	ctx.rect(50,10,100,100);
	ctx.strokeStyle = 'green';
	ctx.lineWidth = '10';
	ctx.stroke();
	ctx.fillStyle = 'orange';
	ctx.fill();
}
</script>
```

# 2. Canvas - Line
```html
<style>
#c{
	width: 400px;
	height: 200px;
	border: 3px solid black;
}
</style>
<canvas id=c width=400 height=200>Canvas not supported!</canvas>
<script>
window.onload = function(){
	var ctx = c.getContext('2d');
	
	ctx.beginPath(); // for reset previous style and width!
	ctx.moveTo(100, 50);
	ctx.lineTo(150, 150);
	ctx.strokeStyle = 'red';
	ctx.lineWidth = 5;
	ctx.stroke();
	
	ctx.beginPath(); // for reset previous style and width!
	ctx.strokeStyle = 'blue';
	ctx.lineWidth = 20;
	ctx.moveTo(200, 50);
	ctx.lineTo(300, 50);
	ctx.lineTo(300, 100);
	ctx.lineCap = 'round';
	ctx.lineCap = 'butt'; // for connect corner
	ctx.stroke();
	
	ctx.clearRect(0,0,400,200);
	
	// triangle
	ctx.beginPath();
	ctx.moveTo(50,150);
	ctx.lineTo(150,50);
	ctx.lineTo(200,150);
	ctx.lineWidth = 5;
	ctx.lineCap = 'butt';
	ctx.fillStyle = 'yellow';
	ctx.closePath();  // autoclose path
	ctx.stroke();
	ctx.fill();
}
</script>
```
