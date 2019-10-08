## Infraestrutura de chaves pública (PKI): conceitos e vocabulário

Uma infraestrutura de chaves públicas (Public Key Infrastructure, PKI) é uma estrutura que serve para relacionar **chaves públicas** a um determinado recurso, ou recursos. Por "estrutura" entendemos que uma PKI consiste em regras, procedimentos, políticas, e o conceito engloba também todo hardware e software envolvidos. Uma PKI envolve entidades emitindo e assinando **certificados** criptográficos, que são os documentos digitais que carregam as chaves públicas e informações dos recursos relacionados a elas. Essas entidades são organizadas em uma hierarquia, de forma que é possível realizar a validação das informações. 

No caso do RPKI, em particular, os recursos vinculados às chaves criptográficas, ou certificados, são os blocos de endereços IP (IPv6 e IPv4) e os ASN. 

Vamos procurar a seguir desvendar o vocabulário e entender importantes conceitos aplicados a infraestruturas de chaves públicas em geral e ao RPKI (Resource Public Key Infrastructure), em particular:

- [Criptografia assimétrica e chaves públicas](#criptografia-assimétrica-e-chaves-públicas)
- [Certificados X.509](#certificados-x-509)
- [Certificados de Recurso (Resource Certificates, RC)](#certificados-de-recurso-resource-certificates-rc)
- [Autoridade de Certificação (Certification Authority, CA)](#autoridade-de-certificação-certification-authority-ca)
- [Trust Anchor (TA)](#trust-anchor-ta)
- [Autoridade de Registro (Registration Authority, RA)](#autoridade-de-registro-registration-authority-ra)
- [CRL](#crl)
- [End Entities (EE)](#end-entities-ee)
- [ROA](#roa)
- [Ghostbusters](#ghostbusters)


### Criptografia assimétrica e chaves públicas

A técnica de criptografia utilizada em infraestrutura de chaves públicas (PKI) é chamada de **criptografia assimétrica**. A criptografia assimétrica envolve a criação de um par de chaves, uma pública, outra privada. Essas chaves são simplesmente números com propriedades matemáticas especiais. A chave pública, como o próprio nome deixa claro, pode e deve ser divulgada publicamente. A chave privada deve ser mantida em segredo. 

A chave privada pode ser utilizada para assinar digitalmente documentos, ou criptografar os mesmos. A assinatura pode ser então verificada por terceiros, ou o documento pode ser descriptografado, usando a chave pública. 

O inverso também é possível, um documento pode ser assinado ou criptografado com a chave pública, podendo então a assinatura ser verificada, ou o mesmo descriptografado, com a chave privada.

Em uma infraestrutura de chaves públicas, estas (as chaves públicas) justamente têm um papel especial, o que deveria ser óbvio, visto que dão o nome para a estrutura. As chaves públicas são divulgadas em documentos chamados **certificados**, que são por sua vez assinados por chaves privadas e organizados em uma estrutura hierárquica. O certificado "pai", na cadeia de validação, ou mais especificamente a chave pública que está contida nele, é usada para validar a assinatura do certificado "filho" (que foi assinado pela chave privada do "pai"). Dessa forma é possível seguir uma cadeia de confiança para a validação de um determinado recurso, vinculado a um certificado. 

[Voltar](#infraestrutura-de-chaves-pública-pki-conceitos-e-vocabulário)


### Certificados X.509

Um certificado criptográfico, em uma estrutura de chaves públicas, é basicamente um documento eletrônico, ou arquivo, que:

- contém uma chave pública;
- contém informações sobre recursos ou identidades vinculados ao certificado (ou seja, à chave pública).
- está associado a uma chave privada, par da chave pública que está no documento, a qual não faz parte do documento mas está sob os cuidados da organização responsável pelo mesmo (essa chave privada é usada para assinar documentos e a validade dessa assinatura pode ser verificada justamente usando a chave pública contida no certificado);
- é assinado por uma chave privada, normalmente de uma outra organização denominada Autoridade de Certificação (CA), a qual faz parte de uma cadeia de certificação;
- pode ser também auto-assinado, pela própria chave privada que é par da chave pública contida no mesmo, sendo dessa forma a raiz de uma cadeia de certificação, chamada de Trut Anchor (TA);
- contém informações sobre a localização do certificado da organização que o assinou, ou seja, da Autoridade de Certificação (CA), permitindo a obtenção do mesmo, seguindo a cadeia de certificação e possibilitando a validação da assinatura à partir da chave pública contida no certificado da CA;
- contém normalmente informações sobre a organização responsável pelo certificado (nos certificados usados no RPKI, por especificação, não há essa informação);
- tem uma validade pré estabelecida, com data de início e fim;

O **X.509** é um [padrão definido pela ITU-T](https://www.itu.int/ITU-T/recommendations/rec.aspx?rec=X.509) para certificados criptográficos. A [RFC 5280](https://tools.ietf.org/html/rfc5280) especifica como utilizar o X.509 na Internet. E, mais especificamente, a [RFC 3779](https://tools.ietf.org/html/rfc3779) define extensões para os certificados X.509 para que eles sejam capazes de relacionar uma lista de blocos de endereços IP, ou seja, de prefixos, ou uma lista de ASN, ao certificado. As RFCs [6487](https://tools.ietf.org/html/rfc6487) e [7318](https://tools.ietf.org/html/rfc7318) detalham a forma de usar os certificados X.509 para representar blocos de endereços IP ou ASN na Internet.

Os **certificados X.509 v.3 são utilizados no RPKI**. Eles também são utilizados em muitos outros protocolos na Internet, por exemplo, no TLS/SSL, que é a base para o HTTPS, o protocolo seguro usado na Web. Eles são usados ainda em uma série de aplicações fora da Internet, por exemplo, para assinatura eletrônica de documentos.

[Voltar](#infraestrutura-de-chaves-pública-pki-conceitos-e-vocabulário)


### Certificados de Recurso (Resource Certificates, RC)

Os certificados X.509 utilizados no RPKI são chamados genericamente de Resource Certificates (RC), ou Certificados de Recursos. Uma característica particular do RPKI, que é interessante destacar, é que os certificados não trazem informações sobre a entidade que os emite. Ou seja, um certificado emitido por um ISP vinculado aos seus blocos de endereço IP não contém o nome do ISP ou outras informações que possam identificá-lo. 

[Voltar](#infraestrutura-de-chaves-pública-pki-conceitos-e-vocabulário)


### Autoridade de Certificação (Certification Authority, CA)

A **Autoridade de Certificação** (Certification Authority, CA) é a entidade que assina os certificados, em uma infraestrutura de chaves públicas (PKI).

No RPKI, cada Regional Internet Registry (RIR) é uma Autoridade de Certificação (CA). Uma organização qualquer que obtem recursos de numeração (IPv6, IPv4, ASN) do RIR gera para si própria um par de chaves e um certificado vinculado a tais recursos (RC). Esse certificado é assinado pelo RIR, que fazendo isso atua no papel CA. 

Essa mesma organização que obteve os recursos e teve o certificado assinado pelo RIR, pode atuar também como CA, assinando certificados gerados por seus clientes, vinculados aos recursos dos mesmos, ou assinando certificados chamados de End Entities (EE) que estão relacionados a utilização dos recursos vinculados aos mesmos e serão explicados mais à frente.

[Voltar](#infraestrutura-de-chaves-pública-pki-conceitos-e-vocabulário)


### Trust Anchor (TA)

Em uma infraestrutura de chaves públicas, a Trust Anchor (TA) é o topo da cadeia de certificação ou, dito de outra forma, a raiz da cadeia de certificação. Ou seja, é um certificado autoassinado que é considerado, por definição, confiável. Sua chave pública é bem conhecida e considerada confiável em toda a cadeia de certificação. 

Normalmente um certificado TA tem uma longa validade, de até vários anos, e a chave privada desse certificado é armazenada offline, sendo usada apenas para reassiná-lo quando necessário. Esse certificado pode ser trocado de tempos em tempos, de forma programada, para aumentar a confiabilidade do sistema, ou pode ser trocado emergencialmente, se houver comprometimento (vazamento) da chave privada. 

No RPKI optou-se por não haver uma raiz única. Esta não é uma limitação técnica, mas uma escolha operacional, de governança da Internet, baseada em diversos critérios. Ou seja, na infraestrutura provida pelo RPKI não existe uma raiz única na cadeia de certificação, mas 5 certificados raiz diferentes, 5 TA diferentes, pertencentes respectivamente ao AFRINIC, ARIN, APNIC, LACNIC e RIPE. 

[Voltar](#infraestrutura-de-chaves-pública-pki-conceitos-e-vocabulário)


### Autoridade de Registro (Registration Authority, RA)

Em uma infraestrutura de chaves públicas, a organização responsável por receber a requisição para a assinatura de um certificado, autenticando a entidade requisitante, verificando as informações necessárias, e autorizando a certificação, é chamada de **Autoridade de Registro** (Registration Authority, RA).

No RPKI os RIRs e NIRs assumem também a função de Autoridade de Registro. Isso é natural, visto que as organizações que têm os recursos alocados já tem acesso a um sistema onde os gerenciam, e nesse sistema já há as funções de autenticação e autorização.

Por sua vez, as organizações que têm recursos alocados pelos RIRs ou NIRs diretamente, podem também emitir e assinar certificados para si próprias ou para seus clientes, sendo responsáveis também pela autenticação e autorização nesses casos, operando como Autoridades de Registro.

No RPKI, pois, as funções de Autoridade de Certificação (Certification Authority, CA) e Autoridade de Registro (Registration Authority, RA):
- estão presentes em vários pontos da cadeia de certificação;
- em um determinado ponto da cadeia de certificação são normalmente executadas pela mesma organização, mas apesar disso são funções diferentes, ou seja, são dois "papéis" diferentes sendo executados pela mesma entidade.

O RIR ou NIR, no papel de Autoridade de Registro (RA), é quem recebe as requisições, verifica a identidade de quem está fazendo a solicitação e se ela é válida. Por exemplo, autentica o usuário do ISP em seu sistema e verifica se os blocos IP vinculados ao certificado estão realmente alocados para o mesmo. Estando tudo certo, autoriza a assinatura ou emissão do certificado. Então o próprio RIR ou NIR, agora no papel de Autoridade de Certificação (CA), assina ou emite o certificado, usando sua chave privada. A organização responsável (o LACNIC, ou o NIC.br, por exemplo) é a mesma, mas executando papéis distintos, funções distintas.

[Voltar](#infraestrutura-de-chaves-pública-pki-conceitos-e-vocabulário)


### CRL

[Voltar](#infraestrutura-de-chaves-pública-pki-conceitos-e-vocabulário)


### End Entities (EE)

[Voltar](#infraestrutura-de-chaves-pública-pki-conceitos-e-vocabulário)


### ROA

[Voltar](#infraestrutura-de-chaves-pública-pki-conceitos-e-vocabulário)


### Ghostbusters

[Voltar](#infraestrutura-de-chaves-pública-pki-conceitos-e-vocabulário)




