# Classificação de dados e controle de acesso

O escopo de Segurança da Informação já estabelece a responsabilidade geral de proteger dados sensíveis dos pacientes. 
Este documento aprofunda dois pontos específicos que o escopo não detalha:

- quais dados exigem qual nível de proteção
- quem dentro do sistema pode acessar o quê.

## Classificação de dados por nível de sensibilidade

Nem todo dado do sistema precisa do mesmo nível de proteção. Classificar os dados evita tanto o excesso **(proteger informação pública como se fosse sigilosa, o que trava o sistema à toa)** quanto a 
falta de cuidado **(tratar dado sensível como se fosse qualquer coisa)**.

| Nível	| Exemplos de dados	| Cuidado necessário |
|-------|-------------------|--------------------|
| Crítico	| CPF, dados de login/senha, diagnósticos	| Proteção máxima: criptografia, controle de acesso restrito, registro de quem acessou |
| Sensível	| Histórico médico, telefone, e-mail, data de nascimento	| Criptografia e controle de acesso rigoroso |
| Normal	| Agendamentos futuros, horários de disponibilidade	| Controle de acesso básico, sem necessidade de criptografia especial |
| Público	| Horário de funcionamento, especialidades oferecidas	| Sem restrição, informação já pensada para ser aberta |

## Perfis de acesso (quem vê o quê)

Além de classificar o dado, é preciso definir quem, dentro do sistema, tem permissão de acessá-lo. Isso evita, por exemplo, que um paciente veja dados de outro, ou que a recepção acesse 
informações clínicas diferentes da sua função.

| Perfil	| O que pode acessar |
|---------|--------------------|
| Paciente	| Apenas seus próprios dados: agendamentos, histórico e resultados |
| Recepção	| Agenda da unidade, confirmação de presença e cadastro de pacientes |
| Profissional de saúde	| Dados dos pacientes que atende: histórico e resultados |
| Gestão da unidade	| Dados agregados e relatórios, sem necessidade de ver informações identificadas de cada paciente |

Essa divisão conversa diretamente com o Banco de Dados, já que é a estrutura de tabelas e relacionamentos (paciente, funcionário, unidade) que permite aplicar essas regras de acesso na prática.
