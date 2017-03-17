# RoadMap

##Geral
- [ ]  **Integração CMD**
- [ ]  Integração Área do Cidadão
- [ ]  Cartão de Avaliação de Episódios
- [ ]  Cartão do Testamento Vital
- [ ]  Cartão de Vacinas
- [ ]  Cartão Contactar CSP
- [ ]  Cartão Pessoa com Doença Rara
- [ ]  Medições de Saúde
- [ ]  Cartão Contactar Médico de Família
- [ ]  Cartão Taxas Moderadoras
- [ ]  Cartão dos Benefícios
- [ ]  Cartão das Alergias
- [ ]  Cartão da Medicação Crónica
- [ ]  Cartão de Emergência
- [ ]  Cartão Saúde Oral - Cheque Dentista
- [ ]  Cartão RCU2
- [ ]  Cartão eGuia Tratamento (push)
- [ ]  Cartão Europeu de Seguro de Doença (com Segurança Social)
- [ ]  Cartão do Dador (com IPST)
- [ ]  Cartão CIT
- [ ]  Cartão de Consultas (marcação CSP)
- [ ]  Cartão SIGA Cirurgias (consulta de LIC)
- [ ]  Cartão SIGA Cirurgias Consultas (estados das referenciações)
- [ ]  Cartão SIGA Cirurgia (vale cirurgico)
- [ ]  Cartão Posologia (eBIC)


##Macro Tasks
####HAPI.js
- [x] HAPI - Auth AMA CMD - Part1 - make request
- [x] +tests
- [ ] HAPI - Auth AMA CMD - Part2 - parse response
- [ ] +tests
- [ ] HAPI - Auth RSP - Part1 - Parse 1s request, send OTP + response
- [ ] +tests
- [ ] HAPI - Auth RSP - Part2 - Parse 2nd request + validate OTP
- [ ] +tests
- [ ] HAPI - auth-ces plugin (decrypt + verify client signature)
- [ ] +tests
- [ ] HAPI - response plugin (encrypt + sign server)
- [ ] +tests
- [ ] HAPI - request validation
- [ ] +tests
- [ ] HAPI - good consumer
- [ ] +tests

####HAPI.js - Dockerfile (Swarm)
- [ ] auth-cmd.ces.mysns.pt
- [ ] auth-rnu.ces.mysns.pt
- [ ] comm.ces.mysns.pt
- [ ] rnu.comm.ces.mysns.pt (internal - endpoint)
- [ ] rsp.comm.ces.mysns.pt (internal - endpoint)

####Azure DocumentDB - database creation (MongoDB)
- [ ] CmdAuthState
- [ ] PubKeys - Client PubKeys + Server PubKeys
- [ ] Comm configuration (dispatcher)
- [ ] LogDatabase (good + encrypted)

####Azure Key Vault - ServerKeys HSM (10 anos+ BYOK)
- [ ] Auth Key 
- [ ] Comm Key
- [ ] Log Key
- [ ] Client Sign Key
- [ ] RNU-Comm <KEYGEN></KEYGEN>
- [ ] RSP-Comm Key