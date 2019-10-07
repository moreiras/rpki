## Infraestrutura de chaves pública (PKI): conceitos e vocabulário

Uma infraestrutura de chaves públicas é uma estrutura, isto é, um conjunto de regras, políticas, procedimentos, hardware e software, que serve para relacionar **chaves públicas** a um determinado recurso. No caso do RPKI, em particular, esses recursos são os blocos de endereços IP e os ASN. Esse relacionamento é feito por uma Autoridade de Certificação (CA) por meio do registro e emissão de **certificados** criptográficos. 

### Criptografia usando chaves públicas

A técnica de criptografia utilizada em uma PKI é chamada de **criptografia assimétrica**. Ela envolve a criação de um par de chaves. Essas chaves são números com propriedades matemáticas especiais. A chave pública, como o próprio nome deixa claro, pode e deve ser divulgada publicamente. A chave privada deve ser mantida em segredo. A chave privada pode ser utilizada para assinar digitalmente documentos, ou criptografar os mesmos. A assinatura pode ser então verificada por terceiros, ou o documento pode ser descriptografado, usando a chave pública. O inverso também é possível, um documento pode ser assinado ou criptografado com a chave pública, podendo então a assinatura ser verificada, ou o mesmo descriptografado, com a chave privada.

### Certificados X.509

Um certificado criptográfico, em uma estrutura de chaves públicas, é basicamente um documento eletrônico, ou arquivo, que:
- contém uma chave pública;
- está associado a uma chave privada, par da chave pública que está no documento, a qual não faz parte do documento mas está sob os cuidados da organização responsável pelo mesmo;
- é assinado por uma chave privada, normalmente de uma outra organização denominada Autoridade de Certificação (CA), a qual faz parte de uma cadeia de certificação;
- pode ser também auto-assinado, pela própria chave privada que é par da chave pública contida no mesmo, sendo dessa forma a raiz de uma cadeia de certificação;
- contém informações sobre a localização do certificado da organização que o assinou, ou seja, da Autoridade de Certificação (CA), permitindo a obtenção do mesmo, seguindo a cadeia de certificação e possibilitando a validação da assinatura à partir da chave pública contida no certificado da CA;
- contém normalmente informações sobre a organização responsável pelo certificado;
- contém informações sobre recursos ou identidades vinculados ao certificado.

O **X.509** é um [padrão definido pela ITU-T](https://www.itu.int/ITU-T/recommendations/rec.aspx?rec=X.509) para certificados criptográficos. A [RFC 5280](https://tools.ietf.org/html/rfc5280) especifica como utilizar o X.509 na Internet. E, mais especificamente, a [RFC 3779](https://tools.ietf.org/html/rfc3779) define extensões para os certificados X.509 para que eles sejam capazes de relacionar uma lista de blocos de endereços IP, ou seja, de prefixos, ou uma lista de ASN, ao certificado.

Os **certificados X.509 são utilizados no RPKI**. Eles também são utilizados em muitos outros protocolos na Internet, por exemplo, no TLS/SSL, que é a base para o HTTPS, o protocolo seguro usado na Web. Eles são usados ainda em uma série de aplicações fora da Internet, por exemplo, para assinatura eletrônica de documentos.

### Certificados de Recurso (Resource Certificates) (RC)

Os certificados X.509 utilizados no RPKI são chamados genericamente de Resource Certificates (RC), ou Certificados de Recursos. Uma característica particular do RPKI, que é interessante destacar, é que os certificados não trazem informações sobre a entidade que os emite. Ou seja, um certificado emitido por um ISP vinculado aos seus blocos de endereço IP não contém o nome do ISP ou outras informações que possam identificá-lo. 

### Autoridade de Certificação (CA)

A **Autoridade de Certificação (CA)** é a entidade que assina os certificados, em uma infraestrutura de chaves públicas (PKI).

No RPKI, cada Regional Internet Registry (RIR) é uma Autoridade de Certificação (CA). Uma organização que obtem recursos de numeração do RIR gera para si própria um par de chaves e um certificado vinculado a tais recursos (RC). Esse certificado é assinado pelo RIR, que atua no papel CA. Essa mesma organização que obteve os recursos e teve o certificado assinado pelo RIR, pode atuar também como CA, assinando certificados gerados por seus clientes, vinculados aos recursos dos mesmos, ou assinando certificados chamados de End Entities (EE) que serão explicados mais à frente.

### Trusted Anchor (TA)

Em uma infraestrutura de chaves públicas, a Trusted Anchor (TA) é o topo da cadeia de certificação ou, dito de outra forma, a raiz da cadeia de certificação. Ou seja, é um certificado que é considerado, por definição, confiável. Sua chave pública é bem conhecida e considerada confiável em toda a cadeia de certificação. Normalmente um certificado TA tem uma longa validade, de até vários anos, e a chave privada desse certificado é armazenada offline, sendo usada apenas para reassiná-lo quando necessário. Esse certificado pode ser trocado de tempos em tempos, de forma programada, para aumentar a confiabilidade do sistema, ou pode ser trocado emergencialmente, se houver comprometimento (vazamento) da chave privada. 

No RPKI optou-se por não haver uma raiz única. Esta não é uma limitação técnica, mas uma escolha operacional, de governança da Internet, baseada em diversos critérios. Ou seja, na infraestrutura provida pelo RPKI não existe uma raiz única na cadeia de certificação, mas 5 certificados raiz diferentes, 5 TA diferentes, pertencentes respectivamente ao AFRINIC, ARIN, APNIC, LACNIC e RIPE. 

### Autoridade de Registro (RA)



### End Entities (EE)

### Ghostbusters

### ROA

### CRL




