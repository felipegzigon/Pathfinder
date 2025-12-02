# Guia de Teste do Projeto

Bem-vindo ao PathFinder!  
Este documento apresenta tudo o que você precisa saber para **testar o jogo**, incluindo movimento, inimigo, colisões, vitória, game over e easter egg.

---

## Como Executar o Projeto

1. Abra o **Godot 4.x**.
2. Carregue o projeto normalmente.
3. Execute a cena principal `Main.tscn` (ícone de play).

---

## Controles do Jogador

O player só pode se mover seguindo as conexões definidas no grafo.

**Setas do teclado:**

- ⬆️ Cima  
- ⬇️ Baixo  
- ⬅️ Esquerda  
- ➡️ Direita  

O movimento é suave e animado conforme a direção.

---

## Marcadores (Waypoints)

- Todos os pontos de movimentação são nós **Marker2D** dentro de `Waypoints`.
- O jogador só pode se mover para vizinhos conectados no grafo definido em **GraphManager.gd**.
- Marcadores intermediários (com “a” ou “b”) criam curvas automáticas.

---

## Inimigo – Como Funciona

### Movimento Padrão — DFS Aleatório
- Explora caminhos ainda não visitados.
- Faz backtracking quando chega em becos sem saída.
- Usa animação: **anim_dfs**

### Perseguição — BFS
Ativada quando:
- O player está a **até 2 marcadores de distância**.

Comportamento:
- Velocidade reduzida para 50%.
- Calcula o **menor caminho** até o player.
- Usa animação: **anim_bfs**

### Respawn
Quando o player leva dano:
- O inimigo respawna em um marcador aleatório (com probabilidades diferentes).

---

## Sistema de Vida

O jogador possui:

- **2 pontos de vida**

Colidir com o inimigo:
- −1 de vida  
- Ativa invencibilidade de 1 segundo  
- Inimigo respawna  

### Game Over
Quando a vida chega a 0:
- Tela de Game Over aparece  
- Após 2 segundos o jogo reinicia  

---

## Condição de Vitória

Alcançar o **Marker28** exibe a tela de vitória e pausa o jogo.

---


## Tela Inicial

Contém:

- **Título do Jogo**
- Botão **Jogar** → vai para `Main.tscn`
- Botão **Sair** → fecha o jogo

---

## Arquivos Principais

| Arquivo | Função |
|--------|--------|
| `MainMenu.tscn` | Tela inicial |
| `Main.tscn` | Cena principal |
| `Player.gd` | Movimento, vida e interações |
| `Enemy.gd` | DFS, BFS, perseguição e respawn |
| `GraphManager.gd` | Grafo e conexões |
| `Waypoints/` | Marcadores do mapa |

---

## Como Testar

### 1. Player
- Movimentar pelas setas.
- Verificar curvas automáticas em intermediários.

### 2. Inimigo
- Checar exploração por DFS.
- Confirmar backtracking.

### 3. Perseguição
- Aproximar-se do inimigo por 2 marcadores.

### 4. Vida e Colisão
- Tocar o inimigo → perder vida e ver respawn.

### 5. Vitória
- Ir até Marker28.

### 6. Easter Egg
- Ir até Marker47.

---

## Fim

Você agora tem tudo para testar o projeto por completo!
