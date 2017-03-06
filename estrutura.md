#Estrutura

## Segurança Fisica e Lógica {#seguranca}

### Medidas de segurança física
A informação do cidadão ficará residente nas bases de dados locais e centrais notificadas junto da CNPD em processos próprios.

Toda a informação adicional, ficará guardada localmente de forma encriptada (por AES 256), no dispositivo móvel do cidadão. 
A meta informação do Servidor CeS será guardada usando algoritmos de criptografia RSA 2048 (armazenados em HSM – hardware security module - FIPS 140-2 Level 2) cujos requisitos de segurança e necessidades de escalabilidade de produto são assegurados pela opção de cloud Azure Key Vault, que contempla níveis de serviço (SLA) não só a nível de disponibilidade como a nível de cibersegurança.

A solução Azure tem inúmeros requisitos de segurança que, para serem implementados num datacenter SPMS implicavam um custo de dimensões não suportáveis nem justificáveis, considerando a criticidade da informação aí alojada (recordamos que a informação de saúde do Cidadão, não fica residente nesta base de dados, apenas nos dispositivos móveis encriptada e nas bases de dados centrais e locais já existentes e notificadas). 

### Medidas de segurança lógica
A comunicação realizada entre o dispositivo móvel e o servidor CeS usa o protocolo HTTPS.
A comunicação realizada entre a base de dados dos vários sistemas de informação (centrais e locais) e o Servidor CeS usa o protocolo HTTPS e toda a informação trocada é encriptada e assinada digitalmente usando os algoritmos de encriptação RSA (2048 bit) e AES (256 bit).
Para a encriptação usando o algoritmo RSA, o par de chaves de encriptação é do tipo HSM (hardware security module - FIPS 140-2 Level 2), cujos requisitos de segurança e necessidades de escalabilidade de produto, levaram a uma opção de cloud Azure Key Vault.
O Servidor CeS não guarda qualquer tipo de informação relativa aos cartões do Cidadão, mas guarda informação de registo (logs encriptados) para diagnóstico de problemas de funcionamento da aplicação, com tempo de conservação máximo de 1 mês. 

