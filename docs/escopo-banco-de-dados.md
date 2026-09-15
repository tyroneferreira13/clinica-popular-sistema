# Escopo Banco de dados

## 1. Objetivo

Estruturar e manter a base de dados da plataforma da Solutech, garantindo que todas as informações da Rede Cuidar+, pacientes, funcionários, agendamentos, horários e histórico de atendimentos, fiquem armazenadas
de forma organizada, íntegra e acessível para as demais áreas do sistema (front end e back end). O objetivo direto é eliminar o problema relatado pela rede de clínicas: dados espalhados de forma desorganizada.

## 2. O que o Banco de Dados deverá fazer

### 2.1 Armazenamento de dados dos funcionários e pacientes

* Nome, cargo/função na clínica (ex: recepção, profissional de saúde), e permissões de acesso ao sistema.
* Vincular cada funcionário aos agendamentos pelos quais é responsável, permitindo montar a agenda individual de cada um.
* Nome, contato (telefone/e-mail), data de nascimento, e demais dados de cadastro necessários para identificação.
* Vincular cada paciente ao seu próprio histórico de agendamentos e resultados, de forma que essas informações nunca se misturem com as de outro paciente.

### 2.2 Gerenciar agendamentos

É necessário registrar a data, o horário, o paciente, o funcionário responsável e o tipo de procedimento de cada agendamento. Também é preciso manter um status atualizado para cada agendamento, 
como: confirmado, pendente, em andamento, concluído ou cancelado. Esse status será utilizado para determinar quais informações e agendamentos serão exibidos na tela do paciente e na tela do funcionário.
Além disso, o sistema deve garantir que dois agendamentos não possam ocupar o mesmo horário para o mesmo profissional, estabelecendo uma regra de integridade que impeça conflitos de horários, conforme o problema identificado originalmente.

### 2.3 Controlar a disponibilidade de horários

Para garantir o funcionamento correto dos agendamentos também é preciso controlar os horários das seguintes formas:

* Manter uma tabela de horários disponíveis por funcionário/profissional, para que o sistema saiba quando é possível marcar uma nova consulta.
* Atualizar automaticamente a disponibilidade sempre que um agendamento for criado, remarcado ou cancelado.

### 2.4 Guardar histórico e resultados de procedimentos

O sistema deve manter o histórico dos procedimentos realizados por cada paciente, permitindo consultar posteriormente os atendimentos que já foram concluídos.

Após a conclusão do procedimento, o paciente poderá visualizar o resultado e as observações disponibilizadas para ele em sua área do sistema, 
enquanto o funcionário poderá registrar ou consultar essas informações de acordo com suas permissões de acesso.

Para cada procedimento realizado, devem ser armazenadas informações como:

* Paciente ao qual o procedimento está vinculado
* Data e horário da realização
* Funcionário responsável pelo atendimento
* Tipo de procedimento realizado
* Status do procedimento, indicando se foi concluído
* Resultado, observação ou informações relevantes registradas pelo funcionário

Os resultados e observações devem permanecer vinculados ao respectivo atendimento, evitando que informações de diferentes procedimentos sejam misturadas.

### 2.5 Separar as informações de acordo com o tipo de login

O sistema deve possuir controle de acesso baseado no tipo de usuário, garantindo que cada pessoa visualize somente as informações necessárias para sua função.

A área do paciente deve permitir o acesso somente às suas próprias informações, como:

* Seus dados cadastrais
* Seus agendamentos
* Status dos procedimentos
* Histórico de atendimentos
* Resultados e observações que estejam disponíveis para visualização

Já a área do funcionário deve permitir o acesso aos agendamentos e informações necessárias para a realização dos atendimentos sob sua responsabilidade. 
Dependendo do cargo ou nível de permissão, o funcionário poderá consultar apenas seus próprios atendimentos ou os agendamentos de toda a clínica.

Dessa forma, o sistema evita que um paciente tenha acesso aos dados de outro paciente ou que um funcionário visualize informações que não fazem parte de suas responsabilidades.

### 2.6 Garantir integridade e consistência dos dados

O sistema deve possuir regras que garantam que os dados armazenados sejam corretos, consistentes e não sejam duplicados ou registrados de forma incorreta.

Entre as principais regras, estão:

* Evitar a duplicidade de cadastros de pacientes, utilizando informações que permitam identificar um paciente já existente
* Garantir que cada agendamento esteja obrigatoriamente vinculado a um paciente, funcionário responsável, data, horário e tipo de procedimento
* Impedir que sejam criados agendamentos sem os dados obrigatórios
* Garantir que dois agendamentos não ocupem o mesmo horário para o mesmo profissional
* Manter relacionamentos claros entre as informações do sistema.

A estrutura dos dados deve seguir uma relação lógica, por exemplo:

Paciente → Agendamento → Data/Horário → Funcionário → Procedimento → Resultado

Essa organização evita a existência de informações "soltas" ou sem vínculo com um paciente ou atendimento específico e facilita a consulta, atualização e manutenção dos dados.

### 2.7 Prever backup e histórico de alterações

O sistema deve possuir mecanismos básicos para proteger os dados contra perda, exclusão acidental ou falhas no sistema, especialmente por se tratar de informações relacionadas a atendimentos e histórico de pacientes.
Por isso deve ser definida uma rotina de backup periódico do banco de dados, permitindo a recuperação das informações caso ocorra algum problema.

### 2.8 Apoiar relatórios básicos de gestão

A estrutura do banco de dados deve ser planejada de forma que as informações armazenadas possam ser utilizadas futuramente para consultas e relatórios de acompanhamento da clínica.

Os dados dos agendamentos, procedimentos e atendimentos devem permitir a geração de relatórios básicos, como:

* Quantidade de atendimentos realizados em determinado período
* Quantidade de agendamentos por funcionário
* Procedimentos mais realizados
* Quantidade de agendamentos cancelados
* Quantidade de pacientes que não compareceram
* Quantidade de atendimentos concluídos, pendentes ou em andamento
* Histórico de atendimentos por período
* Quantidade de atendimentos por tipo de procedimento

Esses relatórios poderão auxiliar a gestão da clínica na análise da demanda, acompanhamento da produtividade, identificação de faltas e cancelamentos e tomada de decisões administrativas.

### 2.9 Suportar múltiplas unidades da rede

Como o sistema será utilizado por uma rede de clínicas, o banco de dados deve permitir o cadastro e o gerenciamento de várias unidades. Cada agendamento, funcionário e horário disponível deverá estar 
vinculado à respectiva unidade.

Essa estrutura evita que um paciente visualize ou agende horários pertencentes a uma unidade diferente daquela em que deseja ser atendido. 
Também facilita a gestão individualizada de funcionários, agendas e atendimentos por unidade.

### 2.10 Gerenciar fila de espera

O banco de dados deverá possuir uma estrutura para registrar pacientes que não encontraram horários disponíveis e desejam entrar em uma fila de espera.

A fila deverá armazenar informações como:

* paciente
* unidade
* especialidade
* profissional desejado
* preferência de data/horário
* status da solicitação

Quando surgir uma vaga compatível, o sistema poderá utilizar essas informações para realizar a notificação do paciente.

### 2.11 Registrar dados de consentimento (LGPD)

Além dos mecanismos de segurança e proteção dos dados, o banco deverá armazenar o registro de consentimento do paciente para utilização e tratamento de seus dados.

Podem ser registrados, por exemplo, a data e hora do consentimento, a versão dos termos ou política de privacidade aceita e o status do consentimento. 
Dessa forma, o sistema mantém evidências que auxiliam na demonstração de conformidade com a LGPD.

### 2.12 Justificar a escolha do banco de dados relacional

Para o projeto, recomenda-se a utilização hipotética de um banco de dados relacional (SQL), pois as informações possuem estrutura definida e relações claras entre as entidades.

Por exemplo, um paciente pode possuir vários agendamentos, um agendamento pertence a uma unidade e a um horário, e funcionários podem estar vinculados a determinadas unidades. 
Esse tipo de relacionamento pode ser representado de forma eficiente por tabelas relacionadas e chaves primárias e estrangeiras.

## 3. Divisão das responsabilidades

A responsabilidade central dessa função de Banco de Dados é modelar toda a estrutura de dados da plataforma, criando o diagrama de entidade-relacionamento, além de definir como essas entidades se relacionam entre si. 
Por exemplo, um paciente pode ter uma unidade preferencial, mas também pode agendar em outras unidades da rede, e cada agendamento está sempre vinculado a um horário, um funcionário responsável e uma unidade específica.

A partir dessa modelagem, cabe também definir a estrutura das tabelas propriamente ditas, especificando os campos necessários 
em cada uma, como nome, contato e unidade vinculada no caso do paciente, ou data, horário, status e motivo de cancelamento no caso do agendamento, incluindo a estrutura da fila de espera, 
que conecta paciente, unidade e horário desejado.

Outra responsabilidade importante é garantir a integridade e a consistência dos dados, evitando agendamentos duplicados ou conflitantes no mesmo horário de um 
mesmo profissional, prevenindo cadastros repetidos de pacientes e funcionários, e assegurando que nenhum registro fique solto sem seus devidos vínculos. 
Como a proposta envolve uma rede de clínicas e não uma unidade isolada, também é responsabilidade dessa função garantir que agendamentos, horários e funcionários estejam corretamente associados à sua 
respectiva unidade, evitando que informações de clínicas diferentes se misturem e acabem causando uma desorganização geral dos dados e dos atendimentos.

O Banco de Dados também precisa atuar em conjunto com a Segurança da Informação, ajudando a identificar quais dados são sensíveis e exigem proteção redobrada, 
como os resultados de procedimentos, e estruturando o registro de consentimento do paciente em relação à LGPD. Da mesma forma, é necessário alinhamento constante com o Back-end, 
definindo quais dados cada tela do sistema precisa consultar ou alterar, seja no painel do funcionário, na área do paciente ou na fila de espera, além do formato de 
permissão de acesso conforme o tipo de usuário.

Por fim, essa função é responsável por dar suporte a futuros relatórios de gestão, organizando os dados de forma que seja possível, 
por exemplo, medir atendimentos por unidade ou motivos de cancelamento. Também é preciso justificar tecnicamente a escolha do tipo de banco de dados utilizado no projeto, e documentar toda essa estrutura
de forma clara, de modo que qualquer pessoa consiga compreender a lógica do banco sem depender de explicação oral da equipe.

## 4. Resultado esperado

O resultado esperado dessa função é a entrega de uma estrutura de dados coerente, segura, organizada e bem documentada, capaz de sustentar toda a plataforma da Solutech para a Rede Cuidar+. Isso significa que o sistema deve ser capaz de armazenar corretamente as 
informações, sem duplicidade e sem dados soltos ou desconectados entre si.

Espera-se também que essa estrutura elimine, na prática, o problema relatado pelo cliente, permitindo que cada funcionário visualize sua própria agenda sem sobreposição de horários, e que cada 
paciente acesse corretamente seus agendamentos em andamento, seu histórico de atendimentos e os resultados de procedimentos já concluídos.

Como a proposta envolve uma rede de clínicas, também é esperado que os dados estejam corretamente segmentados por unidade, garantindo que informações de uma clínica 
não se misturem com as de outra, e que a fila de espera funcione como uma solução real para os casos em que não há horário disponível no momento do agendamento.

## 5. O que poderia acontecer com o projeto caso o Banco de Dados não fosse considerada

Sem uma função dedicada ao Banco de Dados, o projeto correria o risco de reproduzir exatamente o problema que a Rede Cuidar+ já enfrenta hoje, apenas transportado para dentro do sistema. Sem uma estrutura de dados bem definida, as 
informações de pacientes, agendamentos e horários poderiam ficar desorganizadas, duplicadas ou sem vínculo entre si, o que voltaria a gerar os mesmos e até novos conflitos, só que agora dentro de uma plataforma que deveria justamente resolver isso.

Se de fato fosse desconsiderada essa função iria comprometer o trabalho de outras áreas do projeto. O Back-end ficaria sem uma base confiável para consultar e gravar informações. 
A Segurança da Informação teria dificuldade em proteger dados sensíveis de pacientes sem saber exatamente onde e como eles estão estruturados.

Além disso, como a proposta envolve uma rede de clínicas e não uma unidade isolada, a falta dessa função poderia levar à mistura de dados entre unidades diferentes, com pacientes visualizando horários ou históricos que não pertencem à sua clínica. No fim, o projeto perderia justamente aquilo que sustenta toda a confiabilidade da solução, uma base de dados sólida, e isso comprometeria a proposta como um todo, mesmo que front-end, segurança e demais áreas estivessem bem desenvolvidas.

