# Exame Final Paradigmas de Programação - ELC117
Nome: Stéfano Camargo Squarcieri
Curso: Sistemas de informação


O objetivo é entregar melhorias no jogo e/ou no código, garantindo que o projeto esteja refinado e funcional.

## Reorganização das Battlescreens

> No projeto original (https://github.com/elc117/game-2023b-coloniarpg) já tinha duas classes que compartilhavam de propriedades semelhantes mas eram separadas, na minha entrega eu criei mais duas, essas classes foram reduzidas pra GenericBattleScreen.java e BattleState.java :
---
 **GenericBattleScreen.java** : Gerência das telas e dos parâmetros das batalhas

 **BattleState.java**: Dados do estado da batalha 

Ta, a classe BattleState guarda a vida do jogador/inimigo e o indexpergunta é a posicao da pergunta do quiz. E a GenericBattleScreen da o render nos assets e botoes da tela e chama as tela de vitoria/derrota. Pra criar um novo nivel agora so parametrizar as texturas , antes tinha que criar uma classe nova e fica chamando assets e bem dizer toda battlescreen ficava sendo duplicada.

### Tela Vitória/Derrota :

Antes, o projeto usava uma classe única chamada TextScreen, que exibia mensagens de vitória ou derrota, com base em boolean (dead). A motivo pra criar as screens Victory/Defeat foi a adição da recompensa na  tela de vitória que mostra o item ganho (um orb especifico), e uma tela de derrota. Da p considerar um refinamento visual tbm, ja que antes era mais simples a tela.

#### QuestionScreen1:
As perguntas e respostas ficavam tudo na mesma classe, entao separei em QuestionRepository as perguntas, alternativas e respostas. O metódo de transiçao da tela tava duplicado sendo que fazia a mesma coisa, onde o metodo startScreenBattleTransition unificou o startScreenBattleTransition1 e startScreenBattleTransition2. Tava meio que uma bola de neve se quisesse criar outra batalha tinha que copiar a classe inventar mais um startScreenBattle3Transition e com as questoes junto só essa classe tava gigante.

```java

// ANTES
private void startScreenBattle1Transition() {
    BattleScreen1 battleScreenInstance = new BattleScreen1(game);
    fadeScreen = new FadeScreen(game, fadeOut, this, battleScreenInstance);
    game.setScreen(fadeScreen);
}

private void startScreenBattle2Transition() {
    BattleScreen2 battleScreenInstance = new BattleScreen2(game);
    fadeScreen = new FadeScreen(game, fadeOut, this, battleScreenInstance);
    game.setScreen(fadeScreen);
}
```
Atualizado :
```java
private void startScreenBattleTransition(Screen nextScreen) {
    fadeScreen = new FadeScreen(game, fadeOut, this, nextScreen);
    game.setScreen(fadeScreen);
}
```
