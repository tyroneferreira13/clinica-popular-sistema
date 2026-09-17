# Solutech — Plataforma para Rede Cuidar+

Repositório da atividade acadêmica "Construindo uma solução para uma rede de clínicas populares". Aqui está documentada a proposta da Solutech, uma empresa fictícia de tecnologia, para resolver os problemas de agendamento e comunicação de uma rede de clínicas populares fictícia.

## Sobre a empresa

- **Nome:** Solutech
- **Área de atuação:** Desenvolvimento de soluções tecnológicas sob medida
- **Descrição:** Empresa de tecnologia que desenvolve sistemas e plataformas digitais para clientes de diferentes setores. Neste projeto, atua como fornecedora de solução para a Rede Cuidar+.

## O problema

A **Rede Cuidar+**, cliente fictício deste projeto, enfrenta dificuldades para organizar agendamentos, evitar conflitos de horários, enviar lembretes aos pacientes e acompanhar atendimentos. As informações hoje são registradas por telefone, mensagens e planilhas não integradas, o que causa perda de dados, atrasos e falhas de comunicação, agravado pelo fato de ser uma rede com várias unidades, e não uma clínica isolada.

Descrição completa em [`docs/problema-rede-cuidar.md`](docs/problema-rede-cuidar.md).

## A solução

Uma **plataforma web** com dois tipos de login (paciente e equipe da clínica), cada um direcionado a uma área própria do sistema:

- **Equipe:** gerencia sua agenda, evita conflitos de horário, cadastra pacientes
- **Paciente:** agenda consultas, acompanha atendimentos em andamento e consulta o histórico com resultados

Visão geral completa em [`docs/visao-geral-do-projeto.md`](docs/visao-geral-do-projeto.md).

## Estrutura do repositório

```
solutech-rede-cuidar/
│
├── README.md
│
├── docs/ → documentação geral do projeto
│ ├── apresentacao-solutech.md
│ ├── problema-rede-cuidar.md
│ ├── funcionalidades.md
│ ├── mvp.md
| ├── divisao-dos-papeis.md
│ ├── beneficios-e-riscos.md
│ ├── escopo-banco-de-dados.md
│ ├── escopo-back-end.md
│ ├── escopo-front-end.md
│ ├── escopo-seguranca-da-informacao.md
│ └── escopo-qa-suporte.md
│
├── banco-de-dados/ → material técnico de apoio
│ ├── diagrama-entidade-relacionamento.md
│ ├── dicionario-de-dados.md
│ └── justificativa-tecnica.md
│
├── seguranca-da-informacao/
│├── checklist-de-deploy-seguro.md
│├── classificacao-de-dados-e-controle-de-acesso.md
│├── plano-de-resposta-a-incidentes.md
│└── priorizacao-por-fases.md
│
└── linkedin/ → postagens individuais
├── post-cristian.md
├── post-tayrone.md
├── post-vinicius.md
├── post-calebe.md
└── post-carlos.md

```


## Equipe

| Integrante | Papel |
|---|---|
| Cristian | Banco de Dados|
| Tayrone | Back-end |
| Vinicius | Front-end|
| Calebe | Segurança da Informação |
| Carlos | QA e Acessibilidade  |

## Como navegar neste repositório

- Quer entender o projeto como um todo? Comece por `docs/apresentacao-solutech.md`, `docs/problema-rede-cuidar.md`.
- Quer entender uma função específica? Veja o escopo correspondente em `docs/`.
- Quer ver as postagens de LinkedIn de cada integrante? Estão todas na pasta `linkedin/`.

---

Projeto desenvolvido para fins acadêmicos, sem intenção comercial real.
