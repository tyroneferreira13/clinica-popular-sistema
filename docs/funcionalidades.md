# 1. Funcionalidades

## 1.1 Equipe da clínica

- Visualização da própria agenda, com horários ocupados e disponíveis
- Gestão da disponibilidade de horários
- Cadastro de novos pacientes
- Atualização do status do atendimento (confirmado → em andamento → concluído)
- Visualização da fila de espera para encaixes em caso de cancelamento

## 1.2 Pacientes

- Agendamento online de consultas
- Visualização dos agendamentos em andamento (incluindo exames/procedimentos pendentes)
- Acesso ao histórico de atendimentos, com data, profissional e resultados
- Entrada na fila de espera quando não há horário disponível

## 1.3 Administrativas da rede

- Segmentação dos dados por unidade da rede
- Cada clínica gerencia apenas suas próprias informações
- Base para uma futura visão consolidada da rede como um todo

## 1.4 Comunicação e notificação

- Lembretes automáticos antes da consulta
- Notificação ao paciente em caso de remarcação ou mudança de status do agendamento

# 2. Ordem de implementação

O desenvolvimento das funcionalidades segue uma lógica de camadas, começando pelo que sustenta a operação básica do sistema e avançando gradualmente para recursos que atendem o funcionamento completo 
da rede. A primeira etapa concentra-se em fazer o sistema existir de fato: 

- cadastro de pacientes
- agendamento
- painel simples de horários

A partir dessa base, o foco se desloca para a comunicação com o paciente, incluindo lembretes automáticos e o histórico de atendimentos, o que já exige atenção redobrada da Segurança da Informação, já que
passam a existir mais dados sensíveis circulando pelo sistema. Só depois disso o sistema passa a se comportar como uma rede de fato, com suporte a múltiplas unidades e fila de espera, etapa que 
volta a depender fortemente do Banco de Dados, agora em conjunto com quem estiver em função Full Stack para integrar essas regras às telas existentes. Por fim, a camada de gestão, com relatórios e métricas,
é a menos urgente, já que depende de todas as camadas anteriores estarem funcionando para gerar dados confiáveis de análise.

## 2.1 Tabela de implementação

| Fase | O que entra | Áreas envolvidas |
|---|---|---|
| 1. Base do sistema | Cadastro, agendamento e painel de horários | Banco de Dados, Back-end e Front-end |
| 2. Comunicação | Lembretes automáticos e histórico de atendimentos | Back-end e Segurança da Informação |
| 3. Rede completa | Fila de espera e suporte a múltiplas unidades | Banco de Dados, Back-end e Front-end |
| 4. Gestão | Relatórios e métricas da rede | Back-end, Front-end e Banco de Dados |

> QA e Acessibilidade atuam de forma transversal, validando cada fase antes de seguir para a próxima, em vez de entrarem apenas ao final do projeto.
> Isso garante que cada funcionalidade seja testada e corrigida, se for necessário.
