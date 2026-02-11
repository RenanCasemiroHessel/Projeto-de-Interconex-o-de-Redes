# Projeto de Interconexão de Redes

Trabalho da disciplina Laboratório de Redes, com foco em projeto de sub-redes, VLANs, serviços de rede e roteamento dinâmico utilizando o Cisco Packet Tracer.

## Objetivo

Elaborar e implementar um projeto de interconexão de redes contemplando segmentação lógica, endereçamento IP, serviços de rede essenciais e roteamento entre múltiplas LANs em um ambiente simulado.

## Topologia e Redes

O projeto é composto por três LANs principais e enlaces seriais entre roteadores.

- LAN1 (rede amarela): 192.168.10.0/24, segmentada em 3 VLANs:
  - VLAN 10 – Admin
  - VLAN 20 – Vendas
  - VLAN 30 – TI
- LAN2 (rede azul): 192.168.20.0/24, dividida em:
  - Sub-rede 01: suporte para 110 hosts
  - Sub-rede 02: suporte para 31 hosts
- LAN3 (rede verde): 192.168.30.0/24, única sub-rede, com rede cabeada e rede sem fio via access point.

Enlaces entre roteadores (interfaces seriais):
- R1–R2: 192.168.1.0/30  
- R2–R3: 192.168.2.0/30  
- R1–R3: 192.168.3.0/30  

## Equipamentos

Conforme especificado no enunciado:

- LAN1:
  - 1 switch Cisco 2960
  - 6 PCs (2 em cada VLAN)
- LAN2:
  - 2 switches Cisco 2960
  - 4 PCs (2 em cada sub-rede)
  - 2 servidores (HTTP e DNS na sub-rede menor)
- LAN3:
  - 1 switch Cisco 2960
  - 1 access point HomeRouter PT-AC
  - 4 PCs (rede cabeada)
  - 3 laptops (Wi-Fi)
  - 1 servidor DHCP (rede cabeada)

## Serviços Implementados

- VLANs:
  - Criação das VLANs 10, 20 e 30 no switch da LAN1 via CLI.
  - Configuração de interfaces de acesso para cada VLAN e subinterfaces no roteador (router-on-a-stick) para roteamento entre VLANs.
- DHCP (LAN3):
  - Servidor DHCP configurado para entregar IP, máscara, gateway e DNS automaticamente para hosts cabeados e laptops via AP.
- HTTP (LAN2):
  - Servidor HTTP configurado com página index.html acessível a partir de qualquer LAN via navegador do Packet Tracer.
- DNS (LAN2):
  - Servidor DNS configurado com registros necessários para resolução de nomes (incluindo o nome utilizado para acessar o servidor web), com todos os dispositivos das três LANs usando este servidor.
- ACLs (controle de acesso):
  - ACL configurada para permitir que LAN3 acesse apenas LAN2 e bloquear qualquer tráfego originado em LAN3 com destino à LAN1.
- Segurança Wi-Fi:
  - Access point configurado com WPA2-PSK para autenticação dos três laptops da LAN3.

## Endereçamento IP

- LAN1: 192.168.10.0/24, com divisão lógica via VLAN e endereçamento estático nos PCs.
- LAN2: 192.168.20.0/24, subdividida em duas sub-redes para suportar 110 e 31 hosts respectivamente, com endereçamento estático em PCs e servidores.
- LAN3: 192.168.30.0/24, única sub-rede, com DHCP para todos os hosts.
- Enlaces seriais entre roteadores com redes /30 específicas (192.168.1.0/30, 192.168.2.0/30, 192.168.3.0/30).

No relatório em PDF, para cada sub-rede devem ser apresentados: máscara, prefixo, primeiro e último endereços válidos e broadcast.

## Roteamento

- Protocolo de roteamento dinâmico: RIP versão 2.
- Configuração realizada via CLI em todos os roteadores, anunciando as redes LAN (10, 20, 30) e os enlaces seriais (/30) para garantir conectividade total entre as sub-redes permitidas.
## Testes Realizados

- Conectividade:
  - Testes de ping entre todos os dispositivos das LANs de acordo com as regras de ACL (bloqueio LAN3 → LAN1).
- HTTP:
  - Acesso à página index.html do servidor HTTP a partir de terminais nas três LANs, utilizando o Web Browser do Packet Tracer.
- DHCP:
  - Verificação de recebimento automático de IP, gateway e DNS pelos hosts da LAN3.
- DNS:
  - Resolução de nomes para o servidor web e outros registros configurados, a partir de dispositivos em todas as LANs.

## Como Executar o Projeto

1. Abrir o arquivo `.pkt` no Cisco Packet Tracer (versão compatível com a usada na disciplina).
2. Aguardar a inicialização dos dispositivos e, se necessário, emitir alguns pings para popular as tabelas de roteamento via RIP.  
3. Em um PC de qualquer LAN, abrir a aba Desktop → Web Browser e acessar a URL configurada (index.html) para validar o serviço HTTP.
4. Em um host da LAN3, verificar se o IP é atribuído automaticamente (Desktop → IP Configuration → DHCP).  
5. Testar pings entre hosts de diferentes LANs, validando as permissões/negações impostas pelas ACLs.

## Referência dos requisitos do projeto

[CE5320_Projeto de sub-redes_2025_2_v1.pdf](https://github.com/user-attachments/files/25246603/CE5320_Projeto.de.sub-redes_2025_2_v1.pdf)]
