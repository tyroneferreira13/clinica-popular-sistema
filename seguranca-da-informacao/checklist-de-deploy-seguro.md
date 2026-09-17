# Checklist de deploy seguro

Este checklist representa uma entrega prática da função de Segurança da Informação: uma lista de verificação que a equipe usaria, hipoteticamente, antes de colocar qualquer nova versão do sistema no ar, 
garantindo que nenhum cuidado básico de segurança fique esquecido.

**Antes do lançamento**
- [ ] Autenticação testada para os dois tipos de login (paciente e equipe)
- [ ] Permissões de acesso conferidas para cada perfil de usuário, incluindo testes de tentativa de acesso indevido, como um paciente tentando visualizar dados de outro
- [ ] Dados sensíveis protegidos conforme a classificação definida em classificacao-de-dados-e-controle-de-acesso.md
- [ ] Consentimento LGPD sendo corretamente registrado no cadastro
- [ ] Conferência de que dados de uma unidade não estão visíveis para outra unidade da rede
- [ ] Verificação de que lembretes e notificações enviados ao paciente não expõem informações sensíveis no próprio conteúdo da mensagem
- [ ] Verificação de que a fila de espera não expõe a posição ou os dados de outros pacientes aguardando
- [ ] Confirmação de que nenhum dado fictício ou de teste ficou esquecido no ambiente que simula produção
- [ ] Backup atualizado e testado antes de qualquer alteração significativa
- [ ] Plano de resposta a incidentes revisado e atualizado, incluindo confirmação de que Back-end, Banco de Dados e Front-end sabem quando devem ser acionados

**Durante o lançamento**
- [ ] Alguém disponível de cada função crítica (Back-end, Banco de Dados, Segurança) durante a janela de lançamento, mesmo que hipotético, para simular uma resposta rápida caso algo saia do esperado
- [ ] Comunicação avisando a equipe sobre o início do lançamento, evitando que outras alterações sejam feitas ao mesmo tempo

**Depois do lançamento**
- [ ] Verificação de que as permissões de acesso continuam funcionando como esperado após a atualização
- [ ] Revisão de eventuais falhas registradas logo após a liberação
- [ ] Confirmação de que a equipe está ciente do procedimento a seguir caso algum problema seja identificado nas primeiras horas após o lançamento
- [ ] Aprovação final assinada por mais de uma pessoa da equipe, reforçando que a decisão de lançar não dependeu de uma única pessoa
