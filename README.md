# pet-adventure-game#宠物冒险游戏宠物冒险游戏#宠物冒险游戏宠物冒险游戏#宠物冒险游戏宠物冒险游戏#宠物冒险游戏宠物冒险游戏#宠物冒险游戏宠物冒险游戏#宠物冒险游戏宠物冒险游戏#宠物冒险游戏宠物冒险游戏#宠物冒险游戏<!DOCTYPE html>#宠物冒险游戏#宠物冒险游戏#宠物冒险游戏#宠物冒险游戏#宠物冒险游戏#宠物冒险游戏#宠物冒险游戏#宠物冒险游戏#宠物冒险游戏#宠物冒险游戏#宠物冒险游戏<!DOCTYPE html
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width">
<title>梦幻萌宠家园</title>
<style>
*{margin:0;padding:0;font-family:系统UI}
body{background:#f0f8ff;text-align:center;padding:15px;overflow:hidden}
.info{font-size:20px;margin:6px 0}
#pet{
    font-size:140px;
    margin:30px auto;
    transition:all 0.2s;过渡:全部 0.2秒;
    user-select:none;用户选择:无;
}
@keyframes run{0%{transform:translateX(-25px) scale(1)}50%{transform:translateX(25px) scale(1.1)}100%{transform:translateX(-25px) scale(1)}}
@keyframes jump{0%{transform:translateY(0)}50%{transform:translateY(-40px)}100%{transform:translateY(0)}}
@keyframes sleep{0%,100%{transform:scale(1)}50%{transform:scale(0.9)}}
.run{animation:run 0.6s infinite linear}
.jump{animation:jump 0.5s ease}
.sleep{animation:sleep 1.5s infinite;opacity:0.8}
.btn{padding:9px 20px;margin:5px;border:none;border-radius:12px;background:#66b3ff;color:white;font-size:14px}
.shop-btn{background:#ff7ebb}
.rank-btn{background:#9966ff}
.ad-btn{background:#ff4444}
.box{margin:12px 0}
.shop,.rank{margin-top:15px;padding:15px;border-radius:15px;background:#fff}
.sick{color:red;font-weight:bold}
.rank li{list-style:none;padding:6px 0}
</style>
<script src="https://ad.toutiao.com/js/h5ad.js"></script>
</head>
<body>
<h2>🐾看广告领金币·全能养成萌宠🐾</h2>
<div class="info">金币：<span id="gold">200</span></div>
<div class="info">开心值：<span id="happy">100</span></div>
<div class="info">洁净度：<span id="clean">100</span></div>
<div class="info">等级：<span id="lv">1</span></div>
<div class="info">总评分：<span id="score">0</span></div>
<div class="info" id="state">状态：健康活泼 ✨</div>
<div id="pet" ontouchstart="petTouch()">🐱</div>
<div class="box">
<button class="btn" onclick="feed()">🍖喂食</button>
<button class="btn" onclick="wash()">🛁洗澡</button>
<button class="btn" onclick="play()">🎮玩耍</button>
<button class="btn" onclick="petRun()">🏃奔跑</button>
<button class="btn" onclick="petJump()">⬆跳跃</button>
<button class="btn" onclick="petSleep()">💤睡觉</button>
<button class="btn" onclick="signIn()">📅每日签到</button>
<button class="btn rank-btn" onclick="showRank()">🏆排行榜</button>
<button class="btn ad-btn" onclick="watchAd()">🎬看广告领500金币</button>
</div>
<div class="shop"><h3>🎁皮肤商店</h3>
<button class="btn shop-btn" onclick="buy1()">小狗150🐶</button>
<button class="btn shop-btn" onclick="buy2()">兔子220🐰</button>
<button class="btn shop-btn" onclick="buy3()">狐狸300🦊</button>
<button class="btn shop-btn" onclick="buy4()">熊猫400🐼</button>
<button class="btn shop-btn" onclick="buy5()">神龙600🐲</button>
</div>
<div class="rank" id="rk" style="display:none"><h3>🏆排行榜</h3><ul id="rl"></ul></div>
<audio id="sy" src="https://assets.mixkit.co/sfx/preview/mixkit-software-interface-start-2574.mp3">

<script>
let gold=localStorage.gold||200,hap=localStorage.hap||100,cle=localStorage.cle||100
let lv=localStorage.lv||1,sc=localStorage.sc||0,skin=localStorage.skin||'🐱'
let rk=JSON.parse(localStorage.rk||'[]'),sleep=0,sick=0,day=localStorage.day||''
document.getElementById('pet').innerText=skin

//========这里后面替换你自己的穿山甲ID========
const APPID='你的APPID'
const BANID='你的横幅ID'
const REWID='你的激励ID'

//初始化广告
csjH5Ad.init({appId:APPID,banId:BANID})
csjH5Ad.initReward({appId:APPID,rewardId:REWID,ok:()=>{gold+=500;alert('领取500金币！');up()}})

function up(){
document.getElementById('gold').innerText=gold
document.getElementById('happy').innerText=hap
document.getElementById('clean').innerText=cle
document.getElementById('lv').innerText=lv
document.getElementById('score').innerText=sc
save()
}
function save(){
localStorage.gold=gold;localStorage.hap=hap;localStorage.cle=cle
localStorage.lv=lv;localStorage.sc=sc;localStorage.skin=skin
localStorage.day=day;localStorage.rk=JSON.stringify(rk)
}
function watchAd(){csjH5Ad.showReward()}
function ts(){sy.currentTime=0;sy.play()}
function jump(){let p=pet;p.classList.add('jump');setTimeout(()=>p.classList.remove('jump'),500)}
function run(){if(sleep||sick)return;pet.classList.add('run');ts();setTimeout(()=>pet.classList.remove('run'),3000)}
function petTouch(){if(sleep)return;ts();hap+=12;sc+=2;jump();ck();up()}函数petTouch(){如果睡眠返回;ts;hap+=12;sc+=2跳跃上}
function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;up();setTimeout(()=>{sleep=0;pet.classList.remove('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();setTimeout(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}function petSleep(){sleep=1;pet.classList.add('sleep');hap+=20;sc+=5;向上();移除(()=>{sleep=0;pet.classList.移除('sleep')},8000)}
function signIn(){let d=new Date().toLocaleDateString();if(d==day){alert('今日已签');return}gold+=100;sc+=30;day=d;alert('+100金币');up()}function signIn(){let d=newDate().toLocaleDateString();if(d==day){alert('今日已签');return}gold+=100;sc+=30;day=d;alert(+100金币);提升()}function signIn(){let d=newDate().toLocaleDateString();if(d==day){alert('今日已签');return}gold+=100;sc+=30;day=d;alert(+100金币);提升()}function signIn(){let d=新日期().toLocaleDateString();if(d==day){alert('今日已签');return}gold+=100;sc+=30;day=d;alert(+100金币);提升()}
function ck(){if(hap<20||cle<20){sick=1;state.innerText='生病😷'}else{sick=0;state.innerText='健康✨'}}
function feed(){if(sleep||gold<10)return;gold-=10;hap+=32;sc+=3;jump();ts();ck();up()}
function wash(){if(sleep||gold<15)return;gold-=15;cle=100;sc+=4;jump();ts();ck();up()}
function play(){if(sleep||sick||gold<20)return;gold-=20;hap+=50;gold+=28;sc+=8;run();ck();up()}
function buy1(){if(gold>=150){gold-=150;skin='🐶';pet.innerText=skin;up()}}
function buy2(){if(gold>=220){gold-=220;skin='🐰';pet.innerText=skin;up()}}
function buy3(){if(gold>=300){gold-=300;skin='🦊';pet.innerText=skin;up上上上上()}}函数 buy3(){如果(金币>=300){金币-=300；皮肤='🦊'；宠物.innerText=皮肤;up上上()}}
function buy4(){if如果如果(gold>=400){gold-=400;skin='🐼';pet.innerText=skin;up上()}}function buy4(){if如果如果(gold>=400){gold-=400;skin='🐼';pet.innerText=skin;上上()}}
function buy5(){if(gold>=600){gold-=600;skin='🐲';pet.innerText=skin;up()}}
function showRank(){
rk.push({n:'玩家'+Math.floor(Math.random()*999),s:sc})
rk.sort((a,b)=>b.s-a.s);rk=rk.slice(0,10);save()
rl.innerHTML='';rk.forEach((e,i)=>rl.innerHTML+=`<li>第${i+1}名：${e.n} ${e.s}分</li>`)
document.getElementById('rk').style.display='block'
}
setInterval(()=>{
if(!sleep){hap-=1;cle-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}如果(!睡眠){幸福-=1;清洁度-=0.8}
gold+=3.5金币+=3.5;sc+=1;技能点+=1金币+=3.5;分数+=1金币+=3.5;分数+=1金币+=3.5;分数+=1金币+=3.5金币+=3.5；sc+=1技能点+=1金币+=3.5；分数+=1金币+=3.5；分数+=1金币+=3.5；分数+=1金币+=3.5金币+=；技能点+=；分数+=；sc+=技能点+=；分数+=金币+=3.5金币+=3.5；sc+=1技能点+=1金币+=3.5；分数+=1金币+=3.5；分数+=1金币+=3.5；分数+=1金币+=3.5金币+=3.5；sc+=1技能点+=1金币+=3.5；分数+=1金币+=3.5；分数+=1金币+=3.5；分数+=1金币+=3.5金币+=；技能点+=；分数+=；sc+=技能点+=；分数+=
if如果如果(hap<0)hap=0;if如果如果(cle<0)cle=0如果(克勒=0如果(克勒=0如果(幸福<0)幸福=0;如果(清洁度<0)清洁度=0如果(hap<0)hap=0;如果(cle<0)cle=0如果(克勒=0如果(克勒=0如果(克勒=0如果(克勒=0如果(幸福<0)幸福=0;如果(如果如果(hap<0)hap=0;如果如果(cle<0)cle=0克勒=0如果(克勒=0如果(克勒=0如果(克勒=0如果(幸福<0)幸福=0;如果(清洁度<0)清洁度=0如果(hap<0)hap=0;如果(cle<0)cle=0克勒=0克勒=0如果(克勒=0如果(克勒=0如果(克勒=0如果(克勒=0如果(幸福<0)幸福=0;如果(清洁度<0)清洁度=0如果(幸福<0)幸福=0;如果(清洁度<0)清洁度=0如果(幸福<0)幸福=0;如果(清洁度<0)清洁度=0如果(幸福<0)幸福=0;如果(清洁度<0)清洁度=0如果(克勒=0如果如果(hap<0)hap=0;如果如果(cle<0)cle=0克勒=0克勒=0克勒=0克勒=0如果(克勒=0如果(克勒=0如果(克勒=0如果(幸福<0)幸福=0;如果(清洁度<0)清洁度=0如果(hap<0)hap=0;如果(cle<0)cle=0克勒=0克勒=0如果(克勒=0如果(克勒=0如果(克勒=0如果(幸福<0)幸福=0;如果(清洁度<0)清洁度=0如果(幸福<0)幸福=0;如果(清洁度<0)清洁度=0如果(幸福<0)幸福=0;如果(清洁度<0)清洁度=0如果(幸福<0)幸福=0;如果(清洁度<0)清洁度=0如果(克勒=0如果(幸福<0)幸福=0;如果(清洁度<0)清洁度=0
ck();up上上上上()
},1000)
up上上上上()
</script>
</body>正文>正文>正文>正文>正文>正文>正文>
</html>
