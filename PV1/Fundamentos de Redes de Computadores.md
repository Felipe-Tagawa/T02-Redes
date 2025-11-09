
# Modelo OSI - Padronização de funcionalidades de Rede

- Define funcionalidades a serem desenvolvidas, agrupadas em *camadas*.
- Permitiu uma possibilidade de uso de IPv4 até os dias de hoje. 
- Camadas(funcionalidades):
- 1. Física
- 2. Enlace
- 3. Rede
- 4. Transporte
- 5. Sessão
- 6. Apresentação
- 7. Aplicação

#### Física

Interfaces, sinalização(conexão), meios de transporte

#### Enlace

Controle de acesso ao meio, endereço físico, controle de erros ponto a ponto

#### Rede

Conectividade e seleção de caminhos (roteamento), endereçamento lógico(IP)

#### Transporte

Gerência de conexões fim-a-fim (circuitos visuais), confiabilidade fim-a-fim, controle de fluxo

#### Sessão

Gerência de diálogos entre aplicativos

#### Apresentação

Formatação e sintaxe dos dados, criptografia e compressão

#### Aplicação

Serviços de rede para as aplicações

## Pilha TCP/IP

- A ideia é fornecer uma transmissão confiável dos dados para qualquer destino da rede, sob quaisquer circunstâncias.
- Tornou-se o padrão no qual se baseou a Internet
- Pilha de *protocolos* que irão implementar o modelo OSI

![[Pasted image 20250813181335.png]]

#### Modelo OSI x Pilha TCP/IP

![[Pasted image 20250813181721.png]]

#### Encapsulamento e Desencapsulamento

![[Pasted image 20250813181946.png]]

- Interação entre camadas iguais(de diferentes dispositivos)

### Arquitetura de aplicações de Rede

#### Arquiteturas cliente-servidor

- Há sempre um servidor que atende a requisições dos clientes
- Ex.: Serviços web e serviços de e-mail

#### Arquiteturas Peer-to-Peer(P2P)

- Duas máquinas trocando informações(pares - dispositivos finais), sem passar por nenhum servidor
- Ex.: troca de arquivos - BitTorrent e telefonia pela Internet - Skype

Um processo envia mensagens para a rede e recebe mensagens da rede através de uma interface de software denominada *socket* - interface entre a camada de aplicação e a camada de transporte ou também denominada API(application programming interface) entre uma aplicação e a rede.


### Identificadores de Portas (16 bits)

- Porta origem(16 bits) x destino(16 bits)
#### Classificação: 
- Portas bem conhecidas (0 a 1023 - serviços e aplicações)
- Portas registradas (1024 a 49151) - aplicações específicas (solicitada por uma entidade)
- Portas dinâmicas ou privadas (49152 a 65535) - de forma geral atribuídas dinamicamente pelo sistema operacional do cliente e utilizadas para identificar a aplicação do cliente durante a comunicação.

### Serviços de Transporte disponíveis

#### Transferência confiável de dados

- Deve garantir que os dados enviados por um processo origem sejam transmitidos correta e completamente para o processo destino.
- Quando um protocolo de transporte oferece esse serviço, o processo remetente passa seus dados para um socket e confia que eles serão entregues corretamente ao processo destinatário.
- Pode não ser necessário para aplicações tolerantes à perda, tais como aplicações multimídia.

#### Vazão

- Taxa pela qual o processo remetente pode enviar bits ao processo destinatário, podendo oscilar com o tempo.
- Aplicações sensíveis à largura de banda , tais como algumas aplicações multimídia, necessitam de uma vazão mínima garantida.
- Aplicações elásticas, tais como correio eletrônico, transferência de arquivos e transferências Web, podem fazer uso de qualquer quantidade disponível.

#### Transferência

- Aplicações interativas em tempo real, como a telefonia por internet, ambientes virtuais, teleconferências e jogos, exigem restrições de temporização no envio de dados para garantir eficácia.
- Para aplicações que não são em tempo real, é sempre preferível um atraso menor a um maior, mas não há nenhuma limitação estrita aos atrasos fim a fim.

#### Segurança

- Um protocolo de transporte pode, além do sigilo, fornecer outros serviços de segurança aos dados trocados entre os processos origem e destino, incluindo integridade dos dados e autenticação do ponto terminal.

### Protocolos de Transporte

#### TCP (Transmission Control Protocol)

- Protocolo orientado para conexão com um serviço confiável de transferência de dados.
- Serviço Orientado a Conexão: o TCP faz com que o cliente e o servidor troquem informações de controle de camada de transporte antes que as mensagens da camada de aplicação comecem a fluir.
- Serviço Confiável de Transporte: os processos comunicantes contam com o TCP para a entrega de todos os dados enviados sem erros e na ordem correta ao processo destino, com um mecanismo de controle de congestionamento, que limita a capacidade de transmissão de um processo(mais pesado)

#### UDP (User Data Protocol)

- Protocolo *NÃO* orientado para conexão com um serviço não confiável de transmissão de informações.
- Protocolo simplificado e leve (maior velocidade e menor segurança)
- Não há seguranças de que a mensagem chegue ao processo receptor e podem chegar fora de ordem
- Sem mecanismos de congestionamento