Esse dicionário descreve detalhadamente os elementos do banco de dados como:

- Tabelas
- Campos
- Tipos de dados
- Chaves
- Restrições
- Regras de preenchimento

Ele serve como referência para a equipe, garantindo padronização e facilitando a compreensão, implementação e manutenção do banco de dados ao longo do projeto.

### Unidade:
| Campo	| Tipo	| Obrigatório	| Descrição |
|-------|-------|-------------|-----------|
| id	| int (PK)	| Sim	| Identificador único da unidade |
| nome	| string	| Sim	| Nome da clínica dentro da rede |
| endereco	| string	| Sim	| Endereço físico da unidade |
| telefone	| string	| Não	| Telefone de contato da unidade |

### Paciente:
| Campo	| Tipo	| Obrigatório	| Descrição |
|-------|-------|-------------|-----------|
| id	| int (PK)	| Sim	| Identificador único do paciente |
| nome	| string	| Sim	| Nome completo do paciente |
| contato	| string	| Sim	| Telefone ou e-mail para lembretes e notificações |
| data_nascimento	| date	| Sim	| Data de nascimento do paciente |
| consentimento_lgpd	| boolean	| Sim	| Indica se o paciente aceitou os termos de tratamento de dados |
| unidade_id	| int (FK)	| Sim	| Unidade preferencial do paciente |

### Funcionário:
| Campo	| Tipo	| Obrigatório	| Descrição |
|-------|-------|-------------|-----------|
| id	| int (PK)	| Sim	| Identificador único do funcionário |
| nome	| string	| Sim	| Nome completo do funcionário |
| cargo	| string	| Sim	| Função exercida (ex: recepção, profissional de saúde) |
| unidade_id	| int (FK)	| Sim |	Unidade à qual o funcionário está vinculado |

### Horário:
| Campo	| Tipo | Obrigatório	| Descrição |
|-------|------|--------------|-----------|
| id	| int (PK)	| Sim	| Identificador único do horário |
| data	| date	| Sim	| Data do horário disponível |
| hora_inicio	| time	| Sim	| Horário de início do atendimento | 
| hora_fim	| time	| Sim	| Horário de término do atendimento | 
| disponivel	| boolean	| Sim	| Indica se o horário ainda está livre para agendamento |
| funcionario_id	| int (FK)	| Sim	| Funcionário responsável pelo horário |
| unidade_id	| int (FK) |	Sim	| Unidade à qual o horário pertence |

### Agendamento:
| Campo	| Tipo	| Obrigatório	| Descrição |
|-------|-------|-------------|-----------|
| id	| int (PK)	| Sim	| Identificador único do agendamento |
| status	| string	| Sim	| Confirmado, pendente, em andamento, concluído ou cancelado |
| motivo_cancelamento	| string	| Não	| Preenchido apenas se o agendamento for cancelado ou remarcado |
| resultado	| string	| Não	| Observações ou resultado do atendimento, visível ao paciente |
| data_criacao	| datetime	| Sim	| Data e hora em que o agendamento foi criado |
| paciente_id	| int (FK)	| Sim	| Paciente vinculado ao agendamento |
| funcionario_id	| int (FK)	| Sim	| Funcionário responsável pelo atendimento |
| horario_id	| int (FK)	| Sim	| Horário ocupado por esse agendamento |
| unidade_id	| int (FK)	| Sim	| Unidade onde o atendimento ocorre |

### Fila de Espera:
| Campo	| Tipo	| Obrigatório	| Descrição |
|-------|-------|-------------|-----------|
| id	| int (PK)	| Sim	| Identificador único do registro na fila |
| horario_desejado	| date	| Sim	| Data desejada pelo paciente caso surja uma vaga |
| data_entrada	| datetime |	Sim	| Momento em que o paciente entrou na fila de espera |
| paciente_id	 | int (FK) |	Sim	| Paciente que está aguardando vaga |
| unidade_id	| int (FK) |	Sim	| Unidade em que o paciente deseja ser atendido |
