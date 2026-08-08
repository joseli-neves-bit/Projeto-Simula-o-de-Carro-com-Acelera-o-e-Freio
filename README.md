# Projeto: Simulação de Carro com Aceleração e Freio

Este projeto foi desenvolvido no ambiente de programação da Khan Academy (ProcessingJS).  
Ele demonstra conceitos de **movimento com vetores**, incluindo aceleração, velocidade e posição,  
além de controles de teclado para acelerar, frear e impedir que o carro ande para trás.

## Conceitos aplicados
- Uso de `PVector` para representar posição, velocidade e aceleração.
- Aceleração positiva (seta →) para mover o carro.
- Freio com aceleração negativa (seta ←) para desacelerar.
- Verificação para impedir velocidade negativa (não andar para trás).
- Limite de velocidade máxima com `velocity.limit()`.

## Como executar
var Car = function() {
    this.position = new PVector(width/2, height/2);
    this.velocity = new PVector(0, 0);
    this.acceleration = new PVector(0, 0);
};

Car.prototype.update = function() {
    this.velocity.add(this.acceleration);
    this.velocity.limit(10);

    // 🚫 Não deixar ir para trás
    if (this.velocity.x < 0) {
        this.velocity.x = 0;
    }

    this.position.add(this.velocity);
};

Car.prototype.display = function() {
    stroke(0);
    strokeWeight(2);
    fill(255, 0, 0);
    rect(this.position.x-52, this.position.y-59, 60, 60);
    rect(this.position.x-74, this.position.y-30, 100, 31);
    fill(92, 92, 92);
    ellipse(this.position.x, this.position.y, 30, 26);
    ellipse(this.position.x-50, this.position.y, 30, 30);
};

Car.prototype.checkEdges = function() {
    if (this.position.x > width) {
        this.position.x = 0;
    } 
    else if (this.position.x < 0) {
        this.position.x = width;
    }
};

var car = new Car();

draw = function() {
    background(255, 255, 255);

    // Controle da aceleração
    if (keyIsPressed && keyCode === RIGHT) {
        car.acceleration.set(0.05, 0);   // acelera para a direita
    } else if (keyIsPressed && keyCode === LEFT) {
        car.acceleration.set(-0.05, 0);  // freia
    } else {
        car.acceleration.set(0, 0);      // sem aceleração
    }

    car.update();
    car.checkEdges();
    car.display(); 
};

