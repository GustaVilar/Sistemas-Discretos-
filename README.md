# Sistemas-Discretos- Trabalho da disciplina de Sistemas Discretos - UFCG - Período 25.1

## Descrição 
O sistema modela uma torre com 5 salas ligadas em ciclo, onde um gato e um rato se movimentam livremente para salas vizinhas. Os movimentos do gato (controláveis) podem ser restringidos pelo supervisor, enquanto os movimentos do rato (não controláveis) ocorrem de forma espontânea. O objetivo é evitar que o gato entre na mesma sala que o rato, prevenindo colisões, garantindo que o sistema seja não bloqueante e mantendo a maior liberdade possível de movimento. O modelo e o supervisor devem ser implementados no Supremica.

### Contexto

O modelo foi desenvolvido no Supremica para representar o problema do gato e do rato em uma torre com 5 salas ligadas em ciclo. Foram criados dois autômatos:

Gato: estados G1 a G5 representam a posição do gato, com eventos de movimentação Move_GatoE1 e Move_GatoD1 (movimentos controláveis para esquerda e direita).

Rato: estados R1 a R5 representam a posição do rato, com eventos Move_RatoE1 e Move_RatoD (movimentos não controláveis).

As transições foram definidas de modo que cada evento move o personagem para a sala adjacente correspondente. As colisões (mesma sala para gato e rato) foram modeladas como estados perigosos e bloqueados pelo supervisor. O Supervisor foi então sintetizado para evitar essas colisões, mantendo o sistema não bloqueante e permitindo o máximo de liberdade possível.


<img width="1536" height="1024" alt="Circuito do Gato e Rato" src="https://github.com/user-attachments/assets/a5c278f1-90d0-43dc-a86f-26134640ba8b" />


