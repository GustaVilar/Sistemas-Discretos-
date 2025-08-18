# Sistemas-Discretos- Trabalho da disciplina de Sistemas Discretos - UFCG - Período 25.1

## Descrição 
O sistema modela uma torre com 5 salas ligadas em ciclo, onde um gato e um rato se movimentam livremente entre salas vizinhas. Os movimentos do gato são eventos controláveis, podendo ser restringidos pelo supervisor, enquanto os movimentos do rato são não controláveis e ocorrem de forma espontânea. Para permitir o controle do acesso entre salas, foram incluídas portas (nas passagens 1–2, 2–3, 3–4 e 4–5), representadas por autômatos com estados Aberta e Fechada. A passagem 5–1 permanece livre, garantindo que o sistema não fique bloqueado. Além disso, foi modelado um autômato de alternância, que organiza a sequência de movimentos entre gato e rato. O objetivo do supervisor é evitar colisões (gato e rato na mesma sala), utilizando as portas e a restrição dos movimentos do gato, de modo a garantir a não obstrução do sistema e manter a máxima liberdade possível.

### Contexto

O modelo desenvolvido no Supremica representa a movimentação de um gato e de um rato em uma torre com 5 salas conectadas em ciclo. Foram criados autômatos para o gato, para o rato e para as portas que controlam a passagem entre salas. 
O gato possui eventos controláveis
- <img width="427" height="363" alt="ChatGPT Image 16 de ago  de 2025, 19_18_17" src="https://github.com/user-attachments/assets/a8e9ad8e-141f-4aa2-b812-039c6e8e26e4" />


enquanto os movimentos do rato são não controláveis. 
- <img width="427" height="363" alt="ChatGPT Image 16 de ago  de 2025, 19_18_20" src="https://github.com/user-attachments/assets/5414a829-66a2-41ff-bf2d-a47b75d0b09c" />


O modelo foi criado para permitir a síntese de um supervisor que garanta duas propriedades principais:

Segurança – impedir colisões (evitar que gato e rato ocupem a mesma sala).

Não bloqueio – assegurar que o sistema continue sempre funcionando, com a máxima liberdade de movimento possível.




## Modelo do sistema

Para a resolução desse problema, foram criados os seguintes automatos:

1. Gato

Estados G1 a G5 representam a posição do gato. Os eventos de movimentação, como Gato_12, Gato_21, Gato_23, Gato_32, Gato_34, Gato_43, Gato_45, Gato_54, Gato_15 e Gato_51, correspondem às passagens entre salas vizinhas. Esses eventos são controláveis e podem ser restringidos pelo supervisor.

- <img width="427" height="363" alt="image" src="https://github.com/user-attachments/assets/0f5c72dd-71d2-432a-ae58-7ee12b492c36" />

2. Rato

Estados R1 a R5 representam a posição do rato. Os eventos de movimentação, como Rato_12, Rato_21, Rato_23, Rato_32, Rato_34, Rato_43, Rato_45, Rato_54, Rato_15 e Rato_51, ocorrem de forma espontânea e são não controláveis.

- <img width="427" height="363" alt="image" src="https://github.com/user-attachments/assets/db5b0b37-b13f-4436-8f14-fe18912f9d0e" />


3. Portas

Foram modelados quatro autômatos adicionais para as portas localizadas entre as salas 1–2, 2–3, 3–4 e 4–5. Cada porta possui dois estados, Aberta e Fechada, com eventos de controle Abrir_xy e Fechar_xy. Quando a porta está em Aberta, os eventos de passagem do gato e do rato associados àquela conexão (por exemplo, Gato_12, Rato_12, Gato_21, Rato_21 na Porta12) são permitidos; no estado Fechada, esses eventos são bloqueados. A passagem 5–1 permanece livre, garantindo que o sistema não fique bloqueado.

- <img width="427" height="363" alt="image" src="https://github.com/user-attachments/assets/d12498bd-d9ed-4a24-a3c7-e4a16514600d" />


As colisões (gato e rato na mesma sala) foram representadas como estados indesejados na especificação de segurança, sendo evitadas pelo supervisor. As portas foram modeladas na planta como restrições físicas ao deslocamento: quando estão fechadas, bloqueiam os eventos de passagem associados, tanto para o gato quanto para o rato. Dessa forma, o supervisor sintetizado no Supremica atua apenas desabilitando os movimentos do gato que levariam a colisões, enquanto as portas oferecem uma camada adicional de controle físico definida pelo ambiente. 


Essa imagem representa uma breve simulação do sistema modelado no Supremica. Nela, o gato e o rato se movimentam pelas salas conectadas em ciclo, passando pelas portas que regulam o acesso entre os ambientes. As setas destacadas ilustram os possíveis caminhos que cada personagem pode seguir durante a execução: o gato segue sua trajetória controlada, enquanto o rato realiza movimentos não controláveis. O objetivo do modelo é justamente evitar colisões (quando ambos estariam na mesma sala), garantindo segurança, não bloqueio do sistema e liberdade máxima de movimento.

<img src="https://github.com/user-attachments/assets/15be9c97-4786-44d0-840b-68505ef20110" alt="Simulação do sistema" width="400"/>



## Função no sistema:

### Eventos Controláveis

Os eventos do gato (Gato_xy) e os de abrir/fechar portas (Abrir_xy, Fechar_xy) são controláveis. Isso significa que o supervisor pode desabilitar um movimento do gato que levaria a um estado perigoso (mesma sala que o rato).

Por exemplo:

   - Se o rato está na Sala 3 e o gato na Sala 2, o evento Gato_23 pode ser desabilitado para evitar colisão.

   - O evento oposto (Gato_21) ainda pode ser permitido, garantindo que o sistema continue não bloqueante.

   - As portas também fazem parte da planta, mas seus estados (Aberta ou Fechada) afetam diretamente quais movimentos estão disponíveis.

### Eventos Não Controláveis

No contexto da supervisão no Supremica, eventos não controláveis são aqueles que o supervisor não pode impedir de acontecer. Eles ocorrem espontaneamente no sistema.

### Eventos não controláveis no sistema:

Rato_xy → movimentam o rato entre salas vizinhas (sentido horário ou anti-horário), quando a porta correspondente está aberta.



## Eventos do Sistema
Evento       | Personagem | Direção / Passagem      | Tipo            | Descrição
-------------|------------|-------------------------|-----------------|-------------------------------------------
Gato_xy      | Gato       | Entre salas x → y       | Controlável     | Movimento do gato entre salas vizinhas (ou 5–1 livre).
Rato_xy      | Rato       | Entre salas x → y       | Não controlável | Movimento espontâneo do rato entre salas vizinhas (ou 5–1 livre).
Abrir_xy     | Porta x–y  | —                       | Controlável     | Abre a porta entre as salas x e y.
Fechar_xy    | Porta x–y  | —                       | Controlável     | Fecha a porta entre as salas x e y.


## Condições finais do projeto
Com os testes de verificação do Supremica, ficou confirmado que:

- O Sistema é não bloqueante.
- O Sistema é livre de deadlock.

## Resultado final e explicação do modelo

[![Assista no YouTube](https://img.youtube.com/vi/G9lkIe-FZCE/hqdefault.jpg)](https://youtu.be/G9lkIe-FZCE)


## Considerações

Este projeto permitiu aplicar na prática os conceitos de autômatos finitos e da ferramenta Supremica em um problema de modelagem mais próximo de situações reais. A utilização de autômatos para representar o movimento do gato, do rato, das portas e da alternância demonstrou ser uma abordagem eficiente para aprofundar o entendimento sobre supervisão de eventos discretos.

Ao atribuir funções específicas a cada autômato, como o deslocamento do gato (eventos controláveis), os movimentos espontâneos do rato (eventos não controláveis) e o controle das portas, foi possível coordenar as interações do sistema de forma estruturada. O processo de síntese do supervisor mostrou como evitar colisões (estados indesejados) e, ao mesmo tempo, manter o sistema não bloqueante e com a máxima liberdade possível de movimento.

Além disso, o trabalho reforçou a importância de se distinguir entre eventos controláveis e não controláveis dentro do Supremica, mostrando como essa separação influencia diretamente nas estratégias de supervisão e na robustez do sistema.





