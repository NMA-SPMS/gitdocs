# Funcionamento

## Recolha de Dados {#dados}

Para ativação da MySNS Carteira o cidadão regista na aplicação o Número de SNS + Data de Nascimento + Número de Telemóvel.

A informação do cidadão, quer relativa a dados pessoais, quer a dados de saúde, disponibilizada através de cartões, está residente nas bases de dados locais e centrais notificadas junto da CNPD em processos próprios.

Toda a restante informação fica guardada **localmente** de forma encriptada, no dispositivo móvel do Cidadão.

## Comunicação e Interconexões de Dados{#comunicacao}

A MySNS Carteira poderá receber informação das várias bases de dados de informação de saúde, devidamente notificadas junto da CNPD - Comissão Nacional de Protecção de Dados em processos próprios.

A comunicação feita entre o dispositivo móvel e o servidor MySNS Carteira é feita usando o protocolo **HTTPS**.

A comunicação feita entre a base de dados dos vários sistemas de informação (centrais e locais) e o Servidor MySNS Carteira é feita usando o protocolo HTTPS e toda a informação trocada é ainda encriptada e assinada digitalmente usando os algoritmos de encriptação **[RSA (2048 bit)](https://www.emc.com/emc-plus/rsa-labs/standards-initiatives/pkcs-rsa-cryptography-standard.htm)** e **[AES (256 bit)](http://aesencryption.net/)**. 


Para a encriptação usando o algoritmo RSA, o par de chaves de encriptação é do tipo HSM (hardware security module - FIPS 140-2 Level 2), cujos requisitos de segurança e necessidades de escalabilidade de produto, levaram a uma opção de cloud [Azure Key Vault](https://azure.microsoft.com/en-us/services/key-vault).


O Servidor MySNS Carteira não guarda qualquer tipo de informação relativa aos cartões do cidadão, guarda apenas  informação de registo (logs encriptados) para diagnóstico de problemas de funcionamento da aplicação, com tempo de conservação máximo de 1 mês e está alojado na cloud.


A informação será guardada localmente no dispositivo móvel do Cidadão (encriptada) cabendo a este, de forma discricionária, apagá-la quando achar conveniente.
Relativamente ao servidor MySNS Carteira, conforme já referido no ponto de comunicação e interconexões de dados, é apenas guardada meta informação (enquanto o cidadão tiver a MySNS Carteira ativa) e logs encriptados para deteção de problemas, no **prazo máximo de um mês**.

O direito de acesso aos dados recolhidos no âmbito da aplicação MySNS Carteira é efetuado na [SPMS – Serviços Partilhados do Ministério do Saúde, E.P.E.](https://spms.min-saude.pt)
O acesso aos dados dos cartões disponibilizados através da MySNS Carteira continua a ser exercido junto da instituição de saúde onde o titular dos dados está inscrito, ou no caso de dados da saúde, por intermédio de médico escolhido pelo titular dos dados.
