<template>
<div>
  <div class="container">
    <div class="col-span-12">
          <div class="col-span-12 w-full flex-col">
            <div id="myDocument" class="w-full h-full " style="background-color:white;position:relative;">
              <input type="text" id="cursorX" size="6"> X-position of the mouse cursor
              <br /><br />
              <input type="text" id="cursorY" size="6"> Y-position of the mouse cursor
              <img id="test" src="./test.jpg" style="width: 10%;"/>
            </div>
          </div>
    </div>
  </div>
</div>
</template>
<script>
import testImg from './test.jpg'
import testImg2 from './test2.jpg'
//The Window interface represents a window containing a DOM document; the document property points to the DOM document loaded in that window.
// window.onload = init;
//assigns the onload event to whatever is returned from the init function when it's executed. init will be executed immediately

// function init() {
// //window.event = Returns the current event, which is the event currently being handled by the JavaScript code's context, or undefined if no event is currently being handled.
// 	if (window.Event) {
// //https://developer.mozilla.org/en-US/docs/Web/API/Window/captureEvents
// //captures specified events occuring in the document window, in this case mousemove
// 	document.captureEvents(Event.MOUSEMOVE);
// 	}
// // then our function
// 	document.onmousemove = getCursorXY;
// }

// function addElement () {
//   // create a new div element
//   const newDiv = document.createElement("div");

//   // and give it some content
//   const newContent = document.createTextNode("Hi there and greetings!");

//   // add the text node to the newly created div
//   newDiv.appendChild(newContent);

//   // add the newly created element and its content into the DOM
//   const currentDiv = document.getElementBy("myDocument");
//   document.body.insertBefore(newDiv, currentDiv);
// }

// function getCursorXY(e) {
// 	document.getElementById('cursorX').value = (window.Event) ? e.pageX : event.clientX + (document.documentElement.scrollLeft ? document.documentElement.scrollLeft : document.body.scrollLeft);
// 	document.getElementById('cursorY').value = (window.Event) ? e.pageY : event.clientY + (document.documentElement.scrollTop ? document.documentElement.scrollTop : document.body.scrollTop);
//   this.cursorX = (window.Event) ? e.pageX : event.clientX + (document.documentElement.scrollLeft ? document.documentElement.scrollLeft : document.body.scrollLeft);
//   this.cursorY = (window.Event) ? e.pageY : event.clientY + (document.documentElement.scrollTop ? document.documentElement.scrollTop : document.body.scrollTop);

//   // create an element
//   // addElement();
// }



function getMouseCoords(e) {
  // var e = e || window.event;
  document.getElementById('container').innerHTML = e.clientX + ', ' +
    e.clientY + '<br>' + e.screenX + ', ' + e.screenY;
}


var followCursor = (function() {
  // make following rocket
  // var s = document.createElement('div');
  // s.style.position = 'absolute';
  // s.style.margin = '0';
  // s.style.padding = '5px';
  // s.style.border = '1px solid red';
  // s.textContent = "🚀"

  // var test = document.getElementById('test')
  // var div = document.createElement('div');
  var secondImg = document.createElement("img");
  secondImg.src = testImg2;
  secondImg.style.position = 'absolute';
  secondImg.style.margin = '0';
  secondImg.style.border = '2px solid blue';
  secondImg.style.height = '50%';
  secondImg.style.width = '25%';
  var test = document.createElement("img");
  test.src = testImg;
  test.style.position = 'absolute';
  test.style.margin = '0';
  test.style.border = '2px solid blue';
  test.style.height = '50%';
  test.style.width = '25%';
  // var src = document.getElementById("header");
  // src.appendChild(test);

  return {
    // append rocket div
    init: function() {
      // document.body.appendChild(s);
      document.body.appendChild(test);
      // document.getElementById('container').appendChild(test);

    },
    // make rocket follow
    run: function(e) {
      // var e = e || window.event;
      test.style.left = (e.clientX - 5) + 'px';
      test.style.top = (e.clientY - 5) + 'px';
      // s.style.left = (e.clientX - 5) + 'px';
      // s.style.top = (e.clientY - 5) + 'px';
      // console.log(e.clientX, e.clientY)
      if ( e.clientX % 3 != 0){
        // this code switches the image on mousemove
        test.src = testImg2;
      }
      else {
        test.src = testImg;
      }
      getMouseCoords(e);
    }
  };
}());

window.onload = function() {
  followCursor.init();
  document.body.onmousemove = followCursor.run;
}
//TODO: amandabraga.com body element > div with id of cursor inside is a div that is the circle. translate3d(x,y)
//TODO: body element > div with several divs with class "hidden" inside are the images we want to show on mouse move


export default {
  name: 'HomeRouter',
  props: {
    msg: String
  },
 data() {
  return {
    currentTab: 'first',
    none: false,
    cursorX:0,
    cursorY:0,
  }
 },
 methods: {
   handleClick(tab, event) {
     console.log(tab, event);
   }
 }
}
</script>

<style lang="scss" scoped>

/deep/ body {
  margin: 0 !important;
}

.container{
display: grid;
grid-template-columns: repeat(12, minmax(0, 1fr));
height: 100%;
width:100%;
margin:0;
justify-items: center;
overflow: auto;
}
/deep/.el-tabs__header{
  margin: 0;
}
/deep/.el-tabs__nav {
  float:none;
}
/deep/.el-tabs__active-bar{
  visibility: hidden;
}

/deep/.el-tabs__nav-wrap {
  color:white;
  background-color: black;
  justify-items:center;
}

/deep/.el-tabs__item.is-active {
  position: relative;
  color: white;
}

// /deep/.el-tabs__item.is-active::after {
//   position: absolute;
//   content: '';
//   width: 4rem;
//   height: 0.1rem;
//   top:2rem;
//   right:0.8rem;
//   background-color: white;
//   transition: all .3s;
// }

/deep/.el-tabs__item {
  color: #b7b7b7;
}
</style>
