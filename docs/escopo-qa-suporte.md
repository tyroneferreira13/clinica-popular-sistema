# Escopo de QA, Acessibilidade e Suporte ao Usuário

## 1. Objetivo

A área de QA, acessibilidade e suporte tem como objetivo verificar a qualidade da plataforma e se suas principais funções estão funcionando como deveriam.

Também será levado em conta a facilidade de uso do sistema, buscando evitar problemas e ajudar pacientes que tenham alguma dificuldade durante o uso.

---

## 2. O que será feito

Serão planejados testes para verificar o funcionamento da plataforma, principalmente nas funções mais importantes para os pacientes.

Também será analisado questões de acessibilidade e suporte ao usuário para que o sistema seja simples e facil de utilizar.

### 2.1 Planejamento dos testes

Os testes serão feitos pensando tanto no uso normal do sistema como em situações que podem causar erros.

Alguns pontos que serão testados:

- Agendamento de consultas;
- tentativa de agendar horários ocupados;
- cancelamento de consultas;
- visualização dos agendamentos;
- campos preenchidos de forma errada ou incompleta;
- lembretes das consultas;
- mensagens de confirmação e erro.

Caso algum problema seja encontrado ele deverá ser registrado e informado para a área responsável.

### 2.2 Testes de agendamento

Será verificado se o paciente consegue agendar uma consulta em um horário disponível e se o sistema impede a escolha de um horário que já esteja ocupado.

Também será verificado se o agendamento aparece corretamente e se o paciente recebe uma confirmação depois de concluir.

### 2.3 Testes de cancelamento

Será testado se uma consulta pode ser cancelada corretamente e se depois do cancelamento o horário fica disponível novamente.

Também será verificado se o paciente recebe uma confirmação de que sua consulta foi cancelada.

### 2.4 Mensagens e erros

Será verificado se as mensagens apresentadas pelo sistema são claras e faceis de entender.

Por exemplo caso o paciente esqueça de preencher um campo obrigatório, o sistema deverá informar oque precisa ser corrigido em vez de apresentar apenas um erro sem explicação.

### 2.5 Acessibilidade

A acessibilidade será analisada pensando principalmente na facilidade de utilização da plataforma.

Alguns pontos que serão observados:

- Textos fáceis de entender;
- botões com funções claras;
- campos dos formulários identificados;
- mensagens de erro compreensíveis;
- funções importantes fáceis de encontrar;
- informações que não dependam somente de cores.

### 2.6 Suporte ao usuário

O suporte terá como objetivo ajudar pacientes que tenham dúvidas ou problemas ao utilizar a plataforma.

Primeiro será identificado qual é a dificuldade do paciente. Caso seja apenas uma dúvida será fornecida uma orientação, se for um problema técnico ele será registrado e encaminhado para a área responsável.

---

## 3. Plano de Testes

Para verificar a qualidade da plataforma serão utilizados diferentes tipos de testes dependendo da situação.

### Teste Funcional

O teste funcional será utilizado para verificar se as principais funções da plataforma estão funcionando como deveriam.

Nesse teste será verificado por exemplo se o paciente consegue realizar um agendamento em um horário disponível, cancelar uma consulta e visualizar seus agendamentos corretamente.

### Teste de Validação

O teste de validação será utilizado principalmente nos campos preenchidos pelo usuário.

Será testado por exemplo oque acontece quando o paciente deixa um campo obrigatório vazio ou coloca alguma informação de forma incorreta. O sistema deverá informar o problema para que o usuário consiga corrigir.

### Teste Exploratório

O teste exploratório será feito utilizando a plataforma de forma mais livre, sem seguir apenas um caminho definido.

A ideia é navegar pelas funções do sistema, realizar diferentes ações e tentar encontrar erros ou situações que talvez não tenham sido previstas nos outros testes.

### Teste de Regressão

O teste de regressão será utilizado quando alguma alteração ou correção for feita na plataforma.

Depois da alteração serão testadas novamente funções que já estavam funcionando, como agendamento e cancelamento, para verificar se a mudança não acabou causando algum problema em outra parte do sistema.

---

## 4. Acessibilidade

Na parte de acessibilidade será verificado se a plataforma é simples de entender e utilizar pelos pacientes.

Os textos e informações devem ser claros, os botões precisam ter funções faceis de identificar e os campos dos formulários devem mostrar corretamente quais informações precisam ser preenchidas.

Também será observado se as mensagens de erro são compreensíveis e ajudam o paciente a entender oque aconteceu. As principais funções como agendamento e cancelamento devem ser fáceis de encontrar.

Outro ponto importante é evitar que informações importantes dependam somente de cores, já que alguns usuários podem ter dificuldades para diferenciar determinadas cores.

---

## 5. Roteiro de Suporte ao Paciente

O atendimento deverá seguir algumas etapas:

1. Identificar a dificuldade do paciente;
2. verificar se é uma dúvida ou problema do sistema;
3. orientar o paciente caso seja uma dúvida;
4. registrar o problema caso seja uma falha;
5. encaminhar para a área responsável quando necessario;
6. informar ao paciente sobre o encaminhamento.

---

## 6. Responsabilidades

### QA

- Planejar os testes;
- verificar as funções do sistema;
- identificar e registrar falhas;
- informar os problemas encontrados.

### Acessibilidade

- Verificar se as informações são claras;
- analisar a facilidade de uso;
- verificar possíveis dificuldades de acessibilidade.

### Suporte

- Ajudar pacientes com dificuldades;
- registrar problemas relatados;
- encaminhar problemas técnicos.

---

## 7. Resultado Esperado

O resultado esperado é que os testes ajudem a identificar possíveis problemas da plataforma antes que eles prejudiquem os usuários.

A acessibilidade e o suporte também devem ajudar para que o sistema seja mais simples de usar e que os pacientes tenham ajuda caso encontrem alguma dificuldade.
