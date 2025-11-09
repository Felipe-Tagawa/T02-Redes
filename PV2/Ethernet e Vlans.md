## I. Fundamentos do Padrão Ethernet (IEEE 802.3) e Arquitetura de Camada 2

O padrão Ethernet é, historicamente e na atualidade, o protocolo de rede local cabeada adotado em praticamente a totalidade dos ambientes empresariais e residenciais. Sua relevância advém de uma arquitetura robusta e adaptável que evoluiu significativamente desde sua criação no início dos anos 70.   

### 1.1. Contexto e Mapeamento no Modelo OSI

O padrão Ethernet, formalmente conhecido como IEEE 802.3, opera nas duas primeiras camadas do modelo de interconexão de sistemas abertos (OSI): a Camada Física e a Camada de Enlace.   

A Camada Física é responsável pela codificação e transmissão dos bits sobre o meio físico, determinando especificações como tipos de cabo (coaxial, par trançado UTP/STP, ou fibra), distâncias máximas de transmissão e taxas de sinalização. Exemplos históricos incluem padrões como 10BASE-5 e 10BASE-T, enquanto versões modernas focam em 1000BASE-T e 10GBASE-T.   

A Camada de Enlace de Dados é crucial para a funcionalidade do Ethernet e é subdividida em duas subcamadas distintas, conforme definido pelos padrões IEEE :   

1. **Logical Link Control (LLC):** Padronizada pelo IEEE 802.2, a LLC é responsável pelo controle do enlace lógico, fornecendo suporte à Camada de Rede (Camada 3), incluindo endereçamento, reconhecimento de quadros e funções básicas de controle de erros.
    
2. **Media Access Control (MAC):** Esta subcamada, definida principalmente pelo padrão IEEE 802.3, é responsável pelo controle de acesso ao meio compartilhado e pela organização da disputa pelo meio físico. Ela também define o formato do quadro Ethernet e o endereçamento físico.   
    

O mapeamento entre as camadas do modelo OSI e as subcamadas Ethernet é fundamental para a compreensão de sua arquitetura:

Mapeamento Ethernet (IEEE 802.3) no Modelo OSI

|**Camada OSI**|**Padrão Relacionado**|**Subcamada / Função Central**|
|---|---|---|
|Enlace (Data Link)|IEEE 802.3, 802.2|**LLC (Logical Link Control):** Controle de Enlace Lógico, suporte à Camada 3, controle de erros.|
|Enlace (Data Link)|IEEE 802.3 (CSMA/CD)|**MAC (Media Access Control):** Controle de Acesso ao Meio Compartilhado, Endereçamento Físico (MAC).|
|Física (Physical)|IEEE 802.3|Codificação, temporização e transmissão de bits.|

### 1.2. Controle de Acesso ao Meio: CSMA/CD

O método original de controle de acesso ao meio para o padrão IEEE 802.3 é o **CSMA/CD** (_Carrier Sense Multiple Access with Collision Detection_). Esta técnica foi fundamental na fase inicial da Ethernet, baseada em meios compartilhados (como o cabo coaxial), onde todos os dispositivos competiam pelo mesmo segmento de rede.   

O CSMA/CD opera sob um princípio de três etapas :   

1. **Escuta do Meio (_Carrier Sense_):** Quando um nó deseja enviar dados, ele verifica primeiramente se o meio de rede está livre (_não ocupado_). Se estiver ocupado, ele aguarda um tempo aleatório (_backoff_) antes de tentar novamente.
    
2. **Transmissão e Detecção:** Se o meio estiver livre, o nó inicia a transmissão e, simultaneamente, continua a "escutar" o meio para garantir que nenhuma outra estação esteja transmitindo ao mesmo tempo. A ocorrência de uma colisão é detectada pelo aumento da amplitude do sinal físico no meio.   
    
3. **Resolução de Colisão:** Ao detectar uma colisão, o nó interrompe imediatamente a transmissão do quadro. Ele envia um sinal de reforço de colisão (_jam signal_, equivalente a 32 bits) para garantir que todas as outras estações na rede saibam que ocorreu uma colisão. Após isso, o nó reinicia o algoritmo de _backoff_ binário exponencial, que gera um tempo de espera aleatório antes de tentar retransmitir o quadro.   
    

É importante notar que o CSMA/CD é uma característica definidora do padrão 802.3 para redes cabeadas. No entanto, a implementação de Ethernet comutada (_switches_) e a operação em modo _full-duplex_ (onde dispositivos podem transmitir e receber simultaneamente) eliminam a ocorrência de colisões. Essa transição da mídia compartilhada (onde CSMA/CD era essencial) para a comutação ponto-a-ponto demonstra a notável capacidade de adaptação do padrão 802.3. Embora o mecanismo de detecção de colisão seja obsoleto em redes modernas _full-duplex_, o 802.3 mantém sua arquitetura base e endereçamento.   

### 1.3. Endereçamento Físico (MAC) e Estrutura do Quadro

O endereçamento Ethernet é baseado no **Endereço MAC** (_Media Access Control_), denominado endereço físico. Este endereço é um identificador único, globalmente administrado, que está associado ao adaptador de rede (NIC) do dispositivo.   

#### Endereço MAC

O endereço MAC é constituído por **48 bits**, sendo convencionalmente representado na forma hexadecimal (12 dígitos hexadecimais). Este identificador é dividido em duas partes iguais de 24 bits (6 dígitos hexadecimais) :   

1. **Identificador do Fabricante (OUI - _Organizationally Unique Identifier_):** Os primeiros 24 bits são atribuídos pela IEEE ao fabricante do equipamento (por exemplo, `00 60 2F`).
    
2. **Número Serial do Fabricante:** Os 24 bits subsequentes constituem o número de série atribuído pelo fabricante, garantindo a unicidade do endereço para o dispositivo (por exemplo, `3A 07 BC`).   
    

A limitação do endereço MAC é que ele só permite a comunicação dentro do mesmo domínio de broadcast (segmento de rede local). Para a comunicação entre diferentes segmentos lógicos (como redes IP diferentes ou VLANs), torna-se indispensável o uso de endereços lógicos (IP) e dispositivos de Camada 3.

#### Estrutura do Quadro Ethernet

O quadro Ethernet é a unidade de dados na Camada de Enlace. Seu formato padrão inclui vários campos essenciais para o transporte e sincronização dos dados :   

- **Preâmbulo e Delimitador de Início de Quadro:** O **Preâmbulo** é uma sequência de 7 octetos de uns e zeros alternados (10101010) e é utilizado fundamentalmente para a **sincronização** dos relógios entre os dispositivos transmissor e receptor, especialmente nas versões assíncronas de 10 Mbps. O **Delimitador de Início de Quadro** (um octeto, 10101011) marca o final das informações de temporização e o início efetivo do quadro.   
    
- **Endereço de Destino e Endereço de Origem:** Contêm os endereços MAC de 48 bits do destino e da origem, respectivamente.
    
- **Comprimento/Tipo:** Este campo especifica o protocolo da camada superior (Camada 3) contido na seção de Dados (por exemplo, IP, ARP). Alternativamente, pode indicar o número de bytes de dados que se seguem.
    
- **Dados e Enchimento (_Padding_):** Contém os dados da camada superior (carga útil). O quadro Ethernet exige um tamanho mínimo de 46 bytes e um máximo de 1500 bytes (MTU). O _padding_ é adicionado se o campo de dados for menor que o mínimo exigido.
    
- **FCS (_Frame Check Sequence_):** Contém 4 bytes (32 bits) criados e anexados pelo dispositivo emissor, fazendo uso de um código CRC-32 (_Cyclic Redundancy Check_). O dispositivo receptor recalcula o CRC para verificar a integridade do quadro e detectar erros durante a transmissão.   
    

### 1.4. Evolução Tecnológica e Vantagens da Ethernet

A evolução do padrão Ethernet é marcada pela transição do meio coaxial compartilhado para o par trançado e fibra ótica, e mais notavelmente, pela substituição de _hubs_ por _switches_ na década de 90. A introdução da Ethernet comutada (_switches_) permitiu o uso do modo _full-duplex_, eliminando a maioria das colisões e aumentando drasticamente o desempenho e a escalabilidade da rede.   

#### Escalabilidade de Velocidade

A capacidade do padrão 802.3 de escalar suas velocidades, mantendo a compatibilidade fundamental do formato de quadro e endereçamento, é o principal motivo de sua dominância. A evolução cronológica inclui:

|Velocidade|Ano de Padrão (Marco)|
|---|---|
|10 Mb/s|1983|
|100 Mb/s (Fast Ethernet)|1995|
|1 Gb/s (Gigabit Ethernet - GbE)|1998|
|10 Gb/s|2002|
|40 Gb/s e 100 Gb/s|2010|
|2.5 Gb/s, 5 Gb/s, 25 Gb/s, 50 Gb/s, 200 Gb/s e 400 Gb/s|2017|

Além disso, a evolução continua com planos para a próxima era da Ethernet, incluindo 800 GbE, 1.6 TbE e velocidades de 1 Tb/s.   

#### Vantagens Chave

A ampla adoção da Ethernet é atribuída às suas vantagens operacionais e econômicas: simplicidade e facilidade de manutenção, alta confiabilidade e custos econômicos de instalação e atualização.   

## II. Redes Locais Virtuais (VLANs - IEEE 802.1Q)

Embora a Ethernet comutada tenha resolvido os problemas de colisão, todas as estações conectadas a um conjunto de _switches_ de Camada 2 ainda pertencem, por padrão, ao mesmo domínio de broadcast. O excesso de tráfego de broadcast pode degradar o desempenho. As VLANs (_Virtual Local Area Networks_) surgiram como uma solução para segmentar o domínio de broadcast em nível de Camada 2, aumentando a eficiência, a segurança e a organização das redes locais.   

### 2.1. Conceito, Finalidade e Vantagens da Segmentação Lógica

Uma VLAN permite a coexistência de múltiplas redes lógicas independentes na mesma infraestrutura física de _switching_. O conceito central das VLANs é o **agrupamento lógico de _hosts_**, tornando a segmentação de rede independente da localização física do dispositivo.   

#### Segmentação e Domínios de Broadcast

A principal função técnica de uma VLAN é que **cada VLAN define um domínio de broadcast distinto** (uma rede IP separada logicamente). Isso significa que o tráfego de broadcast gerado por um dispositivo em uma VLAN (e.g., VLAN 10) não será encaminhado para dispositivos em outras VLANs (e.g., VLAN 20), garantindo o isolamento lógico.   

A implementação de VLANs oferece várias vantagens significativas :   

- **Desempenho Mais Alto:** Ao dividir uma grande rede em grupos lógicos menores, o tráfego de broadcast é contido. Essa redução da carga de tráfego em cada rede lógica aumenta o desempenho geral.
    
- **Atenuação de Tempestades de Broadcast:** A limitação dos domínios de broadcast reduz o número de dispositivos que podem ser afetados por uma situação de descontrole por excesso de broadcast, melhorando a resiliência da rede.
    
- **Segurança:** Grupos de dispositivos que manipulam dados sensíveis podem ser isolados do restante da rede, criando um perímetro de segurança em Camada 2.
    
- **Redução de Custo:** Resultante do uso mais eficiente da largura de banda e do cabeamento existente, pois não é necessário hardware de _switching_ ou cabeamento separado para cada rede lógica.
    

### 2.2. O Padrão IEEE 802.1Q e o Conceito de Trunking

O padrão que estabelece as definições básicas para a implementação de VLANs em redes Ethernet e o mecanismo para a marcação de quadros (_tagging_) é o **IEEE 802.1Q**.   

#### Tronco de VLAN (Trunking)

Um tronco de VLAN (_trunk_) é um enlace ponto a ponto, tipicamente estabelecido entre dois _switches_ ou entre um _switch_ e um roteador, que tem a capacidade de transportar quadros pertencentes a **diferentes VLANs** simultaneamente. O tronco não pertence a uma VLAN específica; ele funciona como um canal de multiplexação para o tráfego de múltiplas VLANs sobre um único _link_ físico de alta velocidade (Fast Ethernet ou Gigabit Ethernet).   

O padrão 802.1Q é utilizado para coordenar esses troncos. Quando o tráfego atravessa um _link_ tronco, o cabeçalho 802.1Q é adicionado ao quadro Ethernet original para fornecer uma etiqueta (_tag_) que especifica a qual VLAN aquele quadro pertence. A capacidade de multiplexar milhares de redes lógicas em um único cabo físico é o que torna o 802.1Q uma solução eficiente e econômica.   

#### Marcação de Quadros (Tagging)

O processo de marcação (_tagging_) ocorre quando um _switch_ recebe um quadro em uma porta configurada em modo de acesso para uma VLAN específica. Antes de enviar o quadro pela interface de tronco (que pode levar a outro _switch_ ou a um roteador), o _switch_ insere a etiqueta de VLAN (tag) correspondente. A etiqueta 802.1Q está presente apenas nas conexões tronco.   

### 2.3. Estrutura do Campo de Marcação (Tag 802.1Q)

A inserção da marcação 802.1Q adiciona 4 bytes (32 bits) ao quadro Ethernet original. A estrutura desse cabeçalho é definida pelos seguintes campos :   

Campos de Marcação de VLAN (IEEE 802.1Q Tag)

|**Campo**|**Tamanho (Bits)**|**Descrição da Função**|
|---|---|---|
|TPID (_Tag Protocol Identifier_)|16|Identificador de Protocolo, com valor 0x8100 (hexa) para indicar que o quadro contém a marcação 802.1Q.|
|PRI (Prioridade)|3|Bits de prioridade utilizados pelo padrão 802.1p para classificar o tráfego (Qualidade de Serviço - QoS).|
|CFI (_Canonical Format Identifier_)|1|Indicador de formato; permite o transporte de quadros Token Ring por links Ethernet (atualmente sem uso).|
|VID (VLAN ID)|12|**Número de Identificação da VLAN**. Suporta até 212=4096 IDs de VLANs (de 1 a 4094).|

O campo VID, composto por 12 bits, é o elemento crucial que permite ao _switch_ ou roteador multicamada identificar e segregar o tráfego de cada rede lógica.

### 2.4. Intervalos de ID de VLAN

Os identificadores de VLAN (VIDs) são categorizados em dois intervalos, dependendo do porte e da aplicação da rede :   

- **VLANs de Intervalo Normal (1 a 1005):** Usadas tipicamente em redes corporativas de pequeno e médio porte. A VLAN 1 é a VLAN padrão, criada automaticamente em todos os _switches_ e não pode ser removida.
    
- **VLANs de Intervalo Estendido (1006 a 4094):** Usadas em grandes redes empresariais ou por operadoras para estender sua infraestrutura para um número maior de clientes, aproveitando a capacidade total de 4094 IDs.   
    

## III. Comunicação e Roteamento Inter-VLAN (Camada 3)

Apesar de as VLANs segmentarem a rede física em múltiplas redes lógicas de Camada 2, este isolamento lógico implica que dispositivos pertencentes a VLANs diferentes não podem se comunicar diretamente, pois pertencem a domínios de broadcast distintos (e, consequentemente, a sub-redes IP diferentes).   

### 3.1. Necessidade de Roteamento Inter-VLAN

Para que haja comunicação entre hosts em VLANs distintas (por exemplo, um host na VLAN 10 se comunicando com um host na VLAN 20), é estritamente necessário implementar funcionalidades da **Camada 3** (Rede), ou seja, o **roteamento**. O dispositivo responsável por essa função deve ser um roteador dedicado ou um _switch_ que incorpore capacidades de roteamento de Camada 3 (_switch_ multicamada).   

A evolução da infraestrutura de redes locais tem focado em otimizar a velocidade e a eficiência desse roteamento entre VLANs.

### 3.2. Métodos de Roteamento Inter-VLAN

Existem três métodos principais para implementar o roteamento inter-VLAN, que refletem a evolução da tecnologia de rede, visando a maior escalabilidade e desempenho :   

#### A. Roteamento entre VLANs Tradicional

Este é o método original, que requer o uso de múltiplas interfaces físicas em um roteador dedicado. Cada interface física do roteador é configurada para atuar como o _gateway_ de uma VLAN específica, e é conectada a uma porta de acesso diferente do _switch_.   

Embora funcional, este método é extremamente ineficiente e não escalável. Se uma rede possui dez VLANs, são necessárias dez portas no _switch_ e dez interfaces dedicadas no roteador, o que consome rapidamente recursos caros de hardware.   

#### B. Roteamento _Router on a Stick_ (Roteador Fixo)

O método _Router on a Stick_ (roteador fixo) representa um avanço significativo em termos de eficiência. Ele utiliza uma única interface física de alta velocidade no roteador. Essa interface é configurada no modo **tronco (trunk)**, permitindo que ela transporte o tráfego de todas as VLANs.   

Internamente, o roteador é configurado com múltiplas **subinterfaces** lógicas, onde cada subinterface atua como o _gateway_ de uma VLAN específica. O _switch_ conectado a este roteador também deve ter sua porta configurada como tronco, utilizando o padrão IEEE 802.1Q. Quando o tráfego chega ao roteador, o 802.1Q VID é lido, permitindo que o roteador direcione o quadro para a subinterface correta. Este método é a solução mais comum para economizar portas físicas no roteador.   

#### C. Roteamento Baseado em Switch Layer 3 (Multicamada)

O método mais performático e moderno utiliza **switches multicamada (Layer 3)**. Esses _switches_ possuem a capacidade de executar funções de roteamento internamente, substituindo a necessidade de um roteador dedicado para a comunicação inter-VLAN.   

Ao executar o roteamento em _hardware_ especializado (ASIC) e manter o tráfego dentro do _chassis_ do _switch_, o roteamento baseado em _switch_ L3 oferece latência significativamente menor e maior _throughput_ em comparação com o _Router on a Stick_, onde o tráfego precisa sair do _switch_ e retornar para ser roteado. Este método é crucial para redes de alto desempenho.   

A tabela a seguir resume e compara as características dos métodos de roteamento inter-VLAN:

Comparativo de Métodos de Roteamento Inter-VLAN

|**Método**|**Hardware Utilizado**|**Uso da Interface do Roteador**|**Vantagens Chave**|
|---|---|---|---|
|Tradicional|Roteador Dedicado|1 porta física por VLAN (Portas de Acesso)|Simples de configurar para poucas VLANs.|
|_Router on a Stick_ (Roteador Fixo)|Roteador Dedicado|1 porta física para todas as VLANs (Configurada como Tronco/Subinterfaces)|Economia de portas físicas do roteador; Escalabilidade de _links_.|
|Baseado em Switch L3|Switch Multicamada (Layer 3)|Interfaces Virtuais (SVIs) no próprio _switch_|Maior velocidade (hardware ASIC); Baixa latência; Elimina o gargalo externo.|

## Conclusões

O ambiente de redes locais é definido pela sinergia entre o padrão de comunicação Ethernet (IEEE 802.3) e as tecnologias de segmentação de Camada 2 (VLANs/IEEE 802.1Q). O sucesso da Ethernet baseia-se na estabilidade de sua arquitetura de endereçamento MAC de 48 bits e na adaptabilidade de sua Camada Física, que escalou de 10 Mb/s para centenas de Gb/s.   

A introdução das VLANs, padronizadas pelo 802.1Q, permitiu que as redes locais comutadas superassem as limitações de escalabilidade impostas pelo domínio de broadcast único. O 802.1Q é a tecnologia fundamental que permite a multiplexação de até 4094 redes lógicas sobre um único canal físico (o tronco), otimizando a infraestrutura de cabeamento e reduzindo custos operacionais.   

A segmentação lógica imposta pelas VLANs exige inevitavelmente o uso de um dispositivo de Camada 3 (roteador ou _switch_ L3) para permitir a comunicação inter-VLAN. A evolução das técnicas de roteamento (do Tradicional ao _Router on a Stick_ e, finalmente, ao roteamento nativo em _switches_ L3) demonstra uma clara tendência em empurrar as funções de Camada 3 para mais perto do acesso, minimizando a latência e maximizando o desempenho em ambientes de rede segmentada de alto tráfego. O domínio e a interconexão desses dois padrões (802.3 e 802.1Q) são essenciais para o projeto, a manutenção e a escalabilidade de qualquer rede local moderna.