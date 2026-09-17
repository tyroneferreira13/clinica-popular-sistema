**Projeto:** Plataforma de Gerenciamento de Clínicas

**Cliente:** Rede Cuidar+

**Responsável:** Cristian (Banco de Dados)

**Data:** Setembro de 2026

---

## Índice

1. [Objetivo](#1-objetivo)
2. [Entidades e Estrutura de dados](#2-entidades-e-estrutura-de-dados)
3. [Controle de acesso por tipo de login](#3-controle-de-acesso-por-tipo-de-login)
4. [Integridade e Consistência dos dados](#4-integridade-e-consistência-dos-dados)
5. [Backup e Histórico de alterações](#5-backup-e-histórico-de-alterações)
6. [Relatórios básicos de gestão](#6-relatórios-básicos-de-gestão)
7. [Suporte a múltiplas unidades](#7-suporte-a-múltiplas-unidades)
8. [Justificativa do banco relacional](#8-justificativa-do-banco-relacional)
9. [Divisão de responsabilidades](#9-divisão-de-responsabilidades)
10. [Resultado esperado](#10-resultado-esperado)
11. [Riscos caso a função não fosse considerada](#11-riscos-caso-a-função-não-fosse-considerada)

---

## 1. Objetivo

Estruturar e manter a base de dados da plataforma da Solutech, garantindo que todas as informações da Rede Cuidar+ pacientes, funcionários, agendamentos, horários e histórico de atendimentos, fiquem armazenadas de forma organizada, íntegra e acessível para as demais áreas do sistema (front-end e back-end).

> **Objetivo direto:** eliminar o problema relatado pela rede de clínicas, dados espalhados de forma desorganizada.

---

## 2. Entidades e Estrutura de dados

### 2.1 Funcionários e Pacientes

| Entidade | Dados armazenados | Vínculo obrigatório |
|----------|-------------------|----------------------|
| **Funcionário** | Nome, cargo/função (recepção, profissional de saúde etc.) e permissões de acesso ao sistema | Vinculado aos agendamentos pelos quais é responsável, permitindo montar sua agenda individual |
| **Paciente** | Nome, contato (telefone/e-mail), data de nascimento e demais dados de cadastro | Vinculado ao seu próprio histórico de agendamentos e resultados, sem se misturar com o de outro paciente |

### 2.2 Agendamentos

| Campo obrigatório | Detalhe |
|--------------------|---------|
| Data e horário | Momento do atendimento |
| Paciente | Quem será atendido |
| Funcionário responsável | Quem realizará o atendimento |
| Tipo de procedimento | Serviço a ser prestado |
| Status | `confirmado` \| `pendente` \| `em andamento` \| `concluído` \| `cancelado` |

O status é utilizado para determinar quais informações são exibidas na tela do paciente e na do funcionário.

> **Regra de integridade crítica:** dois agendamentos não podem ocupar o mesmo horário para o mesmo profissional.

### 2.3 Disponibilidade de Horários

-  Tabela de horários disponíveis por funcionário/profissional, para o sistema saber quando é possível marcar uma nova consulta.
-  Atualização automática da disponibilidade sempre que um agendamento for **criado**, **remarcado** ou **cancelado**.

### 2.4 Histórico e Resultados de procedimentos

Para cada procedimento realizado, devem ser armazenadas as seguintes informações:

| Informação | Descrição |
|------------|-----------|
| Paciente | A quem o procedimento está vinculado |
| Data e horário | Momento da realização |
| Funcionário responsável | Quem executou o atendimento |
| Tipo de procedimento | Procedimento realizado |
| Status | Indica se o procedimento foi concluído |
| Resultado/observações | Informações relevantes registradas pelo funcionário |

-  **Paciente:** pode visualizar o resultado e as observações disponibilizadas em sua área do sistema, após a conclusão do procedimento.
-  **Funcionário:** pode registrar ou consultar essas informações de acordo com suas permissões.

>  Resultados e observações devem permanecer vinculados ao respectivo atendimento, evitando que informações de diferentes procedimentos se misturem.

### 2.5 Fila de espera

Estrutura para registrar pacientes que não encontraram horário disponível e desejam aguardar uma vaga.

| Campo | Descrição |
|-------|-----------|
| Paciente | Quem está na fila |
| Unidade | Clínica desejada |
| Especialidade | Tipo de atendimento buscado |
| Profissional desejado | Preferência de funcionário |
| Preferência de data/horário | Janela desejada pelo paciente |
| Status da solicitação | Situação atual do pedido |

>  Quando surgir uma vaga compatível, o sistema pode usar essas informações para notificar o paciente.

### 2.6 Consentimento (LGPD)

O banco deve armazenar o registro de consentimento do paciente para uso e tratamento de seus dados.

| Campo | Descrição |
|-------|-----------|
| Data e hora do consentimento | Momento em que foi registrado |
| Versão dos termos/política aceita | Rastreabilidade de qual versão foi consentida |
| Status do consentimento | Situação atual (aceito, revogado etc.) |

>  Mantém evidências que auxiliam na demonstração de conformidade com a LGPD.

---

## 3. Controle de acesso por tipo de login

O sistema deve separar as informações conforme o tipo de usuário, garantindo que cada pessoa visualize apenas o necessário para sua função.

| Perfil | Acesso permitido |
|--------|-------------------|
| **Paciente** | Seus dados cadastrais, seus agendamentos, status dos procedimentos, histórico de atendimentos e resultados/observações disponíveis para visualização |
| **Funcionário (padrão)** | Agendamentos e informações necessárias para os atendimentos sob sua responsabilidade |
| **Funcionário (permissão ampliada)** | Dependendo do cargo/nível de permissão, agendamentos de toda a clínica |

>  Um paciente nunca acessa dados de outro paciente, e um funcionário nunca visualiza informações fora de suas responsabilidades.

---

## 4. Integridade e Consistência dos dados

O sistema deve possuir regras que garantam que os dados armazenados sejam corretos, consistentes e não duplicados:

- [ ] Evitar duplicidade de cadastros de pacientes, identificando pacientes já existentes
- [ ] Garantir que todo agendamento esteja vinculado a paciente, funcionário responsável, data, horário e tipo de procedimento
- [ ] Impedir a criação de agendamentos sem os dados obrigatórios
- [ ] Garantir que dois agendamentos não ocupem o mesmo horário para o mesmo profissional
- [ ] Manter relacionamentos claros entre as informações do sistema

**Estrutura lógica dos dados:**

```
Paciente → Agendamento → Data/Horário → Funcionário → Procedimento → Resultado
```

> Essa organização evita informações "soltas" ou sem vínculo com um paciente ou atendimento específico, facilitando consulta, atualização e manutenção.

---

## 5. Backup e Histórico de alterações

O sistema deve possuir mecanismos básicos para proteger os dados contra perda, exclusão acidental ou falhas, especialmente por envolver histórico de pacientes.

>  **Rotina necessária:** backup periódico do banco de dados, permitindo a recuperação das informações em caso de problema.

---

## 6. Relatórios básicos de gestão

A estrutura do banco deve ser planejada para permitir, futuramente, consultas e relatórios de acompanhamento da clínica, como:

- [ ] Quantidade de atendimentos realizados em determinado período
- [ ] Quantidade de agendamentos por funcionário
- [ ] Procedimentos mais realizados
- [ ] Quantidade de agendamentos cancelados
- [ ] Quantidade de pacientes que não compareceram
- [ ] Quantidade de atendimentos concluídos, pendentes ou em andamento
- [ ] Histórico de atendimentos por período
- [ ] Quantidade de atendimentos por tipo de procedimento

>  Esses relatórios auxiliam a gestão na análise de demanda, produtividade, faltas/cancelamentos e tomada de decisão.

---

## 7. Suporte a múltiplas unidades

Como o sistema atenderá uma **rede** de clínicas, o banco de dados deve permitir o cadastro e gerenciamento de várias unidades.

-  Cada agendamento, funcionário e horário disponível deve estar vinculado à sua respectiva unidade.
-  Evita que um paciente visualize ou agende horários de uma unidade diferente da desejada.
-  Facilita a gestão individualizada de funcionários, agendas e atendimentos por unidade.

---

## 8. Justificativa do banco relacional

Recomenda-se, hipoteticamente, o uso de um **banco de dados relacional (SQL)**, pois as informações possuem estrutura definida e relações claras entre entidades.

```
Paciente   1 ──── N   Agendamento
Agendamento 1 ──── 1   Unidade
Agendamento 1 ──── 1   Horário
Funcionário N ──── 1   Unidade
```

> Esses relacionamentos podem ser representados de forma eficiente por tabelas relacionadas com chaves primárias e estrangeiras.

---

## 9. Divisão de responsabilidades

| Frente | Responsabilidade |
|--------|-------------------|
| **Modelagem** | Criar o diagrama de entidade-relacionamento e definir como as entidades se relacionam (ex.: paciente com unidade preferencial, mas podendo agendar em outras unidades) |
| **Estrutura das tabelas** | Definir os campos de cada tabela (nome, contato e unidade do paciente; data, horário, status e motivo de cancelamento do agendamento; estrutura da fila de espera) |
| **Integridade e consistência** | Evitar agendamentos duplicados/conflitantes, prevenir cadastros repetidos e garantir que nenhum registro fique sem vínculo |
| **Multi-unidade** | Garantir que agendamentos, horários e funcionários estejam corretamente associados à sua unidade, evitando mistura de dados entre clínicas |
| **Alinhamento com Segurança da Informação** | Ajudar a identificar dados sensíveis (ex.: resultados de procedimentos) e estruturar o registro de consentimento LGPD |
| **Alinhamento com Back-end** | Definir quais dados cada tela do sistema precisa consultar/alterar (painel do funcionário, área do paciente, fila de espera) e o formato de permissão por tipo de usuário |
| **Suporte a relatórios de gestão** | Organizar os dados para permitir métricas por unidade e motivos de cancelamento |
| **Documentação** | Justificar tecnicamente o tipo de banco escolhido e documentar toda a estrutura de forma clara, sem depender de explicação oral da equipe |

---

## 10. Resultado esperado

Entrega de uma estrutura de dados **coerente, segura, organizada e bem documentada**, capaz de sustentar toda a plataforma da Solutech para a Rede Cuidar+.

-  Armazenamento correto das informações, sem duplicidade e sem dados soltos ou desconectados.
-  Cada funcionário visualiza sua própria agenda, sem sobreposição de horários.
-  Cada paciente acessa corretamente seus agendamentos em andamento, histórico de atendimentos e resultados de procedimentos concluídos.
-  Dados corretamente segmentados por unidade, sem mistura entre clínicas.
-  Fila de espera funcionando como solução real para casos sem horário disponível no momento do agendamento.

---

## 11. Riscos caso a função não fosse considerada

>  Sem uma função dedicada ao Banco de Dados, o projeto correria o risco de **reproduzir dentro do sistema o mesmo problema** que a Rede Cuidar+ já enfrenta hoje.

-  Informações de pacientes, agendamentos e horários poderiam ficar desorganizadas, duplicadas ou sem vínculo entre si, gerando os mesmos (ou novos) conflitos, agora dentro da própria plataforma.
-  O **Back-end** ficaria sem uma base confiável para consultar e gravar informações.
-  A **Segurança da Informação** teria dificuldade em proteger dados sensíveis sem saber exatamente onde e como estão estruturados.
-  Por se tratar de uma rede de clínicas, poderia haver mistura de dados entre unidades diferentes, com pacientes visualizando horários ou históricos que não pertencem à sua clínica.

> No fim, o projeto perderia justamente aquilo que sustenta a confiabilidade da solução, uma base de dados sólida, comprometendo a proposta como um todo, mesmo com front-end, segurança e demais áreas bem desenvolvidas.

---

**Versão:** 1.0
**Última Atualização:** Setembro de 2026
