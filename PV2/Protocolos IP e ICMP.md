
# Protocolo IP


## IPv4

- Define um mecanismo de transmissão de datagramas (pacotes) do tipo "melhor esforço" - a tentativa de mandar de nó a nó de uma rede a outra é boa, mas não há garantia de entrega dos pacotes.
- Funciona no modo "Não orientado à conexão" e "não confiável".
- Vantagem: Possibilita a entrega(encaminhamento) de diferentes tipos de tráfego (voz, vídeo e dados), com o encapsulamento de diferentes protocolos das camadas 3 e 4 (superior); pode ser transportado por diferentes padrões de redes - permite ser encapsulado em diferentes protocolos da camada 2 (inferior).

### Datagrama IPv4

- Fragmentação: dividir os pacotes em subpacotes para chegar nos dados da camada 2 para que caiba dentro dos dados. Remontagem após chegar - não é feito por roteador(alto processamento).


- Versão (4bits);
- HLEN (header length - 4 bits dados em valores de 32 bits) - mín 20 bytes e máx 60 bytes;
- Tipo/Classe de Serviço (8bits) : indica a *Prioridade* dada ao datagrama IP durante a transmissão - tratamento de diferentes tipo de tráfego - configurado nos roteadores;
- Comprimento Total(16 bits) - comprimento total permitido para um pacote IP (cabeçalho + dados);
- Identificação (16 bits) - número designado pelo remetente para ajudar na remontagem de um datagrama segmentado;
- Flags (3bits) - dois últimos bits usados no *controle da fragmentação*;
- Deslocamento do fragmento (16 bits) - número de partes de 64 bits sem contar o cabeçalho, que estão contidos em fragmentos anteriores;
- Tempo de Vida(TTL) (8bits) - indica o número de saltos permitidos ao datagrama. A cada novo roteador, este campo é decrementado de '1', quando este valor chega a 0, o datagrama será descartado pelo roteador;
- Número de Protocolo (8bits): indica *qual o protocolo encapsulado no campo dados* (carga útil) do datagrama IP;
- Check-Sum do Cabeçalho (Soma de verificação do cabeçalho) (16 bits) - soma de verificações ocorrida no cabeçalho do datagrama, permitindo *detectar possíveis erros no cabeçalho* do datagrama recebido;
- Endereço IP de Origem (32 bits) - endereço IP do Host que *envia* o datagrama;
- Endereço IP de Destino (32 bits) - endereço IP do Host que *recebe* o datagrama;
- Opções (n bits) - campo opcional que pode ser utilizado para funções de *testes de rede e debug*;
- Dados (payload) - utilizado para *transporte de outros protolocos* (carga útil do datagrama IP).

## IPv6

- 128 bits;
- Cabeçalho mais simplificado que o IPv4 - reduz o tempo de processamento dos pacotes;
- Sem uso de NAT(IPv6 não tem endereços privados);
- Apresenta proteção e segurança próprias (IPSec);
- Realiza fragmentação e remontagem de pacotes apenas na origem e no destino;
- Sem endereço de broadcast.

### Datagrama IPv6

- Versão (4 bits) - identifica a versão do protocolo IPv6;
- Classe de Tráfego (8 bits) - identifica e diferencia os pacotes por classes de serviços ou prioridade. Ele continua provendo as funcionalidades e definições do campo Tipo de Serviço do IPv4;
- Rótulo de Fluxo (20 bits) - Identifica e diferencia pacotes de um mesmo fluxo na camada de rede - roteador consegue identificar o tipo de fluxo de cada pacote;
- Tamanho do Conteúdo (16 bits) - Indica o tamanho em bytes, apenas dos dados enviados juntos ao cabeçalho;
- Próximo Cabeçalho (8 bits) - Identifica o cabeçalho que se segue ao cabeçalho IPv6;
- Limite de Saltos (8 bits) - Indica o número máximo de roteadores que o pacote IPv6 pode passar antes de ser descartado, sendo decrementado a cada salto (idêntico ao TTL do IPv4);
- Endereço de Origem (128 bits) - Indica o endereço de origem do pacote;
- Endereço de Destino (128 bits) - Indica o endereço de destino do pacote.

#### Representação

- 128 bits, divididos em 8 campos de 16 bits cada
	- ##### Regras Permitidas
		- Utilizar caracteres maiúsculos ou minúsculos;
		- Omitir zeros à esquerda do campo;
		- Representar zeros contínuos por "::", uma única vez.
		![[Pasted image 20251015113502.png]]


#### Tipos de Endereço

- ##### Unicast
	- Utilizado para identificação de uma única interface na rede. Comunicação 1:1.
- ##### Anycast
	- Utilizado para identificar um grupo de interfaces, porém, com a propriedade de que um pacote enviado a um endereço anycast é encaminhado apenas à interface pertencente ao grupo, que esteja mais próxima da origem do pacote. Comunicação 1:1 de muitos.
- ##### Multicast
	- Utilizados para identificar um grupo de interfaces, sendo que cada uma pode pertencer a mais de um grupo. Os pacotes enviados para esses endereços são entregues a todas as interfaces que compõe o grupo. Comunicação 1:N.
- ##### Global Unicast
	- Equivalente ao endereço global unicast do IPv4;
	- É o endereço que será usado globalmente na Internet (Endereços IP públicos);
	- Prefixo 2000::/3 indica que se trata de um endereço global Unicast.
- ##### Link Local
	- Automaticamente configurado em qualquer Host IPv6, através da conjugação do seu prefixo FE80::/10.
	- Estes endereços são válidos somente na rede em que a interface se encontra conectada (não será roteada para outra).
#### Endereços Especiais

- ##### Loopback ::1/128
	- Equivalente ao endereço IPv4 loopback 127.0.0.1.
- ##### Não Especificado ::/128
	- Equivalente ao endereço IPv4 unspecified 0.0.0.0.
- ##### IPv4 mapeado ::FFFF:wxyz
	- Usado para mapear um endereço IPv4 em um endereço IPv6 de 128 bits, onde wxyz representa os 32 bits do endereço IPv4, utilizando digitos decimais.
	- ![[Pasted image 20251015114803.png]]
- ##### Faixas Especiais
	- 2001:db8::/32: prefixo usado para representar endereços IPv6 em textos e documentações.


### Coexistência e Transição IPv4 E IPv6

##### Pilha Dupla

- Provê o suporte a ambos os protocolos no mesmo dispositivos (Notebooks pessoais);
- Funciona mediante nós - se a comunicação for ocorrer com um nó IPv6, comporta-se como um nó IPv6, a mesma coisa acontece com o IPv4

##### Tunelamento

- Permite o tráfego de pacotes IPv6 sobre a estrutura da rede IPv4 já existente;

##### Tradução

- Permite a comunicação entre nós com suporte apenas a IPv6 com nós que suportam apenas IPv4.


## Protocolo ICMP (Internet Message Control Protocol)

- Mecanismo de envio de mensagens para fins específicos.
- Permite que os hosts enviem *mensagens de ERRO ou de controle* a outros hosts da rede.
- As mensagens são *encapsuladas em datagramas IPv4*.
- Ex.: ping, redes inalcançáveis, hospedeiros inalcançáveis, descoberta de roteador, rede de destino desconhecida, protocolo de destino inalcançável, etc.

- #### ICMPv6
	- Mensagens em duas categorias:
		- Mensagens de erro: diversos tipos(1 a 127);
		- Mensagens de Informação: 128 a 255.
	- Essencial para funcionalidades do IPv6:
		- Gerenciamento de grupos Multicast;
		- Descoberta de vizinhança;
		- Mobilidade IPv6;
		- Descoberta do Path MTU.
	- Assume funcionalidades de outros protocolos do IPv4:
		- ARP: Mapeamento de endereços IP/MAC;
		- IGMP: Gerenciamento de grupos multicast.
