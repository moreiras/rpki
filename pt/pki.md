## Infraestrutura de chaves pública (PKI): conceitos e vocabulário

Uma infraestrutura de chaves públicas é uma estrutura, isto é, um conjunto de regras, políticas, procedimentos, hardware e software, que serve para relacionar **chaves públicas** a um determinado recurso. No caso do RPKI, em particular, esses recursos são os blocos de endereços IP e os ASN. Esse relacionamento é feito por uma Autoridade de Certificação (CA) por meio do registro e emissão de **Certificados** criptográficos. 

### Criptografia usando chaves públicas

A técnica de criptografia utilizada em uma PKI é chamada de criptografia assimétrica. Ela envolve a criação de um par de chaves. Essas chaves são números com propriedades matemáticas especiais. A chave pública, como o próprio nome deixa claro, pode e deve ser divulgada publicamente. A chave privada deve ser mantida em segredo. A chave privada pode ser utilizada para assinar digitalmente documentos, ou criptografar os mesmos. A assinatura pode ser então verificada por terceiros, ou o documento pode ser descriptografado, usando a chave pública. O inverso também é possível, um documento pode ser assinado ou criptografado com a chave pública, podendo então a assinatura ser verificada, ou o mesmo descriptografado, com a chave privada.

### X.509

O X.509 é um [padrão definido pela ITU-T](https://www.itu.int/ITU-T/recommendations/rec.aspx?rec=X.509). A [RFC 5280](https://tools.ietf.org/html/rfc5280) especifica como utilizar o X.509 na Internet. E, mais especificamente, a [RFC 3779](https://tools.ietf.org/html/rfc3779) especifica extensões para o X.509 para que eles sejam capazes de relacionar uma lista de blocos de endereços IP, ou seja, de prefixos, ou uma lista de ASNs, ao certificado.

Os certificados X.509 são utilizados no RPKI. Eles também são utilizados em muitos outros protocolos na Internet, por exemplo, no TLS/SSL, que é a base para o HTTPS, o protocolo seguro usado na Web. Eles são usados ainda em uma série de aplicações fora da Internet, por exemplo, para assinatura eletrônica de documentos.

Um certificado X.509 pode ser assinado por uma Autoridade de Certificação (CA), ou pode ser auto-assinado.


### Autoridade de Certificação (CA)

### Autoridade de Registro (RA)

### End Entities (EE)

### Ghostbusters

### ROA

### CRL




