
Fornece **comunicação lógica fim-a-fim entre processos de aplicações**, acima da rede, por meio de conexões lógicas entre pares de processos. Os protocolos usados são **TCP** e **UDP** (fim-a-fim).

## UDP

- Formato do Segmento: Porta de Origem + Porta de Destino + Comprimento do cabeçalho e Check-Sum (cabeçalho + dados);
- Faz multiplexação e demultiplexação (assim como o TCP).

## TCP

- Formato do Segmento: Porta de Origem + Porta de Destino + Número de sequência + Número de reconhecimento + ACK + SYN + FIN + Janela de Recepção;
- Número de Sequência: 1° byte de dados;
- Número de reconhecimento: próximo número ESPERADO quando ACK ativo;
- ACK: bit de controle (flag) do cabeçalho - indica que o valor do campo Número de reconhecimento é válido (usado pra analisar até que ponto os dados chegaram);
- SYN: bit de controle usado pra iniciar uma conexão TCP - importante pra sincronizar os números de sequência entre cliente e servidor;
- FIN: bit de controle usado pra encerrar uma conexão TCP(sem mais dados a serem enviados);
- Janela de Recepção: informa o buffer disponível no receptor, usado pra controle de fluxo (nunca será enviado uma quantidade de dados maior do que o receptor diz poder receber);
- Faz multiplexação e demultiplexação.

#### Multiplexação e Demultiplexação

##### Multiplexação

**No emissor**:

- Várias aplicações/processos estão rodando no mesmo host (ex.: navegador, cliente de e-mail, jogo online).
    
- Cada aplicação é identificada por um **número de porta** (ex.: HTTP → 80, HTTPS → 443, SMTP → 25).
    
- A **camada de transporte (TCP/UDP)** recebe dados de todos esses processos e **“multiplexa”** (combina) dentro de segmentos TCP/UDP, adicionando o cabeçalho com **porta de origem** e **porta de destino**.
    
- Depois, entrega para a camada de rede (IP), que só vê “um pacote IP” sem saber de qual processo veio.

##### Demultiplexação

**No receptor**:

- A camada de rede (IP) entrega os pacotes para a **camada de transporte**.
    
- O TCP/UDP olha os **números de porta de destino** no cabeçalho.
    
- Com base neles, entrega os dados ao **processo correto** (socket certo).

Analogia simples:

- Multiplexação é como **colocar cartas diferentes em envelopes com remetente/destinatário escritos** e levar todas juntas ao correio.
    
- Demultiplexação é o **carteiro olhar o endereço** de cada envelope e entregar para a **pessoa certa** dentro da casa.

### Reconhecimento e Retransmissão

- Quaisquer erros ou perdas no meio do caminho, será feita a retransmissão dos dados, com descarte de um dos segmentos enviados(duplicado) - 3-way handshake
- ![[Pasted image 20250827181835.png]]
- No caso acima, após o ack = 100, seria esperado o ack = 120 (seg=100 + 20 bytes de dados), mas como houve um problema, todos os outros segmentos são enviados com ack = 100(problema), até que o segmento (seq = 100, 20 bytes) seja novamente enviado para que tudo volte a funcionar.

#### Técnicas de Controle de Retransmissão

- Stop-and-Wait: a cada segmento transmitido aguarda-se uma confimação; o próximo segmento só é transmitido após a confirmação do segmento anterior;
- Go-back-N: uma sequência de segmentos podem ser enviados, sem nenhuma confirmação, até um valor LIMITE; caso haja um pedido de retransmissão de um segmento, este e os próximos transmitidos após este, serão todos retransmitidos;
- Selective-repeat: também permite o envio de uma sequência de segmentos até um valor limite; mas somente o segmento com problemas será retransmitido.

#### Controle de Fluxo

- Identificar a quantidade de dados que podem ser transmitidos sem a recepção de uma confirmação;
- Após o esgotamento do tamanho da janela, o remetente interrompe o envio de dados e aguarda a chegada de uma confirmação, para assim poder reiniciar o envio de dados.

#### Controle de Congestionamento

- Evitar que um ponto específico fique congestionado;
- A camada de rede (camada 3) não fornece nenhuma informação explícita à camada de transporte (camada 4), com relação ao congestionamento;
- Os sistemas finais percebem o problema observando o comportamento da rede (atrasos e perdas de pacotes).
- Papel do TCP: se o remetente perceber que há pouco congestionamento, o tráfego é aumentado (aumenta o tamanho da janela); o contrário é realizado também (redução da taxa de envio).
##### Técnicas de Controle de Congestionamento

- Partida Lenta: a taxa de envio TCP se inicia lenta, mas cresce exponencialmente (1MSS -> 2MSS -> 4MSS);
- Prevenção de Congestionamento: processo similar à partida lenta, mas ao invés de exponencial, o valor é incrementado ao atingir um valor limite de partida lenta (problema);
- Recuperação Rápida: utilizada quando um ACK duplicado é reconhecido - o valor é incrementado a cada ACK duplicado recebido no segmento perdido.





