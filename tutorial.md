# 12. Create slider

```html
  <style>
    #slider{
      width:288px;             /*1. 96+96+96 */
      height:96px;
      border:5px solid black;
      margin:50px auto;
      overflow:hidden;
    }
    #row{
      /*background: pink;*/
      width: 672px;            /*4. 96*7pics */
      position: relative;      /*5. for enable property:LEFT work in js*/
      transition: all ease 1s; /*6. for beautify */
      left: 0;                 /*6. for beautify (antijerk)*/
    }
    #row img{
      float: left;             /*2. remove new lines in html for fit 3 pics in box - every width about 4px*/
    }
    #row::after{               /*3. return to #row height, that was removed by float property, see above */
      content: '';
      display: block;
      clear:both;
    }
  </style>
  <div id='slider'>
    <div id='row'>
      <img src='https://img.icons8.com/fluency/96/000000/dog.png'/>
      <img src='https://img.icons8.com/fluency/96/000000/parrot.png'/>
      <img src='https://img.icons8.com/fluency/96/000000/peacock.png'/>
      <img src='https://img.icons8.com/fluency/96/000000/owl.png'/>
      <img src='https://img.icons8.com/fluency/96/000000/peace-pigeon.png'/>
      <img src='https://img.icons8.com/fluency/96/000000/duck.png'/>
      <img src='https://img.icons8.com/fluency/96/000000/flamingo.png'/>
    </div>
  </div>
  <button id='slider-left'>left</button>
  <script>
    document.querySelector('#slider-left').onclick = sliderLeft;
    var left = 0;
    function sliderLeft(){
      let row = document.querySelector('#row');
      left -= 96;
      if(left<-392) left=0;
      row.style.left = left +'px';
    }
  </script>
```

# 13. Create slider with timer
```html
  <style>
    #slider{
      width:288px;             /*1. 96+96+96 */
      height:96px;
      border:5px solid black;
      margin:50px auto;
      overflow:hidden;
    }
    #row{
      /*background: pink;*/
      width: 672px;            /*4. 96*7pics */
      position: relative;      /*5. for enable property:LEFT work in js*/
      transition: all ease 1s; /*6. for beautify */
      left: 0;                 /*6. for beautify (antijerk)*/
    }
    #row img{
      float: left;             /*2. remove new lines in html for fit 3 pics in box - every width about 4px*/
    }
    #row::after{               /*3. return to #row height, that was removed by float property, see above */
      content: '';
      display: block;
      clear:both;
    }
  </style>
  <div id='slider'>
    <div id='row'>
      <img src='https://img.icons8.com/fluency/96/000000/dog.png'/>
      <img src='https://img.icons8.com/fluency/96/000000/parrot.png'/>
      <img src='https://img.icons8.com/fluency/96/000000/peacock.png'/>
      <img src='https://img.icons8.com/fluency/96/000000/owl.png'/>
      <img src='https://img.icons8.com/fluency/96/000000/peace-pigeon.png'/>
      <img src='https://img.icons8.com/fluency/96/000000/duck.png'/>
      <img src='https://img.icons8.com/fluency/96/000000/flamingo.png'/>
    </div>
  </div>
  <script>
    //document.querySelector('#slider-left').onclick = sliderLeft;
    autoSlider();
    var left = 0;
    var timer = 0;
    function autoSlider(){
      timer = setTimeout(function(){
        let row = document.querySelector('#row');
        left -= 96;
        if(left<-392) {left=0;clearTimeout(timer);}
        row.style.left = left +'px';
        autoSlider();
      }, 1000);
    }
  </script> 
```

# 15. Radiobutton
```html
<p><input type='radio' name='fruit' value='????????????'> ????????????</p>
  <p><input type='radio' name='fruit' value='??????????'> ??????????</p>
  <button id=a>Push</button>
  <script>
    var radio = [...document.querySelectorAll('[name=fruit]')];
    
    for (let i=0; i<radio.length; i++){
      radio[i].onchange = testRadio;
    }
    function testRadio() {
      console.log(this.value);
    }
    
    a.onclick = checkRadio;
    function checkRadio(){
      for (let i=0; i<radio.length; i++){
        if (radio[i].checked){
          alert(radio[i].value);
          break;
        }
      }
    }
  </script>
```

# 16. App - CSS generator
```html
<style>
#test{
	width: 150px;
	height: 150px;
	background: orange;
	margin: 10px;
}
#out{
	width: 300px;
	height: 25px;
	margin: 10px;
}
</style>
<p>Border-radius: <input type='range' id=r1 value='0'></p>
<div id=test></div>
<textarea id=out></textarea>
<script>
document.querySelector('#r1').oninput = cssGenerator; // oninput - every range moving
function cssGenerator() {
	var div = document.querySelector('#test');
	var out = document.querySelector('#out');
	div.style.borderRadius = this.value + 'px';
	out.innerHTML = 'border-radius: '+this.value+'px';
}
</script>
```

# 20. Function
```javascript
function sum(a,b){
	a = a || 10; // undefined || 10 return 10
	b = b || 10; // undefined || 20 return 20
	return alert(a+b);
}

//document.querySelector('#btn').onclick = sum; // Error
document.querySelector('#btn').onclick = function(){ //anonymous function
	sum(1,2);
}
```

# 21. Mouse events
```html
<style>
#one{
	width: 50px;
	height: 50px;
	background: orange;
}
</style>
<div id=one></div>
<script>
var block = document.querySelector('#one');
var a = 0;
// mouse -- click
block.onclick = function(){
	this.style.background = 'green';
	this.onclick = null                // cancel event
}
// mouse -- double click
block.ondblclick = function(){
	this.style.background = 'red';
}
// mouse -- click right mouse button
block.oncontextmenu = function(){
	this.style.background = 'black';
	return false; // ATTENTION! addition for prevent browser to show context menu after click
}
// mouse -- hover
block.onmouseenter = function(){
	console.log('mouse in block!');
}
// mouse -- unhover
block.onmouseleave = function(){
	console.log('mouse out from block!');
}
// mouse -- move in
block.onmousemove = function(){
	a++;
	this.style.width = 50 + a + 'px';
}
// mouse -- press and hold button
block.onmousedown = function(event){
	this.style.background = 'cyan';
	console.log('button: ' + event.button); // show type of mouse button (0 - left button, 1 - scroll click, 2 - right button)
	console.log('which: ' + event.which); // show type of mouse button (not cross-browser version)
}
// mouse -- unpress button
block.onmouseup = function(){
	this.style.background = 'pink';
}
</script>
```

# 22. Img follow cursor
```html
<script>
document.onmousemove = function(){
	document.body.insertAdjacentHTML('beforeEnd', '<img  id=cat src=https://img.icons8.com/emoji/96/000000/cat-emoji.png />');
	cat.style.position = 'fixed';
	document.onmousemove = function(event){
		cat.style.left = event.clientX + 10 + 'px';
		cat.style.top = event.clientY + 10 + 'px';
	}
}
</script>
```

# 23. APP - Photo differ
```html
<style>
#myslide{
	width: 240px;
	height: 240px;
	border: 3px solid black;
	position: relative;
	overflow: hidden;
}
#one, #two{
	width: 240px;
	height: 240px;
	position: absolute;
	left: 0;
	top: 0;
	overflow: hidden;
	transition: all ease 500ms;
}
#one { background: yellow; }
#two { background: blue; }
</style>
<div id=myslide>
	<div id=one>
		<img src='https://img.icons8.com/fluency/240/000000/sun.png' />
	</div>
	<div id=two>
		<img src='https://img.icons8.com/material-rounded/240/000000/sun--v1.png' />
	</div>
</div>
<script>
myslide.onmousemove = function(event){
	var x  = event.offsetX; // coord mouse relative by parent block
	two.style.width = x + 'px';
}
myslide.onmouseleave = function(event){
	two.style.width = '240px';
}
</script>
```

# 25. Keyboard events
```javascript
document.onkeypress = function(event){
	console.log(event);        // altKey, charCode, keyCode, ...
	console.log(event.key)     // a, ??, 2, , Z, /, ...
	if (event.shiftKey) {
		console.log('Shift pressed')
	}
	if (event.keyCode<48 || event.keyCode>57){
		console.log('no digit!');
		return false;      // cancel put symbol to input or smth
	}
	
}
```

# 26. Password trick
```html
<input type='text' id=test />
<script>
var str = ''; 
test.onkeypress = function(event){
	str = str + event.key; // get symbol
	this.value += String.fromCharCode(getRnd(65,122));
	return false;          // cancel put symbol to input
}
function getRnd(min,max){
	return Math.floor(Math.random() * (max-min))+min;
}
</script>
```

# 27. Keyboard arrows moving block
```html
<style>
*{margin:0;}
#block{
	width: 50px;
	height: 50px;
	background: orange;
	position: absolute;
}
</style>
<div id=block></div>
<script>
var left = 0;
var top1 = 0;
document.onkeydown = function(event){ // no onkeypress cuz onkeypress not detect arrows
	if(event.key == 'ArrowRight'){
		block.style.left = left + 'px';
		left++;
	}
	if(event.key == 'ArrowDown'){
		block.style.top = top1 + 'px';
		top1++;
	}
}
document.onkeyup = function(event){
	console.log('inpress key');
}
</script>
```

# 28. Mouse wheel event
```html
<style>
#test{
	width: 600px;
	height: 100px;
	background: yellow;
	margin: 10px;
	position: relative;
}
#test2{
	width: 10px;
	height: 100px;
	background: blue;
	position: absolute;
	left: 290px;
	top: 0;
}
</style>
<p>Direction: <span id=line></span></p>
<p>Speed: <span id=speed></span></p>
<div id=test>
	<div id=test2></div>
</div>
<script>
document.onwheel = function(event){
	if (event.deltaY > 0){ line.innerHTML = 'down'; }
	else                 { line.innerHTML = 'up'; }
	var speed_ = event.deltaY;
	speed_ = Math.abs(speed_);
	if     (speed_ < 100) {speed.innerHTML = 'low'}
	else if(speed_ < 150) {speed.innerHTML =	'middle'}
	else                 {speed.innerHTML = 'high'}
}
var left = 290;
test.onwheel = function(event){
	var line = event.deltaY;
	left = left + 0.2*line;  // 0.2*  for reduce speed
	test2.style.left = left + 'px';
	return false; // cancel vertical page wheeling
}
</script>
```

# 29. Smooth scroll to top
```html
<style>
.text{ width: 50px; }
#top1{
	position: fixed;
	right: 30px;
	bottom: 30px;
}
</style>
<p class=text>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
<button id=top1>Top</button>
<script>
window.onload = function(){              // alternative to <script src='' defer>
	var scrolled;
	var timer;
	top1.onclick = function(){
		scrolled = window.pageYOffset;   // return current scroll coord
		//window.scrollTo(0,0);
		scrollToTop();
	}
	function scrollToTop(){
		if(scrolled>0){
			window.scrollTo(0,scrolled);
			scrolled = scrolled - 100;   // 100 - speed of scroll
			timer = setTimeout(scrollToTop, 100);
		}
		else {
			clearTimeout(timer);
			window.scrollTo(0,0);
		}
	}
}
</script>
```

# 31. App - Tic-tac-toe
```html
<style>
#game{
	width: 150px;
	height: 150px;
	background: orange;
}
.block{
	width: 50px;
	height: 50px;
	float: left;
	border: 1px solid white;
	box-sizing: border-box;  /*fit border to in element*/
	line-height: 50px;
	text-align: center;
	font-size: 40px;
}
</style>
<div id=game></div>
<script>
window.onload = function(){
	for(let i = 0; i < 9; i++){
		game.innerHTML += '<div class=block></div>'
	}
	var hod = 0;
	game.onclick = function(event){
		if(event.target.className == 'block'){
			if(hod%2 == 0){
				event.target.innerHTML = 'X';
			}
			else {event.target.innerHTML = '0';}
			hod++;
			checkWinner();
		}
	}
	function checkWinner(){
		var ab = [...document.querySelectorAll('.block')];
		if (ab[0].innerHTML=='X' && ab[1].innerHTML=='X' && ab[2].innerHTML=='X'){alert('X win!')}
		else if (ab[3].innerHTML=='X' && ab[4].innerHTML=='X' && ab[5].innerHTML=='X'){alert('X win!')}
		else if (ab[6].innerHTML=='X' && ab[7].innerHTML=='X' && ab[8].innerHTML=='X'){alert('X win!')}
		else if (ab[0].innerHTML=='X' && ab[3].innerHTML=='X' && ab[6].innerHTML=='X'){alert('X win!')}
		else if (ab[1].innerHTML=='X' && ab[4].innerHTML=='X' && ab[7].innerHTML=='X'){alert('X win!')}
		else if (ab[2].innerHTML=='X' && ab[5].innerHTML=='X' && ab[8].innerHTML=='X'){alert('X win!')}
		else if (ab[0].innerHTML=='X' && ab[4].innerHTML=='X' && ab[8].innerHTML=='X'){alert('X win!')}
		else if (ab[2].innerHTML=='X' && ab[4].innerHTML=='X' && ab[6].innerHTML=='X'){alert('X win!')}
		//
		else if (ab[0].innerHTML=='0' && ab[1].innerHTML=='0' && ab[2].innerHTML=='0'){alert('0 win!')}
		else if (ab[3].innerHTML=='0' && ab[4].innerHTML=='0' && ab[5].innerHTML=='0'){alert('0 win!')}
		else if (ab[6].innerHTML=='0' && ab[7].innerHTML=='0' && ab[8].innerHTML=='0'){alert('0 win!')}
		else if (ab[0].innerHTML=='0' && ab[3].innerHTML=='0' && ab[6].innerHTML=='0'){alert('0 win!')}
		else if (ab[1].innerHTML=='0' && ab[4].innerHTML=='0' && ab[7].innerHTML=='0'){alert('0 win!')}
		else if (ab[2].innerHTML=='0' && ab[5].innerHTML=='0' && ab[8].innerHTML=='0'){alert('0 win!')}
		else if (ab[0].innerHTML=='0' && ab[4].innerHTML=='0' && ab[8].innerHTML=='0'){alert('0 win!')}
		else if (ab[2].innerHTML=='0' && ab[4].innerHTML=='0' && ab[6].innerHTML=='0'){alert('0 win!')}
	}
}
</script>
```

# 32. LocalStorage
```html
<button id=green>Green</button>
<button id=red>Red</button>
<script>
window.onload = function(){
	if(localStorage.getItem('mybgcolor')!== null){
		var color = localStorage.getItem('mybgcolor');
		document.body.style.background = color;
	}
	green.onclick = function(){
		document.body.style.background = 'green';
		localStorage.setItem('mybgcolor','green'); // values only strings
	}
	red.onclick = function(){
		document.body.style.background = 'red';
		localStorage.setItem('mybgcolor','red'); // values only strings
	}
}
</script>
```

# 34. Adaptive menu with js
```html
<style>
*{margin:0;padding:0;box-sizing:border-box;}
#menu{
	width: 250px;
	height: 100px;
	background: grey;
	position: fixed;
	left: -230px;
	top: 0;
	transition: all ease 1s;
}
</style>
<div id=menu>
<ul>
	<li>Item 1</li>
	<li>Item 2</li>
	<li>Item 3</li>
</ul>
</div>
<script>
window.onload = function(){
	menu.onmouseover = menuShow;
	menu.onmouseout = menuHide;
	document.onkeydown = function(event){
		if(event.code==='KeyM') menuShow();
		if(event.code==='Escape') menuHide();
	}
	function menuShow(){
		menu.style.left = 0;
	}
	function menuHide(){
		menu.style.left = '-230px';
	}
}
</script>
```

# 35. App - Clock with js
```html
<style>
*{margin:0;padding:0;box-sizing:border-box;}
.s0 { fill: #ff0000;stroke: #ff0000 }
.s1 { fill: #0000ff;stroke: #0000ff }
#clock{
	width:700px;
	height: 700px;
	border: 1px solid brown;
	position: relative;
}
#sec, #min{
	display:block;
	position: absolute;
	left: 200px;
	top: 0;
	/*transition: all ease 500ms;*/
}
</style>
<div id=clock>
<svg id=minute version='1.2' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 300 700' width='300' height='700'><path id='Layer 1' class='s1' d='m136 53h29v325h-29z' /></svg>
<svg id=second version='1.2' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 300 700' width='300' height='700'><path id='Shape 1' class='s0' d='m147 92h7v305h-7z' /></svg>
</div>
<script>
window.onload = function(){
	setInterval(fSec, 1000);
	var sec = 0;
	var min = 0;
	
	function fSec(){
		second.style.transform = 'rotate('+sec+'deg)';
		minute.style.transform = 'rotate('+min+'deg)';
		if(sec+6 == 366) {
			sec = 0;
			min +=6;
		}
		sec+=6;
	}
}
</script>
```

# 36. Tabs
```html
<style>
*{margin:0;padding:0;box-sizing:border-box;}
.tabs{
	width: 600px;
	margin: 50px auto;
}
.tab-h{
	display: inline-block;
	padding: 5px;
	line-height: 30px;
	border: 1px solid black;
	text-align: center;
	cursor: pointer;
}
.tab-b{
	display: none;
	padding: 20px;
	border: 1px solid black;
}
.tabs-body{
    position: relative;
    top: -1px;
    z-index: 1;
}
.tabs-header{
    position: relative;
    z-index: 2;
}
.active{
	border-bottom: 1px solid white;
}
</style>
<div class=tabs>
	<div class=tabs-header>
		<div class='tab-h active' data-tab='0'>One</div>
		<div class=tab-h data-tab='1'>Two</div>
		<div class=tab-h data-tab='2'>Three</div>
	</div>
	<div class=tabs-body>
		<div class=tab-b style='display:block;'>Text one</div>
		<div class=tab-b>Text two</div>
		<div class=tab-b>Text three</div>
	</div>
</div>
<script>
window.onload = function(){
	document.querySelector('.tabs-header').addEventListener('click', fTabs);
	function fTabs(event){
		if(event.target.className = 'tab-h'){
			var dataTab = event.target.dataset.tab;
			var tabH = document.querySelectorAll('.tab-h')
			for(let i = 0; i < tabH.length; i++){
				tabH[i].classList.remove('active');
			}
			event.target.classList.add('active');
			var tabBody = document.querySelectorAll('.tab-b');
			for(let i = 0; i < tabBody.length; i++){
				if(dataTab == i) tabBody[i].style.display = 'block';
				else tabBody[i].style.display = 'none';
			}
		}
	}
}
</script>
```

# 37. Columns height equalify
```html
<style>
*{margin:0;padding:0;box-sizing:border-box;}
#left, #right{
	float: left;
	width: 30%;
}
#left{ background: coral; }
#right{ background: orange; }
</style>
<div id=left>
	Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
	Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
</div>
<div id=right>
	Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
</div>
<script>
window.onload = function(){
	equalHeight();
	function equalHeight(){
	    left.style.height = 'auto';
		right.style.height = 'auto';
		var leftH = left.offsetHeight;
		var rightH = right.offsetHeight;
		var max = Math.max(leftH, rightH);
		left.style.height = max+'px';
		right.style.height = max+'px';
	}
	
	window.onresize = equalHeight;
}
</script>
```

# 38. Detect Desktop and Mobile
```html
<p id=out></p>
<script>
window.onload = function(){
	if(navigator.userAgent.match('iPhone') || navigator.userAgent.match('Android')){
		console.log('Mobile');
	}
	else console.log('Desktop');
	
}
</script>
```

# 39. Scroll effect layers
```html
<style>
*{margin:0;padding:0;box-sizing:border-box;}
#jlehmann{
	width: 500px;
	height: 200px;
	border: 5px solid black;
	position: relative;
	overflow: hidden;
}
.red{background:red;z-index:50;}
.blue{background:blue;z-index:49;}
.yellow{background:yellow;z-index:48;}
.layer{
	width: 100%;
	height: 100%;
	position: absolute;
	left: 0;
	top: 0;
}
</style>
<div id=jlehmann>
	<div class='layer red'></div>
	<div class='layer blue'></div>
	<div class='layer yellow'></div>
</div>
<script>
window.onload = function(){
	var mas = document.querySelectorAll('.layer');
	var j = 0;
	var y = 0;
	// onscroll vs onmousewheel ?
	jlehmann.onmousewheel = function(event){
        y = y - Math.round(event.deltaY);
        if(j !== mas.length-1){ // cancel yellow block scrolling
            if (j===0 && y>0){  // blocking red block to scroll down
                y=0
            } 
            else {
                mas[j].style.top = y*0.4 + 'px';
            }
            //jlehmann.onmousewheel = null;
        }
        else if (event.deltaY < 0){
            y = 1;
        }
        console.log(event.deltaY + ' y:' + y + ' j:' + j);
		if(-(y*0.4) >= 200){
			j++; y=0;
		}
        else if(-1*(y*0.4)< 0 && j>0){
            j--;
            y = y*0.4 - 500; 
        }
	}
}
//200px / 5000 = 0.4   // 5000 imaged digit, 200px is height from styles
</script>
```
