
Local onde se encontram as aplicações (como navegadores e e-mails) que usam os protocolos da camada de transporte (TCP e UDP), de modo a trocar mensagens entre os sistemas finais.

## DNS (Domain Name System)

- Responsável pela tradução de nomes de domínio(ex.: inatel.br) em endereços IP (ex.: 119.8.151.60);
- Encapsulado no UDP 53 (sem confiabilidade, fica reiterando o pedido);
- Buscar o DNS: nslookup;
- Funciona como um banco de dados distribuído e hierárquico;
- Hierarquia de servidores:
	- Raiz - 13 servidores pelo mundo;
	- TDL (Domínios de alto nível, ex.: .com, .br);
	- Autoritativos (possuem registros DNS de uma organização);
	- Locais (caches próximos ao usuário).
- Processo: cliente consulta servidor local → raiz → TLD → autoritativo → retorna o IP.

![[Pasted image 20250820181357.png]]


## HTTP (HyperText Transfer Protocol)

- Protocolo padrão da Web (funciona no modelo requisição-resposta entre servidor e cliente);
- Versões: HTTP/1.0, HTTP/1.1, HTTP/2(Roda em cima do TCP) e HTTP/3 ou Quic (Roda em cima do UDP)
- Cada URL tem dois componentes básicos: um nome de hospedeiro(hostname - ex.: cisco.com) e um nome do caminho do objeto(index.html);
- Conexões não persistentes(HTTP/1.0): Cada par de requisição/resposta deve ser enviado por uma conexão TCP distinta, no máximo um objeto é enviado em cada conexão TCP.
- Conexões persistentes(HTTP/1.1 e HTTP/2): Todas as requisições e suas respostas são enviadas por uma mesma conexão TCP, múltiplos objetos podem ser enviados em uma mesma conexão.
- *handshake: processo inicial de comunicação entre dois dispositivos em uma rede* para estabelecer uma conexão confiável antes de começar a trocar os dados(3 vias - pedido de conexão, servidor responde, cliente envia confirmação).
- Modelos principais:
	- Requisição: GET, PUT, DELETE, POST, HEAD.
	- Resposta: 200 OK, 301 Moved Permanently, 400 Bad Request, 404 Not Found, 505 HTTP Version Not Supported.
- Cache Web: servidores proxy que armazenam cópias de páginas para agilizar acesso
- HTTPS: Versão mais segura do HTTP, usa criptografia  (TLS, SSL) e autenticação e porta TCP 443.