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

Será utilizado um checklist para organizar essas verificações.

### 2.6 Suporte ao usuário

O suporte terá como objetivo ajudar pacientes que tenham dúvidas ou problemas ao utilizar a plataforma.

Primeiro será identificado qual é a dificuldade do paciente. Caso seja apenas uma dúvida será fornecida uma orientação, se for um problema técnico ele será registrado e encaminhado para a área responsável.

---

## 3. Plano de Testes

| Teste | Situação | Resultado esperado |
|---|---|---|
| 01 | Agendar em horário disponível | Consulta agendada |
| 02 | Agendar em horário ocupado | Sistema impede o agendamento |
| 03 | Cancelar uma consulta | Consulta cancelada |
| 04 | Visualizar agendamentos | Agendamentos aparecem corretamente |
| 05 | Deixar campo obrigatório vazio | Sistema informa o problema |
| 06 | Cancelar uma consulta | Horário fica disponível novamente |
| 07 | Consulta próxima | Paciente recebe o lembrete |

---

## 4. Checklist de Acessibilidade

- [ ] Textos e informações são claros;
- [ ] botões são fáceis de identificar;
- [ ] campos possuem identificação;
- [ ] mensagens de erro são compreensíveis;
- [ ] funções principais são fáceis de encontrar;
- [ ] informações importantes não dependem apenas de cores;
- [ ] agendamento e cancelamento são simples de utilizar.

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
- utilizar o checklist de acessibilidade.

### Suporte
- Ajudar pacientes com dificuldades;
- registrar problemas relatados;
- encaminhar problemas técnicos.

---

## 7. Resultado Esperado

O resultado esperado é que os testes ajudem a identificar possíveis problemas da plataforma antes que eles prejudiquem os usuários.

A acessibilidade e o suporte também devem ajudar para que o sistema seja mais simples de usar e que os pacientes tenham ajuda caso encontrem alguma dificuldade.
