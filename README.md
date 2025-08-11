# Sistemas-Discretos- Trabalho da disciplina de Sistemas Discretos - UFCG - Período 25.1

## Descrição 
O sistema modela uma torre com 5 salas ligadas em ciclo, onde um gato e um rato se movimentam livremente para salas vizinhas. Os movimentos do gato (controláveis) podem ser restringidos pelo supervisor, enquanto os movimentos do rato (não controláveis) ocorrem de forma espontânea. O objetivo é evitar que o gato entre na mesma sala que o rato, prevenindo colisões, garantindo que o sistema seja não bloqueante e mantendo a maior liberdade possível de movimento. O modelo e o supervisor devem ser implementados no Supremica.

### Contexto

O modelo foi desenvolvido no Supremica para representar o problema do gato e do rato em uma torre com 5 salas ligadas em ciclo. Foram criados dois autômatos:

### 1. Gato: 
Estados G1 a G5 representam a posição do gato, com eventos de movimentação Move_GatoE1 e Move_GatoD1 (movimentos controláveis para esquerda e direita).

### 2. Rato: 
Estados R1 a R5 representam a posição do rato, com eventos Move_RatoE1 e Move_RatoD (movimentos não controláveis).

As transições foram definidas de modo que cada evento move o personagem para a sala adjacente correspondente. As colisões (mesma sala para gato e rato) foram modeladas como estados perigosos e bloqueados pelo supervisor. O Supervisor foi então sintetizado para evitar essas colisões, mantendo o sistema não bloqueante e permitindo o máximo de liberdade possível.


- <img width="427" height="363" alt="Circuito do Gato e Rato" src="https://github.com/user-attachments/assets/a5c278f1-90d0-43dc-a86f-26134640ba8b" />

## Componentes do Sistema

O sistema é modelado no Supremica com três autômatos principais:

### 1. Gato
- **Estados:** G1, G2, G3, G4, G5 (representam a sala onde o gato está).
- **Eventos controláveis:** 
  - `Move_GatoD1` – movimenta o gato uma sala no sentido horário.
  - `Move_GatoE1` – movimenta o gato uma sala no sentido anti-horário.
- **Controle:** eventos do gato podem ser desabilitados pelo supervisor para evitar colisões.

### 2. Rato
- **Estados:** R1, R2, R3, R4, R5.
- **Eventos não controláveis:** 
  - `Move_RatoD` – movimenta o rato uma sala no sentido horário.
  - `Move_RatoE1` – movimenta o rato uma sala no sentido anti-horário.
- **Controle:** movimentos do rato não podem ser impedidos; ocorrem espontaneamente.

### 3. Supervisor
- **Função:** monitora os estados combinados de gato e rato.
- **Objetivo:** impedir que gato e rato ocupem a mesma sala (estado perigoso), garantindo:
  - **Segurança:** evitar colisões.
  - **Não bloqueio:** o sistema nunca entra em um estado sem eventos possíveis.
  - **Máxima permissividade:** restringir apenas o necessário.
 
## Eventos Controláveis

No contexto da supervisão no Supremica, **eventos controláveis** são aqueles que o supervisor pode permitir ou desabilitar, influenciando diretamente o comportamento do sistema.

### Eventos controláveis no sistema:
- `Move_GatoD1` → movimenta o gato uma sala no sentido horário.
- `Move_GatoE1` → movimenta o gato uma sala no sentido anti-horário.

### Função no sistema:
Esses eventos permitem que o supervisor impeça movimentos do gato que levariam a um estado perigoso (mesma sala que o rato).  
Por exemplo:
- Se o rato está na Sala 3 e o gato na Sala 2, o evento `Move_GatoD1` pode ser desabilitado para evitar colisão.
- O movimento oposto (`Move_GatoE1`) ainda pode ser permitido, garantindo que o sistema continue não bloqueante.

### Observação:
Os movimentos do **rato** (`Move_RatoD` e `Move_RatoE1`) são **não controláveis**, ou seja, o supervisor não pode impedir que aconteçam.

## Eventos Não Controláveis

No contexto da supervisão no Supremica, **eventos não controláveis** são aqueles que o supervisor **não pode impedir** de acontecer. Eles ocorrem espontaneamente no sistema, sem possibilidade de bloqueio direto.

### Eventos não controláveis no sistema:
- `Move_RatoD` → movimenta o rato uma sala no sentido horário.
- `Move_RatoE1` → movimenta o rato uma sala no sentido anti-horário.

### Função no sistema:
Esses eventos representam a movimentação livre e imprevisível do rato.  
O supervisor deve **antecipar** a possibilidade de colisões com base nessas movimentações, bloqueando previamente eventos controláveis do gato que possam levar a um estado perigoso.

### Observação:
Como não é possível impedir que o rato se mova, a lógica do supervisor precisa considerar **todos os caminhos possíveis** resultantes desses eventos para manter o sistema seguro e não bloqueante.

## Modelo Utilizado

O sistema foi modelado no **Supremica** por meio de **dois autômatos independentes**, representando os movimentos do gato e do rato.

### 1. Autômato do Gato
- **Estados:** G1, G2, G3, G4, G5 (cada estado representa a sala onde o gato se encontra).
- **Eventos:** 
  - `Move_GatoD1` (controlável) – movimenta o gato uma sala no sentido horário.
  - `Move_GatoE1` (controlável) – movimenta o gato uma sala no sentido anti-horário.
- **Características:** o supervisor pode habilitar ou desabilitar esses eventos para evitar colisões.

- <img width="427" height="363" alt="image" src="https://github.com/user-attachments/assets/576a6524-e27e-432e-bee6-19f95414700f" />


### 2. Autômato do Rato
- **Estados:** R1, R2, R3, R4, R5 (cada estado representa a sala onde o rato se encontra).
- **Eventos:** 
  - `Move_RatoD` (não controlável) – movimenta o rato uma sala no sentido horário.
  - `Move_RatoE1` (não controlável) – movimenta o rato uma sala no sentido anti-horário.
- **Características:** esses eventos ocorrem de forma espontânea, sem possibilidade de bloqueio pelo supervisor.
- <img width="427" height="363" alt="image" src="https://github.com/user-attachments/assets/e5eff9f9-39ef-4b35-9af5-f156c666b9f2" />


Os dois autômatos são combinados em um produto síncrono para representar todas as possíveis posições simultâneas de gato e rato.  
A partir desse modelo composto, o supervisor é sintetizado no Supremica para impedir que gato e rato ocupem a mesma sala, garantindo segurança, não bloqueio e máxima permissividade.

## Eventos do Sistema

| Evento         | Personagem | Direção          | Tipo              | Descrição |
|----------------|------------|------------------|-------------------|-----------|
| Move_GatoD1    | Gato       | Horário (direita) | Controlável       | Move o gato uma sala no sentido horário. |
| Move_GatoE1    | Gato       | Anti-horário (esquerda) | Controlável | Move o gato uma sala no sentido anti-horário. |
| Move_RatoD     | Rato       | Horário (direita) | Não controlável   | Move o rato uma sala no sentido horário. |
| Move_RatoE1    | Rato       | Anti-horário (esquerda) | Não controlável | Move o rato uma sala no sentido anti-horário. |






