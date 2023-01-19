# PONG
Pong com Alura
//variaveis bolinha
let xBolinha = 300;
let yBolinha = 200;
let diametro = 15;
let raio = diametro / 2;

//variaveis velocidade da bolinha/raquete
let velocidadeXBolinha = 6 ;
let velocidadeYBolinha = 6 ;
let raqueteComprimento = 10;
let raqueteAltura = 90;

//variaveis raquete
let xRaquete = 5;
let yRaquete = 150;

//variaveis raquete oponente
let XRaqueteOponente = 585 ;
let YRaqueteOponente = 150 ;
let velocidadeYOponente;
let velocidadeXOponente;

//placar do jogo
let meusPontos = 0;
let pontosOponente = 0;

let colisa = false;

//sons do jogo
let raquetada;
let ponto;
let trilha;

function setup() {
  createCanvas(600, 400) ;
} 

function draw() {
  background(0) ;
  mostraBolinha();
  movimentaBolinha();
  verificaBolinha();
  mostraRaquete(xRaquete,yRaquete);  
  movimentaMinhaRaquete()
  //verificaColisaoRaquete();
  //verificaColisaoRaquete();  
  verificaColisaoRaqueteBiblioteca(xRaquete, yRaquete);
  mostraRaquete(XRaqueteOponente, YRaqueteOponente );
  movimentaRaqueteOponente();
  verificaColisaoRaqueteBiblioteca(XRaqueteOponente, YRaqueteOponente);
  incluiPontos();
  marcaPontos();
  
  }
  function mostraBolinha(){
     circle(xBolinha, yBolinha, diametro) ;
  }
  function movimentaBolinha(){
    xBolinha += velocidadeXBolinha ;
    yBolinha += velocidadeYBolinha ;
  
  }
  function verificaBolinha (){
    if (xBolinha + raio > width || xBolinha - raio < 0){
    velocidadeXBolinha *= -1 ;
  }
  if (yBolinha + raio > height || yBolinha - raio < 0){
    velocidadeYBolinha *= -1 ;
  }
  } 
   function mostraRaquete(x, y){
     rect(x, y, raqueteComprimento, raqueteAltura);
   }
    function mostraRaqueteOponente(){
     rect(xRaqueteOponente, yRaqueteOponente, raqueteComprimento, raqueteAltura);
    }
   function movimentaMinhaRaquete(){
     if(keyIsDown(UP_ARROW)){
       yRaquete -= 10;
     }
      if(keyIsDown(DOWN_ARROW)){
       yRaquete += 10;
   }
   }
    function verificaColisaoRaquete(){      
      if(xBolinha - raio < xRaquete + raqueteComprimento &&  yBolinha - raio < yRaquete + raqueteAltura && yBolinha + raio >  yRaquete){
        velocidadeXBolinha *= -1;
      }
    }
    function verificaColisaoRaqueteBiblioteca(x, y){
      colisa = collideRectCircle(x, y, raqueteComprimento, raqueteAltura, xBolinha, yBolinha, raio);
      if(colisa){
        velocidadeXBolinha *= -1;
      }
      
    }
    function movimentaRaqueteOponente(){
      velocidadeYOponente = yBolinha -YRaqueteOponente -raqueteComprimento / 2 - 30;
      YRaqueteOponente += velocidadeYOponente;
      
    }
    function incluiPontos(){
      stroke(255);
      textAlign(CENTER);
      textSize(16);
      fill(color(255,140,0));
      rect(150,10,40,20);                
      fill(255);
      text(meusPontos, 170, 26);
      fill(color(255, 140, 0));
      rect(450, 10, 40, 20);
      fill(255);
      text(pontosOponente, 470, 26);
    }
   function marcaPontos(){
     if(xBolinha > 590){
       meusPontos += 1;
     }
     if(xBolinha < 10){
       pontosOponente += 1;
     }
   }
    
