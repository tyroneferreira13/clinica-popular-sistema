# Priorização de segurança da informação por fases

## 1. Sobre este documento

Este documento conecta a função de **Segurança da Informação** ao fluxo de fases definido em [`docs/funcionalidades.md`](docs/funcionalidades.md).

O objetivo é deixar claro que segurança não deve ser tratada como uma etapa isolada ao final do projeto, mas como uma preocupação **transversal e contínua**, acompanhando a evolução das funcionalidades e dos riscos envolvidos em cada fase.
Cada fase apresenta diferentes necessidades de segurança, que devem ser consideradas desde o planejamento e desenvolvimento das funcionalidades.

---

## 2. Segurança em cada fase

### 2.1 Fase 1 — Base do sistema

Na **Fase 1**, são desenvolvidas as funcionalidades fundamentais do sistema, como:

- Cadastro
- Agendamento
- Painel de horários

Nesse momento, a prioridade de Segurança da Informação é estabelecer os controles básicos de acesso ao sistema.

#### Prioridades de segurança

- Implementar autenticação básica para os dois tipos de usuário
- Definir quais dados cada perfil de usuário pode acessar
- Aplicar as regras de autorização de acordo com a classificação dos dados
- Garantir que usuários não tenham acesso a informações além das necessárias para sua função

A definição dos níveis de acesso deve estar alinhada ao documento de **classificação de dados**, garantindo que a exposição das informações seja compatível com seu nível de sensibilidade.

---

### 2.2 Fase 2 — Comunicação

Na **Fase 2**, o sistema passa a trabalhar com funcionalidades de comunicação, como:

- Lembretes automáticos
- Histórico de interações e informações relacionadas ao atendimento

Com isso, aumenta a quantidade de dados sensíveis que circulam pelo sistema.

#### Prioridades de segurança

- Proteger os dados sensíveis que passam a ser utilizados nas novas funcionalidades
- Garantir o controle de acesso ao histórico dos pacientes
- Proteger informações relacionadas a resultados de procedimentos
- Garantir o registro adequado do consentimento do paciente
- Considerar os requisitos aplicáveis da **LGPD** no tratamento dos dados

O aumento do fluxo de informações exige atenção especial para evitar exposição indevida durante o armazenamento, processamento ou compartilhamento desses dados.

---

### 2.3 Fase 3 — Rede completa

Na **Fase 3**, o sistema passa a suportar múltiplas unidades da rede e funcionalidades adicionais, como:

- Gestão de diferentes unidades
- Fila de espera
- Dados associados a diferentes clínicas

Nesse cenário, o isolamento dos dados entre unidades se torna uma das principais preocupações de segurança.

#### Prioridades de segurança

- Garantir que as permissões de acesso respeitem a unidade à qual o usuário está vinculado
- Isolar os dados entre diferentes unidades
- Impedir que usuários de uma clínica tenham acesso indevido aos dados de outra
- Validar as regras de autorização também no acesso aos dados e não apenas na interface
- Garantir que pacientes, agendamentos, horários e demais informações estejam corretamente associados à unidade correspondente

O principal risco dessa fase é a **exposição cruzada de dados entre unidades**, tornando o controle de acesso e a segregação das informações pontos críticos da implementação.

---

### 2.4 Fase 4 — Gestão

Na **Fase 4**, são desenvolvidas funcionalidades voltadas para análise e acompanhamento do sistema, como:

- Relatórios
- Métricas
- Indicadores de desempenho

Nesse momento, o principal cuidado está relacionado à forma como os dados dos pacientes são apresentados e utilizados para gerar informações gerenciais.

#### Prioridades de segurança

- Evitar a exposição de dados identificáveis dos pacientes
- Utilizar dados agregados para geração de relatórios sempre que possível
- Anonimizar informações quando a identificação do paciente não for necessária
- Restringir o acesso aos relatórios conforme o perfil do usuário
- Garantir que métricas e indicadores não permitam a identificação indireta de pacientes

Os relatórios devem fornecer informações úteis para a gestão sem expor dados pessoais ou sensíveis que não sejam necessários para a finalidade do relatório.

---

## 3. Visão geral das prioridades

| Fase | Contexto | Principal preocupação de segurança |
|------|----------|------------------------------------|
| **Fase 1 — Base do sistema** | Cadastro, agendamento e painel de horários | Autenticação e controle de acesso |
| **Fase 2 — Comunicação** | Lembretes e histórico | Proteção de dados sensíveis e consentimento |
| **Fase 3 — Rede completa** | Múltiplas unidades e fila de espera | Isolamento de dados entre unidades |
| **Fase 4 — Gestão** | Relatórios e métricas | Agregação e anonimização dos dados |

---

## 4. Atuação transversal

Assim como **QA** e **Acessibilidade**, a **Segurança da Informação** atua de forma transversal durante todo o desenvolvimento do projeto.

A diferença é que o tipo de risco e a prioridade de segurança mudam conforme as funcionalidades são introduzidas.

De forma resumida:

1. **Fase 1:** controlar **quem pode acessar** o sistema e quais dados pode visualizar
2. **Fase 2:** proteger **os dados sensíveis que passam a circular** e registrar adequadamente o consentimento
3. **Fase 3:** garantir **isolamento entre as unidades** da rede
4. **Fase 4:** evitar que relatórios e métricas **exponham pacientes identificáveis**

Dessa forma, a segurança acompanha a evolução do produto desde sua base até as funcionalidades de gestão, permitindo que os riscos sejam tratados no momento em que surgem, em vez de serem corrigidos apenas ao final do projeto.
