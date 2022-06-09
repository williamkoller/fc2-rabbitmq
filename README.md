# Sobre o RabbitMQ

- Message Broker

- Implementa AMQP, MQTT, STOMP e HTTP

- Desenvolvido em Erlang

- Desacoplamento entre services

- Rapido e poderoso (as mensagens por default cai na memoria)

- Default de mercado

## Por baixo dos panos

<p align="center">
  <img src="imgs/por-baixo-dos-panos.png">
</p>

## Funcionamento Basico

<p align="center">
  <img src="imgs/fundamentos-basicos.png">
</p>

 ### Tipos de Exchange

- Direct

- Fanout (todas as filas que estao relacionadas a essa exchange)

- Topic

- Headers (menos utilizados)

#### Exemplos

### Direct Exchange

<p align="center">
  <img src="imgs/direct-exchange.png">
</p>

- BIND (processo de relacionar exchange cm a fila)

- Routing key (marca o exchange como X e a routing key X vai para fila X)

### Fanout Exchange

<p align="center">
  <img src="imgs/fanout-exchange.png">
</p>

### Topic Exchange

<p align="center">
  <img src="imgs/topic.png">
</p>

## Queues

- FIFO, First In, First Out

- Propriedades:
  - Durable: Se ela deve ser salva mesmo depois do restart do broker
  - Auto-delete: Removida automaticamente quando o consumer se desconecta
  - Expiry: Define o tempo que nao ha mensagens ou clientes
  - Message TTL: tempo de vida da mensagem
  - Overflow:
    - Drop head (remova a ultima)
    - Reject publish
  - Exclusive: Somente channel que criou piode acessar
  - Max Length ou bytes: Quantidade de mensagens o tamanho dem butes maximo permitido


## Dead letter queues

- Algumas mensagens nao conseguem ser entregues por qualquer motivo

- Sao encaminhadas para uma exchange especifica que roteia as mensagens para uma dead letter queue

- Tais mensagens podem ser consumidas e averiguadas posteriormente

## Lazy Queues

- Mensagens sao armazenadas em disco

- Exige alto I/O

- Quando ha milhoes de mensagem em uma fila, por qualquer motivo, ha a possibilidade de liberar a memoria, jogando especificamente as mensagens em questao em disco


#### Direct Exchange

<p align="center">
  <img src="imgs/direct.png">
</p>


#### Fanout Exchange

<p align="center">
  <img src="imgs/fanout.png">
</p>


#### Topic Exchange

<p align="center">
  <img src="imgs/topic-e.png">
</p>


## Confiabilidade

- Como garantir que as mensagens nao serao perdidas no meio do caminho?!
- Como garantir que as mensagens puderam ser processadas corretamente pelos consumidores?
- Recurssos do RabbitMQ pensados para resolver tais situacoes
  - Consumer acknowledgement
  - Publish confirm
  - Filas e mensagens duraveis e persistidas