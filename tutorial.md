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
