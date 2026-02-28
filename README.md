[index.html](https://github.com/user-attachments/files/25620837/index.html)
<html>
<head>
<title>Young Mi's Quarter of a Century</title>

<style>
body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 0;
    background: linear-gradient(to bottom, #dff6ff, #f4fff4);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    overflow: hidden;
}

h1 { margin-bottom: 10px; }

#countdown {
    font-size: 36px;
    margin-bottom: 20px;
}

#hiddenContent {
    display: none;
    font-size: 26px;
    color: #2e7d32;
    margin-top: 20px;
}

canvas {
    position: fixed;
    top: 0;
    left: 0;
    pointer-events: none;
}

/* Frog + Mouse positioning */
.frog-container { position: fixed; bottom: 0; left: 20px; }
.mouse-container { position: fixed; bottom: 0; right: 20px; }

/* Balloon float */
@keyframes float {
    0% { transform: translateY(0px); }
    50% { transform: translateY(-12px); }
    100% { transform: translateY(0px); }
}
.balloon { animation: float 3s ease-in-out infinite; }

/* Eye blink */
@keyframes blink {
    0%, 90%, 100% { transform: scaleY(1); }
    95% { transform: scaleY(0.1); }
}
.eye { animation: blink 4s infinite; }

/* Mouse nibble */
@keyframes nibble {
    0%,100% { transform: rotate(0deg); }
    50% { transform: rotate(-5deg); }
}
.mouse-head {
    transform-origin: 60% 60%;
    animation: nibble 1.5s infinite ease-in-out;
}

/* Frog jump */
@keyframes frogJump {
    0%   { transform: translateY(0); }
    30%  { transform: translateY(-120px); }
    50%  { transform: translateY(-150px); }
    70%  { transform: translateY(-120px); }
    100% { transform: translateY(0); }
}
.frog-jump { animation: frogJump 1s ease-out; }

/* Final screen */
#finalScreen {
    position: fixed;
    inset: 0;
    background: linear-gradient(to bottom, #fff0f6, #e0f7fa);
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 40px;
    font-size: 20px;
    line-height: 1.6;
    max-width: 900px;
    margin: auto;
    text-align: center;
    opacity: 0;
    pointer-events: none;
    transition: opacity 2s ease;
    z-index: 10;
}

/* Typewriter cursor */
#typewriter::after {
    content: "|";
    animation: blinkCursor 1s infinite;
}

@keyframes blinkCursor {
    0%,50%,100% { opacity: 1; }
    25%,75% { opacity: 0; }
}
</style>
</head>

<body>

<h1>Young Mi's Quarter of a Century</h1>
<div id="countdown"></div>
<div id="hiddenContent">🎉 It's 2AM AEST on March 2! Surprise unlocked! 🎆</div>

<canvas id="fireworks"></canvas>

<!-- Frog -->
<div class="frog-container">
<svg width="220" height="300" viewBox="0 0 220 300">
<g class="balloon">
<line x1="150" y1="60" x2="150" y2="160" stroke="#555" stroke-width="2"/>
<ellipse cx="150" cy="40" rx="35" ry="45" fill="#ff6b81"/>
<polygon points="145,85 155,85 150,95" fill="#ff6b81"/>
</g>
<ellipse cx="110" cy="200" rx="70" ry="60" fill="#66bb6a"/>
<ellipse cx="110" cy="215" rx="40" ry="35" fill="#a5d6a7"/>
<circle cx="80" cy="130" r="20" fill="#66bb6a"/>
<circle cx="140" cy="130" r="20" fill="#66bb6a"/>
<g class="eye">
<circle cx="80" cy="130" r="10" fill="white"/>
<circle cx="80" cy="130" r="5" fill="black"/>
</g>
<g class="eye">
<circle cx="140" cy="130" r="10" fill="white"/>
<circle cx="140" cy="130" r="5" fill="black"/>
</g>
<path d="M75 165 Q110 190 145 165" stroke="#2e7d32" stroke-width="4" fill="transparent"/>
</svg>
</div>

<!-- Mouse -->
<div class="mouse-container">
<svg width="220" height="200" viewBox="0 0 220 200">
<polygon points="120,140 190,120 190,170 120,170" fill="#ffd54f"/>
<ellipse cx="80" cy="150" rx="50" ry="35" fill="#b0bec5"/>
<g class="mouse-head">
<ellipse cx="110" cy="140" rx="30" ry="25" fill="#b0bec5"/>
<circle cx="120" cy="135" r="4" fill="black"/>
</g>
</svg>
</div>

<div id="finalScreen">
<h1 id="typewriter"></h1>
</div>

<script>
const targetDate = new Date("March 2, 2026 02:00:00 GMT+10:00").getTime();
const countdownElement = document.getElementById("countdown");
const hiddenContent = document.getElementById("hiddenContent");

const timer = setInterval(function() {
    const now = new Date().getTime();
    const distance = targetDate - now;

    if (distance <= 0) {
        clearInterval(timer);
        countdownElement.style.display = "none";
        hiddenContent.style.display = "block";
        startFireworks();

        setTimeout(() => {
            document.getElementById("finalScreen").style.opacity = "1";
            document.getElementById("finalScreen").style.pointerEvents = "auto";
            startTypewriter();
            makeFrogJump();
        }, 6000);

        return;
    }

    const days = Math.floor(distance / (1000*60*60*24));
    const hours = Math.floor((distance % (1000*60*60*24))/(1000*60*60));
    const minutes = Math.floor((distance % (1000*60*60))/(1000*60));
    const seconds = Math.floor((distance % (1000*60))/1000);

    countdownElement.innerHTML =
        days+"d "+hours+"h "+minutes+"m "+seconds+"s ";
},1000);

function makeFrogJump() {
    const frog = document.querySelector(".frog-container");
    frog.classList.add("frog-jump");
    setTimeout(()=> frog.classList.remove("frog-jump"),1000);
}

function startTypewriter() {
const message = `Happy birthday to my precious angel... 

Cakes and Candles Amy x  
Don't party too hard.

Yours,  
Weylin`;

const element = document.getElementById("typewriter");
let index=0;

function type(){
if(index<message.length){
const currentChar=message.charAt(index);
element.innerHTML+= currentChar === "\n" ? "<br><br>" : currentChar;
index++;

let delay=35;

if(message.substring(index-13,index).includes("Yours,")){ delay=120; }
if(message.substring(index-7,index).includes("Weylin")){ delay=200; }

setTimeout(type,delay);
}}
type();
}

function startFireworks(){
const canvas=document.getElementById("fireworks");
const ctx=canvas.getContext("2d");
canvas.width=window.innerWidth;
canvas.height=window.innerHeight;
let particles=[];

function createFirework(){
const x=Math.random()*canvas.width;
const y=Math.random()*canvas.height/2;
const color=`hsl(${Math.random()*360},100%,50%)`;
for(let i=0;i<80;i++){
particles.push({
x:x,y:y,
angle:Math.random()*2*Math.PI,
speed:Math.random()*5+2,
life:100,color:color
});}}

function update(){
ctx.fillStyle="rgba(0,0,0,0.15)";
ctx.fillRect(0,0,canvas.width,canvas.height);
particles.forEach((p,i)=>{
p.x+=Math.cos(p.angle)*p.speed;
p.y+=Math.sin(p.angle)*p.speed;
p.life--;
ctx.beginPath();
ctx.arc(p.x,p.y,2,0,Math.PI*2);
ctx.fillStyle=p.color;
ctx.fill();
if(p.life<=0){particles.splice(i,1);}
});
requestAnimationFrame(update);
}

setInterval(createFirework,700);
update();
}
</script>

</body>
</html>
