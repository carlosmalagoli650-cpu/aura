
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Farmar Aura</title>
<style>
body{margin:0;background:#09091b;color:white;font-family:Arial;text-align:center}
h1{color:#c18aff;text-shadow:0 0 20px purple;font-size:38px}
.box{background:#191932;border:1px solid #754bba;border-radius:18px;padding:20px;margin:15px auto;max-width:600px}
button{background:#874cff;color:white;border:0;border-radius:12px;padding:14px;margin:7px;font-size:16px;font-weight:bold;cursor:pointer}
button:hover{filter:brightness(1.3)}
#orb{margin:25px auto;width:130px;height:130px;border-radius:50%;background:radial-gradient(white,#a64dff,#18052f);box-shadow:0 0 45px #a64dff;animation:pulse 2s infinite}
@keyframes pulse{50%{transform:scale(1.12);filter:hue-rotate(70deg)}}
.stat{display:inline-block;background:#242442;padding:12px;border-radius:10px;margin:5px}
#nome{font-size:25px;color:#c18aff;font-weight:bold}
</style>
</head>
<body>
<h1>✨ FARMAR AURA ✨</h1>
<div class="stat">⚡ Energia: <b id="energia">0</b></div>
<div class="stat">🪙 Moedas: <b id="moedas">0</b></div>
<div class="stat">💪 Multiplicador: x<b id="mult">1</b></div>
<div class="box">
<div id="orb"></div>
<div id="nome">Aura Básica</div>
<p id="descricao">Comece sua jornada!</p>
<button onclick="farmar()">⚡ FARMAR</button>
<p id="mensagem">Clique para ganhar energia!</p>
</div>
<div class="box">
<h2>🎲 Girar uma aura</h2>
<p>Custa 50 moedas por giro.</p>
<button onclick="girar()">GIRAR AURA</button>
</div>
<div class="box">
<h2>🛒 Melhorias</h2>
<p>Ganho por clique: <b id="ganho">1</b></p>
<button onclick="melhorar()">Comprar melhoria</button>
<p>Custo: <b id="custo">100</b> moedas</p>
</div>
<div class="box">
<h2>🌟 Renascimento</h2>
<p>Precisa de 5.000 de energia. Reinicia o progresso e aumenta seu multiplicador!</p>
<button onclick="renascer()">RENASCER</button>
<p>Renascimentos: <b id="renascimentos">0</b></p>
</div>
<div class="box">
<h2>🎒 Auras desbloqueadas</h2>
<p id="colecao">Aura Básica</p>
</div>
<script>
let energia=0,moedas=0,mult=1,ganho=1,custo=100,renascimentos=0;
let aura={nome:"Aura Básica",cor:"#b66aff",poder:1};
let colecao=["Aura Básica"];
const auras=[
 {nome:"Aura Básica",cor:"#b66aff",poder:1,peso:45},
 {nome:"Aura de Fogo",cor:"#ff542f",poder:2,peso:25},
 {nome:"Aura Elétrica",cor:"#4deaff",poder:4,peso:15},
 {nome:"Aura Cósmica",cor:"#e14dff",poder:8,peso:9},
 {nome:"Aura Divina",cor:"#ffe45c",poder:20,peso:5},
 {nome:"AURA SECRETA",cor:"#ff2ca8",poder:100,peso:1}
];
function atualizar(){
 document.getElementById("energia").textContent=Math.floor(energia).toLocaleString("pt-BR");
 document.getElementById("moedas").textContent=Math.floor(moedas).toLocaleString("pt-BR");
 document.getElementById("mult").textContent=mult;
 document.getElementById("ganho").textContent=ganho*mult*aura.poder;
 document.getElementById("custo").textContent=custo;
 document.getElementById("renascimentos").textContent=renascimentos;
 document.getElementById("colecao").textContent=colecao.join(" • ");
}
function farmar(){
 let n=ganho*mult*aura.poder;
 energia+=n;
 moedas+=Math.max(1,Math.floor(n/5));
 document.getElementById("mensagem").textContent="+"+n+" energia e moedas!";
 atualizar();
}
function girar(){
 if(moedas<50){document.getElementById("mensagem").textContent="Você precisa de 50 moedas!";return}
 moedas-=50;
 let total=auras.reduce((s,a)=>s+a.peso,0),r=Math.random()*total;
 let escolhida=auras[0];
 for(let a of auras){r-=a.peso;if(r<=0){escolhida=a;break}}
 aura=escolhida;
 if(!colecao.includes(aura.nome))colecao.push(aura.nome);
 document.getElementById("nome").textContent=aura.nome;
 document.getElementById("nome").style.color=aura.cor;
 document.getElementById("descricao").textContent="Poder da aura: x"+aura.poder;
 document.getElementById("orb").style.background="radial-gradient(white,"+aura.cor+",#09091b)";
 document.getElementById("orb").style.boxShadow="0 0 55px "+aura.cor;
 document.getElementById("mensagem").textContent="Você conseguiu "+aura.nome+"!";
 atualizar();
}
function melhorar(){
 if(moedas<custo){document.getElementById("mensagem").textContent="Moedas insuficientes!";return}
 moedas-=custo;ganho++;custo=Math.floor(custo*1.6);
 document.getElementById("mensagem").textContent="Melhoria comprada!";
 atualizar();
}
function renascer(){
 if(energia<5000){document.getElementById("mensagem").textContent="Precisa de 5.000 de energia!";return}
 energia=0;moedas=0;ganho=1;custo=100;renascimentos++;mult++;
 document.getElementById("mensagem").textContent="Renascimento realizado! Multiplicador aumentado!";
 atualizar();
}
atualizar();
</script>
</body>
</html>
