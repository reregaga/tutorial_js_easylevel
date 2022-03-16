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
<p><input type='radio' name='fruit' value='яблоки'> Яблоки</p>
  <p><input type='radio' name='fruit' value='груши'> Груши</p>
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
