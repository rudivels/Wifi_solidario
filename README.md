# WIFI solidário
Rudi @ setembro 2020

Implementação de uma rede wifi num sítio na zona rural.

# Apresentação

Minhas pesquisas e ações de extensão na área de geração descentralizada de energia elétrica para comunidades distantes das redes de distribuição sempre me levaram a encarar novos desafios tecnológicos.
As grandes demandas dessas comunidades são água, iluminação, comunicação e geração de renda, e a energia elétrica é um serviço que pode ajudar a atender essas quatro principais demandas. 

Neste sítio em particular, a gente tinha implementado uma turbina hidrocinética na década de 1990 e este empreendimento deu origim a diversos projetos de pesquisa e extensão e de certa forma nos deu a possibilidade de testar vários estratégias de tecnologias sociais ou solidários [1]. 

O desafio neste caso, foi a necessidade extender uma rede de wifi de uma casa para outra casa numa distância de aproximadamente 800 metros. Entre as duas casas tem uma área cerrado nativo preservada ao longo do Rio Corrente e uma estrada de acesso.

Aparentemente um problema simples de resolver, nos colocou um interessante desafio tecnológico. Como estender um rede wifi para cobrir uma area rural, com o uso de tecnologias acessíveis no mercado, custo baixo, levando em consideração as limitações de disponibilidade de energia elétrica. 

Pois bem. Feito o desafio vamos buscar uma solução.

# Situação atual
Sem cobertura de celular. Mostrar link para mapa de cobertura da aneel, mostrando que o ponto de acesso com cobertura de celular está a 100 km. 
A única opção de serviço é telefone rural ou internet via satélite. Essa opção de internet via satélite está ficando um pouco mais acessível nos ultimos tempos a custos acessíveis, tornando o seu uso acessível. A grande vantagem disso é que permite o uso de whatsapp no smartphones, substituindo o uso de telefone convencional. 

A situação atual é uma assinatura de internet via satélite, uma antenna parabólica acoplada a um modem com uma saida Ethernet 10BaseT ligando um roteador comercial de Wifi disponibilizando acesso a rede internet.

Diagrama de bloco 
Satelite - modem - roteador - smartfone.
 
![](figuras/configuracao_atual.png)

A ligação entre o roteador pode ser representado usando o modelo de Camadas OSI, conforme o esquema abaixo, mostrando as camadas fisicas, enlace, rede e aplicação. 

| Camada    | Roteador          | Celular | 
|:---------:|:-----------------:|:-------:|
| Aplicação | Serviços internet | Serviços internet (Whatsapp)|
| Rede      | TCP/IP (DHCP)     | TCP IP dinâmico| 
| Enlace    | IEEE 802          | IEEE 802       |
| Física    | Radio 2.4 Ghz     | Radio 2.4 GHz  |  



## Opção 1 - extensão por meio de cabo de rede

Essa opção basicamente trabalho na camada física e de enlace.
Disponibilidades: o Roteador tem uma porta de saída RJ45 para cabo par transado 10base-T ou 100base-T.
Limitações: O cabo 10base-T permite uma extensão de 100 metros. 
Há algumas opções antigos de cabo de rede coaxial que permite maiores alcances, entretanto é uma tecnologia obsoleto e o cabo de rede coaixal é muito caro, além de precisar uma conversor cabo UTP para cabo coaxial.

| Camada    | Roteador          | Celular | 
|:---------:|:-----------------:|:-------:|
| Aplicação | Serviços internet | Serviços internet (Whatsapp)|
| Rede      | TCP/IP (DHCP)     | TCP IP dinâmico| 
| Enlace    | IEEE 802          | IEEE 802       |
| Física    | Cano de redeR     | Cabo de rede   |  

## Opção 2 - uso de repetidores da sinal de WiFi

Uma opção bastante interessante seria de usar repetidores de sinal de rádio que são equipamentos comercialmente disponíveis que permitem repetir o sinal de WiFi. 
O alcance convencional de WiFi é em torno de 30 metros quando não tem obstáculos entre o receptor e transmissor quando se usa antennas omnidirecional.
Existem diverso modelos de repetidores de sinal de WiFi disponível no mercado que tem um custo que varia de 100 a 300 R$, que basicamente são desenhados para funcionar em ambientes internos e que recebem numa antenna o sinal do roteador e depois repetem este sina (provavelmente em outro canal) por meio de uma outra antenna. 
Como estes repetidores são desenhados para ambientes internos eles são projetos para ser alimentados pela rede elétrica e tem antennas internas de baixo ganho. 

Poderia-se usar essa solução, mas um dos grandes impecilios é que serão necessários algumas repetidores para poder cubrir o trajeto de 800 metros. Além disso haverá a necessidade de alimentar estes repetidores no meio do caminho. Lembrando que o acesso a eletricidade é um das condições de contorno.

Solução Enlace - Fisica

| Camada    | Roteador          | Repetidor | Repetidor | Celular | 
|:---------:|:-----------------:|:---------:|:---------:|:--------|
| Aplicação | Serviços internet | | | Serviços internet |
| Rede      | TCP/IP (DHCP)     | | | TCP IP dinâmico| 
| Enlace | IEEE 802      | IEEE 802 |IEEE 802  | IEEE 802 |
| Física | Radio 2.4 GHz | Radio 2.4 GHz | Radio 2.4 GHz | Radio 2.4 GHz |

Essa solução seria bastante interessante se tivesse a necessidade de ter pontos de acesso no meio do caminho de uma casa até a outra. No nosso caso, por enquanto isso não é necessária.

## Opção 3 - uso de link de radio direcional e novo ponto de acesso

A opção 3 foco no otimizar o uso do canal de rádio WiFi e expandir seu alcance com algumas técnicas interessantes. 
Um levantamento bibliográfico mostrou que essa tecnologia já está sendo implemento em situações onde se precisa aumentar o alcance dos serviços de internet ou de intranet em áreas rurais ou a implementação de serviços comunitários de comunicação na zona rural.

A grande vantagem de usar essa tecnologia para essas aplicações é que ele não precisa de licenças específicas das autoridades de telecomunicações e pode ser implementado por qualquer pessoa, não necessitando de empresas de telecomunicações ou telefonia. 

Como ele usa o espectro de 2.4 GHz que já é liberado para estes fim, a tecnica consiste em melhor o alcance do radio enlace usando antennas direcionais em vez de antennas onmidirecional.

Teoricamente o alcance que se pode ter com essa tecnologia seria de até 3km. Este limite é imposto pelo protocolo IEEE 802 de controle de acesso ao meio físico e verificação de erros. Acontece que ao mandar um pacote de dados na camada de enlace o transmissor do dados espera receber do receptor um pacoto de dados confirmando a recepção do pacote. Se o transmissor não recebe o pacote num determinado periode de tempo, ele entende que o pacato foi perdido no meio do caminho e o transmissor re-envia o pacote.
A limitação consiste no tempo do pacote sair do transmissor até o receptor e o tempo de mandar a confirmação de recepção ACK pelo receptor. 
Este tempo limita o alcance de 3 km. Entretanto há meios de aumentar este tempo no protocolo e assim aumentar o alcance do radio enlace. O recorde de distância de transmissão atualmente é de uma radio enlace de visibilidade de com essa tecnologia em Venezuela de 382 km  [2].


Há de diversos relatos do uso dessa tecnologia em aplicações comunitárias. 

Essa solução pode ser representado pelas seguintes camadas Rede, Enlace e Física.


| Camada    | Roteador | Link direcional A | Link direcional B | Ponto de acesso | Celular |
|:---------:|:--------:|:---------:|:---------:|:--------:|:------:|:-----:|
| Aplicação | Serviços internet | | | | Serviços internet |
| Rede      | TCP/IP (DHCP)     |TCP IP fixo |TCP IP fixo | TCP IP DHCP | TCP IP dinâmico| 
| Enlace | IEEE 802      | IEEE 802 | IEEE 802  | IEEE 802 | IEEE 802 |
| Física | Radio 2.4 GHz | Radio 2.4 GHz | Radio 2.4 GHz | Radio 2.4 GHz| Radio 2.4 GHz |

O hardware para implementar a solução:



# Bibliografia

[1] Els RH van, Balduino LF, Henriques AMD, Campos C de O. Hydrokinetic turbine for isolated villages. PCH Notícias SHP News 2003;19:24–5.
[2] Pietrosemoli E. Setting Long Distance WiFi Records : Proofing Solutions for Rural Connectivity. J Community Informatics 2008;4:1–10.

