Escopo do Back-end

1. Objetivo

O Back-end será responsável pela parte do sistema que fica por trás da aplicação. Ele vai receber as informações enviadas pelo Front-end, verificar os dados, realizar os processos necessários e devolver uma resposta.

Para esse projeto, será utilizado Node.js junto com o Express, que será utilizado para organizar e criar a API do sistema.

O Back-end também ficará responsável pelas regras do sistema e pela comunicação com o banco de dados.

---

2. Tecnologias utilizadas

Para o desenvolvimento do Back-end serão utilizadas:

- Node.js: utilizado para executar o código do Back-end;
- Express: utilizado para criar e organizar a API;
- JSON: utilizado para enviar e receber informações entre o Front-end e a API;
- Banco de dados SQL: utilizado para armazenar as informações do sistema.

A escolha dessas tecnologias permite criar uma API para que o Front-end consiga se comunicar com o Back-end de forma organizada.

---

3. O que o Back-end deverá fazer

3.1 API

O Back-end terá uma API responsável pela comunicação com o Front-end.

A API receberá as solicitações, processará as informações e retornará uma resposta.

Os principais métodos HTTP utilizados serão:

- GET: consultar informações;
- POST: cadastrar informações;
- PUT: atualizar informações;
- DELETE: excluir ou desativar informações quando necessário.

As informações enviadas pela API serão trabalhadas no formato JSON.

---

3.2 Cadastro de pacientes

O Back-end deverá permitir o cadastro e a consulta dos pacientes.

Entre as funções previstas estão:

- cadastrar um paciente;
- consultar pacientes cadastrados;
- consultar um paciente específico;
- atualizar os dados;
- verificar se os campos obrigatórios foram preenchidos;
- evitar cadastros duplicados quando necessário.

As informações deverão ser tratadas com cuidado, principalmente por envolverem dados relacionados aos pacientes.

---

3.3 Agendamento

O Back-end também será responsável pelos agendamentos.

Será necessário permitir:

- criar um agendamento;
- consultar agendamentos;
- alterar um agendamento;
- cancelar um agendamento;
- verificar horários disponíveis;
- evitar que dois agendamentos ocupem o mesmo horário;
- relacionar o agendamento ao paciente, profissional e unidade.

Antes de confirmar um agendamento, o sistema deverá verificar se as informações estão corretas e se o horário está disponível.

---

3.4 Unidades

O sistema poderá trabalhar com mais de uma unidade da clínica.

Por isso, o Back-end deverá levar em consideração a unidade relacionada a cada informação.

Isso é importante para evitar que dados de uma unidade sejam misturados com os dados de outra.

A forma como essas informações serão armazenadas ficará de acordo com a estrutura do banco de dados definida pelo responsável por essa parte.

---

3.5 Usuários e acesso

O Back-end deverá cuidar das operações relacionadas aos usuários do sistema.

Entre elas estão:

- cadastro de usuários, quando necessário;
- login;
- verificação dos dados de acesso;
- controle das permissões;
- identificação do usuário durante as operações.

Cada usuário deverá ter acesso somente às funções permitidas para o seu perfil.

---

3.6 Regras do sistema

O Back-end será responsável por colocar em prática as regras definidas para o funcionamento do sistema.

Alguns exemplos são:

- não permitir agendamento em horário ocupado;
- verificar se o profissional está disponível;
- verificar se o paciente existe antes de realizar um agendamento;
- relacionar o agendamento à unidade correta;
- verificar se os dados enviados são válidos;
- controlar alterações e cancelamentos;
- verificar se o usuário possui permissão para determinada ação.

---

3.7 Validação dos dados

Os dados recebidos pela API deverão ser verificados antes de serem processados.

Algumas verificações serão:

- campos obrigatórios;
- formato dos dados;
- valores permitidos;
- informações duplicadas;
- existência de registros;
- regras relacionadas aos agendamentos.

O objetivo é evitar que informações incorretas sejam inseridas no sistema.

---

3.8 Tratamento de erros

O sistema deverá informar quando alguma operação não puder ser realizada.

Por exemplo:

- paciente não encontrado;
- agendamento não encontrado;
- horário já ocupado;
- dados enviados incorretamente;
- usuário sem permissão;
- usuário não autenticado;
- problema na comunicação com o banco.

Para essas situações serão utilizados os códigos HTTP correspondentes.

Alguns exemplos são:

- 200: operação realizada com sucesso;
- 201: cadastro realizado;
- 400: dados incorretos;
- 401: usuário não autenticado;
- 403: usuário sem permissão;
- 404: informação não encontrada;
- 409: conflito, como um horário já ocupado;
- 500: erro interno.

---

3.9 Comunicação com o banco de dados

A parte de criação e organização do banco de dados ficará com outro integrante do grupo.

O Back-end, porém, precisará se comunicar com o banco para conseguir trabalhar com as informações do sistema.

Essa comunicação será utilizada para operações como:

- cadastrar informações;
- consultar informações;
- atualizar informações;
- excluir ou desativar registros quando necessário;
- consultar informações relacionadas.

A estrutura utilizada pelo Back-end deverá seguir o que for definido pelo responsável pelo banco de dados.

---

3.10 Segurança

O Back-end deverá seguir as medidas de segurança definidas para o projeto.

Entre os principais pontos estão:

- autenticação dos usuários;
- controle de acesso;
- validação das informações recebidas;
- proteção dos endpoints;
- prevenção contra SQL Injection;
- utilização de conexão segura;
- controle de tentativas de acesso;
- registro de operações importantes.

Como o sistema trabalha com informações de pacientes, também deverão ser consideradas as medidas de proteção de dados e as orientações relacionadas à LGPD.

---

3.11 Testes

Serão realizados testes para verificar se o Back-end está funcionando corretamente.

Os testes deverão considerar principalmente:

- funcionamento dos endpoints;
- cadastro de pacientes;
- consultas;
- agendamentos;
- validação dos dados;
- regras do sistema;
- conflitos de horários;
- tratamento de erros;
- login e permissões;
- comunicação com o banco de dados.

---

3.12 Documentação da API

A API também deverá possuir uma documentação para facilitar o entendimento e a integração com o Front-end.

A documentação deverá informar:

- endpoints disponíveis;
- métodos utilizados;
- função de cada endpoint;
- dados que precisam ser enviados;
- respostas esperadas;
- possíveis erros.

---

4. Principais recursos da API

Considerando as funcionalidades previstas para o projeto, os principais recursos do Back-end serão:

Recurso| Operações previstas
Pacientes| Cadastro, consulta e atualização
Agendamentos| Criação, consulta, alteração e cancelamento
Unidades| Consulta e relacionamento com os registros
Profissionais| Consulta e disponibilidade
Usuários| Login e controle de acesso

Os endpoints definitivos poderão ser definidos posteriormente, de acordo com a organização do projeto e do banco de dados.

---

5. Divisão das responsabilidades

A minha parte no projeto ficará focada no Back-end, utilizando Node.js e Express.

As principais responsabilidades serão a criação e documentação da API, implementação das regras do sistema, validação dos dados, tratamento de erros, comunicação com o banco de dados, segurança da API e realização dos testes.

A criação e organização do banco de dados ficará com outro integrante do grupo.

Mesmo com essa divisão, será necessário manter contato entre as duas partes para que o Back-end consiga utilizar corretamente as informações e relacionamentos definidos no banco.

Também será necessário manter a comunicação com o responsável pelo Front-end para que a API forneça as informações necessárias para o funcionamento da interface.

---

6. Resultado esperado

Ao final do projeto, espera-se que a documentação deixe claro como o Back-end deverá funcionar e quais serão suas responsabilidades dentro do sistema.

O Back-end deverá ser responsável por receber as solicitações do Front-end, verificar os dados, aplicar as regras do sistema, realizar a comunicação com o banco de dados e devolver as respostas necessárias.

Como o projeto tem como objetivo a documentação, este documento representa o planejamento de como o Back-end deverá funcionar caso o sistema seja desenvolvido posteriormente.