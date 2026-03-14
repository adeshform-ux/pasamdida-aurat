```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Birthday Surprise for Rupashree 🎂</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>

body{
margin:0;
font-family:Arial;
overflow:hidden;
background:#0a0a2a;
color:white;
text-align:center;
}

/* screens */

.screen{
position:absolute;
width:100%;
height:100vh;
display:flex;
justify-content:center;
align-items:center;
flex-direction:column;
transition:opacity 1s;
}

.hidden{
opacity:0;
pointer-events:none;
}

/* card */

.card{
background:white;
color:#ff4d6d;
padding:35px;
border-radius:20px;
box-shadow:0 10px 30px rgba(0,0,0,0.4);
max-width:420px;
}

button{
padding:12px 25px;
border:none;
border-radius:25px;
background:#ff4d6d;
color:white;
font-size:18px;
cursor:pointer;
margin-top:15px;
}

/* flower garden ground */

.garden{
position:absolute;
bottom:0;
width:100%;
height:200px;
background:linear-gradient(#2b8a3e,#1b5e20);
}

/* flowers */

.flower{
position:absolute;
font-size:25px;
animation:sway 3s infinite alternate;
}

@keyframes sway{
from{transform:rotate(-5deg)}
to{transform:rotate(5deg)}
}

/* butterflies */

.butterfly{
position:absolute;
font-size:28px;
cursor:pointer;
transition:transform 0.5s;
}

/* floating decorations */

.float{
position:absolute;
font-size:24px;
animation:rise 10s linear infinite;
}

@keyframes rise{
0%{transform:translateY(100vh)}
100%{transform:translateY(-10vh)}
}

/* cake */

.cake{
font-size:110px;
cursor:pointer;
}

/* hearts for mini game */

.heart{
position:absolute;
font-size:30px;
cursor:pointer;
}

</style>
</head>

<body>

<!-- loading -->

<div class="screen" id="loading">
<h2>✨ Preparing something magical... ✨</h2>
</div>

<!-- gift -->

<div class="screen hidden" id="gift">

<div class="card">

<h2>🎁 A Special Gift</h2>
<p>Someone made something special for you ❤️</p>

<button onclick="next('question')">Open Gift 🎁</button>

</div>

</div>

<!-- question -->

<div class="screen hidden" id="question">

<div class="card">

<h2>🥺 Hey Rupashree</h2>
<p>Before you see your surprise...</p>

<h3>Are you excited? 😍</h3>

<button onclick="next('garden')">YES 😍</button>
<button onclick="next('garden')">Maybe 🤭</button>

</div>

</div>

<!-- garden -->

<div class="screen hidden" id="garden">

<h1>🌸 Flower Garden 🌸</h1>

<div class="garden" id="gardenGround"></div>

<button onclick="next('birthday')">Continue 🌷</button>

</div>

<!-- birthday -->

<div class="screen hidden" id="birthday">

<div class="card">

<h1>🎉 Happy Birthday Rupashree 🎉</h1>

<div class="cake" id="cake">🕯️🎂</div>

<p>Blow the candle 🎂 (allow microphone)</p>

<p id="message"></p>

<button onclick="startGame()">Play Love Game 🎮</button>

</div>

</div>

<script>

/* loading */

setTimeout(()=>{
next("gift")
},2000)

function next(id){

document.querySelectorAll(".screen").forEach(s=>{
s.classList.add("hidden")
})

document.getElementById(id).classList.remove("hidden")

}

/* flower garden */

for(let i=0;i<25;i++){

let f=document.createElement("div")
f.className="flower"
f.innerHTML="🌸"
f.style.left=Math.random()*100+"vw"
f.style.bottom=Math.random()*150+"px"

document.getElementById("gardenGround").appendChild(f)

}

/* butterflies */

for(let i=0;i<5;i++){

let b=document.createElement("div")
b.className="butterfly"
b.innerHTML="🦋"
b.style.left=Math.random()*100+"vw"
b.style.top=Math.random()*60+"vh"

b.onclick=function(){
b.style.transform="scale(2) translateY(-200px)"
}

document.body.appendChild(b)

}

/* floating decorations */

let items=["❤️","✨","🌸","🎈"]

setInterval(()=>{

let el=document.createElement("div")
el.className="float"
el.innerHTML=items[Math.floor(Math.random()*items.length)]
el.style.left=Math.random()*100+"vw"

document.body.appendChild(el)

setTimeout(()=>el.remove(),10000)

},400)

/* typing message */

let text="You are one of the most special people in my life ❤️ May your day be filled with happiness 🌸 smiles 😊 love 💖 and beautiful memories ✨ Happy Birthday Rupashree 🎂🥳"

let i=0

function type(){

if(i<text.length){

document.getElementById("message").innerHTML+=text.charAt(i)

i++

setTimeout(type,40)

}

}

setTimeout(type,4000)

/* microphone candle blowing */

navigator.mediaDevices.getUserMedia({audio:true}).then(stream=>{

let audioContext=new AudioContext()
let mic=audioContext.createMediaStreamSource(stream)
let analyser=audioContext.createAnalyser()

mic.connect(analyser)

let data=new Uint8Array(analyser.frequencyBinCount)

function detect(){

analyser.getByteFrequencyData(data)

let volume=data.reduce((a,b)=>a+b)/data.length

if(volume>80){

document.getElementById("cake").innerHTML="🎂✨"
alert("🎉 Make a birthday wish Rupashree!")

}

requestAnimationFrame(detect)

}

detect()

})

/* mini love game */

function startGame(){

alert("Catch the hearts ❤️")

for(let i=0;i<10;i++){

let h=document.createElement("div")
h.className="heart"
h.innerHTML="❤️"

h.style.left=Math.random()*90+"vw"
h.style.top=Math.random()*80+"vh"

h.onclick=function(){
h.remove()
}

document.body.appendChild(h)

}

}

</script>

</body>
</html>
```
