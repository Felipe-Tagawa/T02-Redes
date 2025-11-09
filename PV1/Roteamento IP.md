
- Os roteadores tem a função de escolher a melhor rota para mandar os pacotes.
- Há comunicação entre os roteadores para escolha das melhores rotas.
- Se não houver uma rota, o pacote é descartado, a não ser que exista uma *rota padrão*, que fará com que o pacote sempre seja encaminhado a ela se não for encontrado a rota correta.
- Tipos de Roteamento:
	- Estático: O próprio desenvolvedor cria manualmente as rotas.
	- Dinâmico: Rotas criadas automaticamente por protocolos (mais flexível, escalável e fácil de gerenciar grandes redes)

#### Configuração de Interface pelo Roteador(Packet Tracer)


![[Pasted image 20250910175410.png]]
![[Pasted image 20250910175650.png]]

## 1. Introdução: O Roteamento como Coração das Redes de Dados

O roteamento IP é um conceito fundamental para o funcionamento de qualquer rede de dados moderna, servindo como o mecanismo central que permite a comunicação entre dispositivos localizados em redes distintas. Em sua essência, o roteamento consiste em selecionar o caminho ideal para que um pacote de dados viaje de sua origem até seu destino final. Essa seleção de caminho é denominada "rota" e é a base sobre a qual toda a infraestrutura da internet está construída.  

A complexa malha de redes interconectadas que compõe a internet exige que dispositivos especializados, conhecidos como roteadores, atuem como guias inteligentes para direcionar o fluxo de tráfego. Para cumprir essa função, cada roteador mantém uma base de dados interna, a Tabela de Roteamento, que armazena informações sobre as rotas conhecidas. A eficiência e a resiliência dessa tabela são críticas para garantir que os pacotes cheguem aos seus destinos de forma confiável e com o menor atraso possível. Sem um sistema de roteamento bem-definido, a navegação de dados em uma rede de grande escala seria impraticável e ineficiente, tornando a internet, como a conhecemos, inviável.  

## 2. A Distinção Essencial: Protocolos Roteados vs. Protocolos de Roteamento

A terminologia no campo do roteamento IP pode ser sutil e, por vezes, confusa. Uma das distinções mais importantes a ser compreendida é a diferença fundamental entre "protocolos roteados" e "protocolos de roteamento". Embora os nomes sejam semelhantes, suas funções e propósitos na arquitetura de rede são completamente distintos.

### 2.1 Protocolos Roteados: O Transportador de Dados

Os protocolos roteados, também conhecidos como protocolos roteáveis, são aqueles que fornecem as informações de endereçamento lógico para que os roteadores possam tomar decisões de encaminhamento. Eles operam na Camada 3 (Camada de Rede) do modelo OSI e são responsáveis por *encapsular e transportar os dados do usuário* final através de redes interconectadas. A principal característica de um protocolo roteado é que ele contém um endereço de rede de origem e um endereço de rede de destino, permitindo que um roteador identifique para onde o pacote deve ser enviado em sua jornada. O exemplo mais proeminente e praticamente universal de um protocolo roteado é o *Protocolo de Internet (IP), tanto em sua versão IPv4 quanto IPv6*. Outros exemplos históricos incluem IPX da Novell e XNS da Xerox.  

### 2.2 Protocolos de Roteamento: O Construtor de Rotas

Em contraste, os protocolos de roteamento não transportam os dados do usuário final. Eles são utilizados exclusivamente pelos roteadores para *trocar informações sobre redes conhecidas e construir a Tabela de Roteamento*, também referida como Routing Information Base (RIB). A função primordial desses protocolos é a *descoberta e atualização de rotas*. Eles se comunicam em segundo plano, enviando mensagens de controle que permitem aos roteadores aprender sobre a topologia da rede, identificar novos caminhos e adaptar-se a falhas ou mudanças. A família de protocolos de roteamento dinâmico inclui exemplos como *RIP, OSPF, BGP, EIGRP e IS-IS*.  

### 2.3 A Interdependência Crítica: Uma Análise Causal

A relação entre esses dois tipos de protocolos é uma simbiose essencial para o funcionamento de uma rede. Os protocolos de roteamento (p. ex., OSPF) dependem do protocolo roteado (IP) para transportar suas próprias mensagens de controle. Ou seja, uma mensagem de atualização de roteamento de um roteador OSPF é encapsulada dentro de um pacote IP para ser enviada a outro roteador. Ao receber essa mensagem, o roteador a processa e usa as informações contidas nela para atualizar sua Tabela de Roteamento.  

Essa atualização é o ponto de virada. A partir de uma Tabela de Roteamento completa e atualizada, o roteador ganha o conhecimento necessário para encaminhar de forma inteligente o tráfego de dados real, que é transportado pelo protocolo roteado (IP). A dependência é cíclica e fundamental: *os protocolos de roteamento constroem a base de conhecimento que permite o funcionamento do roteamento, e utilizam o próprio protocolo roteado como o meio de transporte para construir e manter essa base de conhecimento*.

O quadro a seguir sintetiza as diferenças e a interdependência entre os dois tipos de protocolos:

|Característica|Protocolos Roteados|Protocolos de Roteamento|
|---|---|---|
|**Finalidade Principal**|Transportar dados do usuário final.|Construir e manter tabelas de roteamento.|
|**Camada OSI de Operação**|Camada 3 (Rede).|Camada 3 (Rede) ou superior (dependendo do protocolo, como BGP usando TCP).|
|**Exemplos**|IP, IPX, XNS.|RIP, OSPF, BGP, EIGRP, IS-IS.|
|**Tipo de Tráfego Transportado**|Tráfego de dados de aplicativos (e-mail, web, vídeo, etc.).|Mensagens de controle e de atualização de roteamento.|


## 3. Tipos de Rotas e Suas Aplicações

A tabela de roteamento de um roteador pode ser populada por diferentes tipos de rotas, cada uma com uma origem e uma finalidade específica. O conhecimento de como esses tipos de rotas são descobertos ou configurados é crucial para o gerenciamento de uma rede.

### 3.1 Rotas Diretas (ou Automáticas)

São as rotas mais elementares. Um roteador as aprende de forma automática quando uma de suas interfaces é ativada e conectada a uma rede. *Essa rota indica que a rede em questão está diretamente acessível através daquela interface física ou virtual*. A tabela de roteamento as identifica como redes "diretamente conectadas."  

### 3.2 Rotas Estáticas

Uma rota estática é um *caminho de rede configurado manualmente* por um administrador. Por serem fixas, *essas rotas não se adaptam automaticamente a mudanças na topologia da rede*. *Sua utilização é comum em redes de pequeno porte* ou para criar caminhos de backup específicos para determinados destinos.  

O material de pesquisa fornecido detalha a sintaxe de configuração para ambos os protocolos IP. Para IPv4, o comando é `ip route`, seguido pela rede de destino, a máscara de sub-rede e o próximo salto (que pode ser o endereço IP do roteador seguinte ou a interface de saída). Um exemplo de configuração seria  

`Router1(config)# ip route 192.168.20.0 255.255.255.0 192.168.100.2`. Da mesma forma, para IPv6, o comando  

`ipv6 route` é usado, com a rede de destino e seu prefixo, seguidos pelo próximo salto ou interface de saída.  

### 3.3 Rotas Padrão (Default Routes)

*Uma rota padrão é uma rota de último recurso. Ela é utilizada pelo roteador para encaminhar um pacote quando a rede de destino não é encontrada em sua tabela de roteamento*. Em termos práticos, é a "rota para tudo o que eu não conheço."  

Sua aplicação é ideal para redes _stub_, que são redes com um único ponto de saída para o resto da internet. Por exemplo, a rede de uma residência ou de uma pequena empresa que se conecta a um único provedor de serviços de internet. A configuração de uma rota padrão é feita utilizando endereços de rede genéricos: `0.0.0.0 0.0.0.0` para IPv4 e `::/128` para IPv6, seguidos pelo gateway de último recurso.  

### 3.4 Rotas Dinâmicas

Diferentemente das rotas estáticas, *as rotas dinâmicas são automaticamente descobertas e mantidas através da comunicação entre roteadores, utilizando os protocolos de roteamento*. Essa capacidade de adaptação automática é o que permite que redes de grande escala, como a internet, se ajustem a falhas de link, novos caminhos e mudanças na topologia sem intervenção manual constante.  

## 4. Classificação dos Protocolos de Roteamento Dinâmico: Uma Arquitetura Hierárquica

A arquitetura de roteamento da internet é hierárquica e federada, refletindo a necessidade de gerenciar a conectividade em diferentes escalas. Essa estrutura é o que impulsiona a classificação dos protocolos de roteamento em grupos distintos, cada um projetado para um propósito específico.

### 4.1 Classificação por Finalidade: IGP vs. EGP

*A base dessa classificação é o conceito de Sistema Autônomo (AS - Autonomous System), que é um conjunto de redes sob uma única administração e que compartilha uma política de roteamento comum*. Cada AS é identificado por um número exclusivo, o ASN (Autonomous System Number). A internet é, em essência, uma coleção de ASes interconectados.  

Os ASes podem ser classificados em três tipos principais:

- **AS Stub:** Um sistema autônomo conectado a apenas um outro AS, sem permitir tráfego de trânsito.  
    
- **AS Multihomed:** Um sistema autônomo conectado a mais de um AS, mas que também não permite tráfego de trânsito. Isso é comum em grandes empresas que buscam redundância de conexão com a internet.  
    
- **AS de Trânsito:** Um sistema autônomo conectado a mais de um AS e que permite que o tráfego de dados passe por ele, interligando outras redes. Grandes provedores de serviços de internet (ISPs) são exemplos de ASes de trânsito.  
    

Com base nesse conceito, os protocolos de roteamento são divididos em:

- **Interior Gateway Protocols (IGPs):** *Operam _dentro_ de um único Sistema Autônomo (Intra-AS). Sua principal função é garantir que todos os roteadores internos tenham uma visão consistente da topologia e do melhor caminho para qualquer destino dentro daquele AS. Exemplos incluem RIP, OSPF, EIGRP e IS-IS.*
    
- **Exterior Gateway Protocols (EGPs):** *Operam _entre_ diferentes Sistemas Autônomos (Inter-AS). O principal protocolo EGP em uso hoje é o Border Gateway Protocol (BGP). A escolha de rotas entre ASes não se baseia apenas em métricas de "menor custo" como nos IGPs, mas também em políticas, acordos comerciais e outros fatores complexos.*  
    

### 4.2 Classificação por Operação: Vetor de Distância, Estado de Enlace e Vetor de Caminho

A forma como um protocolo de roteamento coleta e distribui informações define seu algoritmo de operação, que está diretamente relacionado ao seu desempenho, escalabilidade e consumo de recursos.

- **Protocolos Vetor de Distância (Distance Vector):** O princípio fundamental desses protocolos é que cada roteador anuncia rotas com base em duas características: a "distância" (custo para a rede de destino, geralmente o número de saltos) e o "vetor" (a direção, ou seja, a interface de saída ou o próximo salto). Os roteadores só trocam informações com seus vizinhos diretos, e essas atualizações ocorrem periodicamente, mesmo que não haja mudanças na topologia. A principal desvantagem é a *convergência lenta e a falta de uma visão completa da rede*, o que pode levar a problemas como loops de roteamento. Exemplos incluem *RIPv1*, RIPv2 e RIPng.  
    
- **Protocolos Estado de Enlace (Link State):** Esses protocolos operam de maneira mais complexa. Cada roteador constrói um "mapa" completo da topologia da rede, descobrindo seus vizinhos e os custos para alcançá-los. Essas informações são empacotadas em pacotes de estado de enlace (LSPs) e "inundadas" para todos os outros roteadores na mesma área. Com esse "mapa" em mãos, *cada roteador executa o algoritmo SPF (Shortest Path First), também conhecido como algoritmo de Dijkstra, para calcular a árvore de caminho mais curto para cada destino e, em seguida, popula sua tabela de roteamento*. As atualizações não são periódicas; elas ocorrem apenas na inicialização e quando uma mudança na topologia é detectada. A principal vantagem é a *convergência rápida e a garantia de um roteamento sem loops*, mas isso vem ao custo de um *maior uso de recursos computacionais, como CPU e memória*. Exemplos notáveis são *OSPF e IS-IS*.  
    
- **Protocolos Vetor de Caminho (Path Vector):** Semelhante aos protocolos de vetor de distância, mas o anúncio de rota inclui a lista completa de Sistemas Autônomos que o pacote deve atravessar para chegar ao destino. Essa característica é crucial para o roteamento Inter-AS, pois permite que o protocolo evite loops de roteamento de forma mais eficaz e aplique políticas de tráfego complexas, um fator mais importante do que a simples distância em uma rede global. O único exemplo proeminente é o *BGP*.  
    

O quadro a seguir resume as principais diferenças entre os algoritmos de roteamento:

| Característica                 | Vetor de Distância                            | Estado de Enlace                                        | Vetor de Caminho                   |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------- | ---------------------------------- |
| **Princípio de Operação**      | Troca de tabelas com vizinhos diretos.        | Construção de um mapa topológico da rede.               | Anúncio de caminhos de AS para AS. |
| **Métrica Típica**             | *Contagem de saltos*.                         | *Custo (inversamente proporcional à largura de banda)*. | *Políticas, atributos de caminho*. |
| **Visão da Topologia**         | Parcial (apenas a de vizinhos).               | Completa da área.                                       | De caminhos entre ASes.            |
| **Velocidade de Convergência** | Lenta.                                        | Rápida.                                                 | Lenta (focada em estabilidade).    |
| **Uso de Recursos**            | Baixo.                                        | Alto (CPU e memória).                                   | Baixo a moderado.                  |
| **Escalabilidade**             | Limitada (mais adequado para redes pequenas). | Alta (suporta hierarquia de áreas).                     | Máxima (usado na internet global). |


## 5. Análise Detalhada dos Principais Protocolos de Roteamento

### 5.1 Família RIP (Routing Information Protocol)

O RIP é um dos protocolos de roteamento dinâmico mais antigos e simples. O RIPv1, a versão original, é um protocolo de vetor de distância que utiliza o algoritmo Bellman-Ford. *Sua métrica se baseia na contagem de saltos (hops)*, com um limite máximo de 15 saltos, o que o torna inadequado para redes de grande escala. Além disso, o RIPv1 é um protocolo _classful_, o que significa que ele não inclui informações de máscara de sub-rede em seus anúncios, inviabilizando o uso de sub-redes de tamanho variável (VLSM). As atualizações de rota são enviadas periodicamente a cada 30 segundos, utilizando broadcast.  

O RIPv2 foi uma atualização crucial que o tornou um protocolo _classless_, permitindo que as máscaras de rede fossem incluídas nos anúncios. Isso viabilizou o suporte a VLSM e CIDR. Outra melhoria foi a substituição do broadcast pelo endereço multicast 224.0.0.9 para o envio de atualizações.  

Para IPv6, foi desenvolvida a versão RIPng (RIP next generation), que mantém o princípio de vetor de distância e a métrica de contagem de saltos com o limite de 15. Embora seja uma adaptação para o novo protocolo de endereçamento, o RIPng ainda é considerado de *convergência lenta e mais adequado para redes pequenas e médias*.  

### 5.2 OSPF (Open Shortest Path First)

O OSPF é um protocolo de roteamento de *estado de enlace* e de padrão aberto (daí o "Open"). Diferentemente do RIP, ele usa o algoritmo de Dijkstra (SPF) para calcular o caminho de *menor custo* até um destino. *O custo de um link é uma métrica calculada com base na largura de banda (BW) da interface*, onde Custo = 108 / BW. Uma largura de banda maior resulta em um custo menor, o que tende a priorizar links mais rápidos.  

Uma das maiores vantagens do OSPF é sua *rápida convergência*, pois as atualizações são disparadas imediatamente quando uma mudança na topologia é detectada. Ele também é *altamente escalável e suporta uma arquitetura hierárquica multiárea*, na qual todas as áreas devem se conectar à Área de Backbone (Área 0). A versão OSPFv2 é amplamente utilizada em redes IPv4, enquanto o OSPFv3 foi desenvolvido para redes IPv6 e pode rodar em redes IPv4 e IPv6 simultaneamente. Estudos mostram que o OSPFv3 tem desempenho superior ao RIPng em termos de atraso e perda de pacotes.  

### 5.3 BGP (Border Gateway Protocol)

O BGP é o protocolo de fato para roteamento na internet global, sendo o *único Exterior Gateway Protocol (EGP) relevante*. *Sua função é permitir a troca de informações de roteamento entre Sistemas Autônomos*, viabilizando que um AS anuncie suas redes e as redes que ele aprendeu de outros ASes.  

*O BGP é um protocolo de vetor de caminho*. Seus anúncios de rota incluem a lista completa de ASes que o pacote deve atravessar para chegar ao seu destino. Essa característica é crucial para evitar loops de roteamento em redes de grande escala e para permitir a implementação de políticas de roteamento complexas, que podem levar em conta fatores como largura de banda, preço da conexão e acordos comerciais. As sessões BGP entre roteadores de borda são estabelecidas usando o protocolo TCP na porta 179, o que garante a confiabilidade na troca de informações.  

O BGP pode operar em dois modos:

- **eBGP (external BGP):** Utilizado para a comunicação entre roteadores localizados em ASes distintos.  
    
- **iBGP (internal BGP):** Utilizado para a comunicação entre roteadores dentro do mesmo AS, para garantir a consistência das rotas aprendidas via eBGP.  
    

A seguir, um quadro comparativo dos principais protocolos de roteamento:

| Característica                 | RIP                      | OSPF                                  | BGP                                     |
| ------------------------------ | ------------------------ | ------------------------------------- | --------------------------------------- |
| **Classificação (IGP/EGP)**    | IGP                      | IGP                                   | EGP                                     |
| **Tipo de Algoritmo**          | Vetor de Distância       | Estado de Enlace                      | Vetor de Caminho                        |
| **Métrica**                    | *Contagem de saltos*     | *Custo (baseado em largura de banda)* | *Políticas, atributos do caminho*       |
| **Escalabilidade**             | Limitada (até 15 saltos) | Alta (multiárea)                      | Máxima (Internet)                       |
| **Velocidade de Convergência** | Lenta                    | Rápida                                | Lenta                                   |
| **Uso de Recursos**            | Baixo                    | Alto                                  | Baixo a moderado                        |
| **Exemplo de Aplicação**       | Pequenas redes locais    | Grandes redes corporativas            | Roteamento entre provedores de internet |


## 6. Modelos de Roteamento: Unicast vs. Multicast

Além de selecionar o melhor caminho, o roteamento também define o modelo de transmissão de dados, ou seja, para quantos e quais destinatários um pacote deve ser enviado.

### 6.1 Roteamento Unicast(1:1)

O roteamento unicast é o modelo de transmissão mais comum e o padrão para a maioria das comunicações na internet. *Ele é caracterizado por uma comunicação "um-para-um", onde um único dispositivo de origem envia dados para um único dispositivo de destino*. Isso é o que ocorre quando um usuário navega em um site, faz uma consulta a um servidor DNS, ou envia um e-mail. O roteador, nesse caso, encaminha o pacote para uma única interface de saída, conforme o endereço de destino na tabela de roteamento.  

### 6.2 Roteamento Multicast(1:N)

O roteamento multicast se baseia em um modelo de transmissão "um-para-um-grupo". *Uma única fonte envia dados para um grupo específico de destinatários que podem estar em redes diferentes*. Esse modelo é crucial para otimizar o uso da largura de banda em aplicações como IPTV, streaming de vídeo e videoconferências, onde a mesma informação precisa ser entregue a múltiplos receptores simultaneamente sem a necessidade de replicar o pacote para cada um individualmente.  

No contexto de protocolos de roteamento, o OSPF utiliza endereços multicast (por exemplo, 224.0.0.5) para enviar suas mensagens "Hello" e descobrir vizinhos, o que demonstra a aplicação do multicast em tráfego de controle. O IPv6, em um avanço de design, aboliu o conceito de broadcast e o substituiu por um endereço multicast ( `ff02::1`) que tem a mesma finalidade de alcançar todos os nós em um link, mas de forma mais controlada.  

## 7. Conclusões e Apanhado Geral

A complexidade do roteamento IP é uma resposta direta à necessidade de interligar redes globalmente de forma eficiente e resiliente. A jornada de um pacote começa com a distinção fundamental entre os protocolos que o transportam (os roteados, como o IP) e os que guiam seu caminho (os de roteamento, como OSPF e BGP).

A estrutura da internet é governada por uma arquitetura hierárquica, baseada nos Sistemas Autônomos. Dentro de cada AS, protocolos como o OSPF ou RIP garantem a conectividade interna e a convergência rápida. A nível global, o BGP orquestra o roteamento entre os ASes, levando em conta não apenas a distância, mas políticas administrativas e comerciais. Essa divisão de responsabilidades é o que permite que a internet escale de forma massiva, sem que cada roteador precise conhecer a totalidade da topologia global.  

A escolha de um protocolo de roteamento é uma decisão de engenharia que exige ponderação de fatores como convergência, consumo de recursos e escalabilidade. O OSPF, com sua rápida convergência e roteamento sem loops, é a escolha robusta para redes corporativas, ao custo de um maior consumo de recursos. O RIP, por sua vez, é simples e de baixo consumo, mas sofre com a lentidão de convergência e limitações de escala. A compreensão desses  

_trade-offs_ e da interconexão entre os diferentes conceitos, do tipo de rota à classificação de protocolos, é a essência do design de redes de dados e a base para a gestão eficiente da comunicação em qualquer escala.