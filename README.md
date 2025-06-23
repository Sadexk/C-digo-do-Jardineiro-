// Definindo variáveis globais
let jardineiro;
let plantas =  [];
let temperatura = 10;
let totalArvores = 0;


function setup() {
  createCanvas(600, 400);
  jardineiro = new Jardineiro(width / 2, height - 50);
}


function draw() {
  
  // Usando map() para ajustar a cor de fundo de forma mais controlada
  let corFundo = lerpColor(color(217, 112, 26), color(219, 239, 208),
                            map(totalArvores, 0, 100, 0, 1));
  background(corFundo);
  
  mostrarInformacoes();
  
 temperatura += 0.1;
  
  jardineiro.atualizar();
  jardineiro.mostrar();
  
  // Verificar se o jogo acabou 
  verificarFimDeJogo();
  
  // Usando map() para aplicar o comportamento de árvores plantadas
  plantas.map((arvore) => arvore.mostrar());
}

// Função para mostrar as informações na tela
function mostrarInformacoes() {
  textSize(26);
  fill(0);
  text("Temperatura: " + temperatura.toFixed(2), 10, 30);
  text("Árvores plantadas: " + totalArvores, 10, 50);
  text("Para movimentar o personagem use as setas do teclado." , 10, 80);
}

// Função para verif🌳icar se o jogo acabou
 function verificarFimDeJogo() {
  if (totalArvores > temperatura){
    mostrarMensagemDeVitoria();
  } else if (temperatura > 50) {
    mostrarMensagemDeDerrota();
  }
 }

// Função para mostrar a mensagem de vitoria
function mostrarMensagemDeVitoria() {
  textSize(20);
  fill(0, 0, 0);
  text("🎉 Você venceu! Você plantou muitas árvores!", 100, 200);
  noLoop();
}

// Função para mostrar a mensagem de derrota
function mostrarMensagemDeDerrota() {
  textSize(20);
  fill(0, 0, 0);
  text("😢 Você perdeu!  A temperatura está muito alta. ", 100, 200);
  noLoop();
}

// Classe que cria o jardineiro
class Jardineiro {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.emoji ='👨‍🌾';
    this.velocidade = 3;
  }
  
  // Função para atualizar a posição do jardineiro
  atualizar() {
    if (keyIsDown(LEFT_ARROW)) {
      this.x -= this.velocidade;
    }
    if (keyIsDown(RIGHT_ARROW)) {
      this.x += this.velocidade;
    }
    if (keyIsDown(UP_ARROW)) {
      this.y -= this.velocidade;
    }
    if (keyIsDown(DOWN_ARROW)) {
      this.y += this.velocidade;
    }
  }
  
  // Função para desenhar o jardineiro na tela
  mostrar() {
    textSize(32);
    text(this.emoji, this.x, this.y);
  }
}

// Função para criar e plantar uma árvore
function keyPressed() {
  if (key === ' ' || key === 'p') {
    let arvore = new Arvore(jardineiro.x, jardineiro.y);
    plantas.push(arvore);
    totalArvores++;
    temperatura -= 3;
    if (temperatura < 0) teperatura = 0;
  }
}

// Classe que cria a árvore
class Arvore{
  contructor(x, y){
    this.x = x;
    this.y = y;
    this.emoji = '🌳';
  }
  
  //Função para desenhar a árvore na tela
  mostrar() {
    textSize(32);
    text(this.emoji, this.x, this.y);
  }
}
     
   

