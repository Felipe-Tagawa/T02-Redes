
### Endereçamento Físico (MAC ou camada 2 ou LAN)

-  Associado ao adaptador de rede(interface física);
-  Independe da rede que se encontra, é sempre fixo;
-  Constituído de 48 bits, representados no formato hexadecimal.

### Endereçamento IP

- Endereço Lógico, atribuído pelo administrador da rede
- IPV4: 32bits representados no formato decimal com pontos
	Ex.: 192.168.15.180
	2^32 endereços 
- IPV6: 128bits

- IPV4 - Formado por duas partes: Net-Id(bits mais significativos) e Host-Id (bits menos significativos)
- Net-Id identificam a rede


*/24. = 255.255.255.0 = 11111111.11111111.11111111.0 (/24 - primeiros 24 bits mais significativos igual a 1 são os que identificam a rede) - máscara*

- Endereços de Rede e de Broadcast - não podem ser atribuídos a nenhum dispositivo de rede.
- Endereço de Rede - identifica a rede e bits Host_Id = 0 todos (.0 = 00) 
- Endereço de Broadcast - permite o envio de pacotes para todos os hosts (disponíveis) de uma rede específica e bits Host_Id = todos (.3 = 11)

Gateway Padrão - Ponto de acesso padrão

#### Endereços Privados

- NAT(Network Adress Translation)
- **Privados:** `10.x.x.x`, `172.16–31.x.x`, `192.168.x.x` (não acessam a internet diretamente).
    
- **Públicos:** todos os outros (endereços globais, roteáveis na internet).