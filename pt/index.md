# RPKI

Na Internet usamos o protocolo de roteamento BGP (Border Gateway Protocol). Colocando em termos simples, o BGP é o conjunto de regras de comunicação usados pelos roteadores de borda das redes, dos Sistemas Autônomos, para trocar informações sobre os blocos de endereços IP (IPv6 e IPv4) que estão sob responsabilidade de cada um. Com o BGP, cada rede informa à outra todos os IPs sob sua responsabilidade e também recebe a informação correspondente das redes vizinhas. A informação recebida de um vizinho também é passada para outro. Essa troca de informações acontece em escala global e permite que cada roteador envolvido crie para si um mapa de toda a Internet. Esse mapa é chamado de Tabela de Roteamento Global, ou Tabela de Roteamento BGP. O BGP é um dos pilares tecnológicos, um dos protocolos mais básicos, sobre o qual se baseia a Internet.

Apesar de sua grande importância, o BGP é um protocolo que não é, por si só, seguro. Isto é, o BGP não tem, de forma automática, mecanismos para validação das informações que envia ou recebe. O que um roteador informa ao outro é tomado como verdade. Isso gera a necessidade de mecanismos de proteção, como filtros, baseados em informações ou bases de dados externos. A 

## O que é um PKI?


## Para que serve o RPKI?

## Para que NÃO SERVE o RPKI? 

## Os principais componentes

### Protocolo UP-Down
