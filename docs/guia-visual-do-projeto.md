# 01 — O PROJETO

### Solutech

**Criação de uma plataforma de agendamento para a Rede Cuidar+**

### A proposta

* Centralizar agendamentos
* Organizar informações
* Facilitar o atendimento
* Reduzir conflitos de horários
* Apoiar a gestão das unidades

### Usuários

| Paciente             | Equipe da Clínica       |
| -------------------- | ----------------------- |
| Agendar consultas    | Gerenciar agenda        |
| Acompanhar consultas | Gerenciar pacientes     |
| Consultar histórico  | Controlar horários      |
| Consultar resultados | Acompanhar atendimentos |

> Transformar um processo descentralizado em uma plataforma centralizada.

### Divisão de pápeis

**A divisão foi feita considerando principalmente:**

- Interesse pessoal de cada integrante
- Vontade de conhecer uma nova área
- Contribuição para o desenvolvimento profissional

**Objetivo da divisão**

Transformar o projeto em uma experiência prática,permitindo que cada integrante atuasse em uma área de seu interesse e desenvolvesse conhecimentos que pudessem agregar à sua 
formação e ao seu futuro profissional.

---

# 02 — O PROBLEMA

## Como funciona hoje?
**Dados espalhados**
```text
Telefone
   +
Mensagens
   +
Planilhas
   +
Informações separadas
```

### Principais problemas

* Informações descentralizadas
* Conflitos de horários
* Dificuldade de acompanhamento
* Falhas de comunicação
* Retrabalho
* Maior risco de perda de informação

### Problema adicional

**Rede ≠ clínica isolada**

*A Rede Cuidar+ possui **múltiplas unidades**.*

**Portanto:**

Dados de uma unidade precisam permanecer corretamente vinculados àquela unidade.

> O problema principal não é apenas agendar. É **organizar e centralizar as informações da rede**.

---

# 03 — A SOLUÇÃO

## Plataforma web

```text
                    SISTEMA
                       │
          ┌────────────┴────────────┐
          │                         │
       PACIENTE                  CLÍNICA
          │                         │
      Agendamento              Agenda
      Histórico                Pacientes
      Consultas                Profissionais
      Resultados               Horários
                                Unidades
```
> Dois perfis, necessidades diferentes, uma única plataforma.

### Paciente

* Acesso aos próprios dados
* Agendamento
* Acompanhamento
* Histórico
* Resultados

### Clínica

* Gestão da agenda
* Controle de horários
* Cadastro de pacientes
* Profissionais
* Unidades
* Atendimentos

---

# 04 — EVOLUÇÃO DO PROJETO

## Desenvolvimento por fases

*Primeiro resolvemos o problema principal. Depois evoluímos o sistema.*

### FASE 1 — BASE

**Prioridade:** funcionamento essencial

* Cadastro
* Agendamento
* Painel de horários

↓

### FASE 2 — COMUNICAÇÃO

**Prioridade:** relacionamento com o paciente

* Lembretes
* Histórico
* Consentimento

↓

### FASE 3 — REDE COMPLETA

**Prioridade:** expansão para múltiplas unidades

* Múltiplas unidades
* Fila de espera
* Isolamento de dados

↓

### FASE 4 — GESTÃO

**Prioridade:** informações para gestão

* Relatórios
* Métricas
* Dados agregados

### MVP

```text
CADASTRO
    +
AGENDAMENTO
    +
PAINEL DE HORÁRIOS
```

---

# 05 — BANCO DE DADOS

## O banco é a base do sistema

### Principais preocupações

* Integridade dos dados
* Relacionamentos
* Consistência
* Não duplicação
* Controle de horários
* Múltiplas unidades

### Regra importante

> **Um profissional não pode possuir dois agendamentos para o mesmo horário.**

### Multiunidade

```text
UNIDADE A
   ↓
Pacientes / Agenda / Funcionários

UNIDADE B
   ↓
Pacientes / Agenda / Funcionários
```

**Os dados precisam permanecer corretamente associados à sua unidade.**

### Banco + Segurança

A modelagem também influencia:

* Controle de acesso
* Isolamento entre unidades
* Proteção de dados
* LGPD

> O banco não é apenas onde os dados ficam armazenados. Ele sustenta as regras e relacionamentos do sistema.

---

# 06 — BACK-END

## Responsável por processar as regras

```text
FRONT-END
     ↓
   API
     ↓
BACK-END
     ↓
BANCO DE DADOS
```

### Responsabilidades

* Regras de negócio
* Validações
* Processamento
* Comunicação com o banco
* APIs
* Controle das operações
* Integração com Front-end

### Exemplo

**Paciente agenda consulta**

```text
Escolhe horário
      ↓
Sistema recebe solicitação
      ↓
Verifica disponibilidade
      ↓
Valida regras
      ↓
Grava no banco
      ↓
Confirma agendamento
```

### Pergunta-chave

**"O usuário pode simplesmente escolher qualquer horário?"**

**Não.**

O sistema precisa:

* verificar disponibilidade;
* validar regras;
* evitar conflito;
* persistir corretamente.

> O Back-end transforma as ações do usuário em operações válidas dentro do sistema.

---

# 07 — FRONT-END

## Interface entre usuário e sistema

### Paciente

```text
LOGIN
  ↓
HORÁRIOS
  ↓
AGENDAMENTO
  ↓
CONFIRMAÇÃO
  ↓
ACOMPANHAMENTO
```

### Equipe

```text
LOGIN
  ↓
DASHBOARD
  ↓
AGENDA
  ↓
PACIENTES
  ↓
ATENDIMENTOS
```

### Prioridades

* Clareza
* Simplicidade
* Organização
* Feedback ao usuário
* Responsividade
* Facilidade de navegação

### Objetivo

> O usuário não precisa conhecer a complexidade existente no sistema.

Ele precisa conseguir:

**entender → realizar → acompanhar**

---

# 08 — SEGURANÇA DA INFORMAÇÃO

## Segurança desde o início

### Dados sensíveis

O sistema trabalha com:

* Dados pessoais
* Dados de pacientes
* Informações de saúde
* Resultados de procedimentos

### Controle de acesso

```text
USUÁRIO
   ↓
AUTENTICAÇÃO
   ↓
PERFIL
   ↓
PERMISSÕES
   ↓
DADOS AUTORIZADOS
```

### Principais pontos

**Autenticação**

Quem é o usuário?

**Autorização**

O que ele pode acessar?

**Multiunidade**

Qual unidade ele pode acessar?

**Dados sensíveis**

Quais informações precisam de maior proteção?

**LGPD**

Como os dados pessoais são tratados?

### Segurança por fase

| Fase | Prioridade                      |
| ---- | ------------------------------- |
| 1    | Autenticação + acesso           |
| 2    | Dados sensíveis + consentimento |
| 3    | Isolamento entre unidades       |
| 4    | Relatórios sem identificação    |

---

# 09 — QA + ACESSIBILIDADE

## Qualidade também é transversal

### QA

**Validar antes de entregar.**

* Testes funcionais
* Testes exploratórios
* Testes de regressão
* Validação dos fluxos
* Identificação de erros

### Fluxos críticos

```text
CADASTRO
AGENDAMENTO
CANCELAMENTO
HORÁRIO OCUPADO
LOGIN
ACESSO
```

### Acessibilidade

Garantir que o sistema possa ser utilizado por diferentes usuários.

* Textos claros
* Botões identificáveis
* Formulários compreensíveis
* Mensagens de erro
* Navegação consistente
* Informações não dependentes apenas de cores

### Ideia

```text
FUNCIONA?
   ↓
É SEGURO?
   ↓
É USÁVEL?
   ↓
É ACESSÍVEL?
```
---

# 10 — CONCLUSÃO

## O que construímos?

```text
PROBLEMA
   ↓
DESCENTRALIZAÇÃO
   ↓
PLATAFORMA CENTRALIZADA
   ↓
AGENDAMENTO
   ↓
GESTÃO
   ↓
SEGURANÇA
   ↓
QUALIDADE
```

### Resultado esperado

**Para o paciente**

* Mais autonomia
* Agendamento organizado
* Acompanhamento

**Para a clínica**

* Agenda centralizada
* Menos conflitos
* Organização das informações
* Melhor gestão

**Para a rede**

* Estrutura preparada para múltiplas unidades
* Dados organizados
* Segurança
* Evolução por fases

