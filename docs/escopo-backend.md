# Escopo do Back-end

## 1. Objetivo

O Back-end vai ser responsável pela parte do sistema que fica por trás da aplicação. Ele vai receber as informações enviadas pelo usuário, verificar os dados, fazer os processos necessários e depois enviar uma resposta para o Front-end.

A ideia é que o Back-end faça essa comunicação de forma organizada, cuidando do processamento das informações e das regras que forem definidas para o sistema.

## 2. O que o Back-end deverá fazer

### 2.1 API

Será desenvolvida uma API para fazer a comunicação entre o Front-end e o Back-end.

A API vai receber as solicitações feitas pelo sistema, processar essas informações e retornar uma resposta.

Os principais métodos HTTP que poderão ser utilizados são:

* GET, para consultar informações;
* POST, para cadastrar informações;
* PUT, para atualizar informações;
* DELETE, para excluir informações.

### 2.2 Usuários

Caso o sistema utilize usuários, o Back-end deverá cuidar das operações relacionadas a eles, como:

* Fazer o cadastro;
* Consultar os usuários;
* Alterar informações;
* Excluir usuários;
* Verificar se os dados informados estão corretos.

### 2.3 Login e acesso

Se o projeto precisar de login, o Back-end também será responsavel por verificar os dados de acesso dos usuários.

Também deverá controlar o acesso às partes do sistema que precisam de autenticação.

### 2.4 Regras do sistema

O Back-end será responsável por colocar em prática as regras definidas para o funcionamento do sistema.

Antes de realizar alguma operação, os dados recebidos deverão ser analisados para verificar se estão de acordo com o que foi definido no projeto.

### 2.5 Validação dos dados

Os dados recebidos pela API deverão ser validados antes de serem processados.

Algumas das verificações serão:

* Conferir os campos obrigatórios;
* Verificar o formato dos dados;
* Impedir valores que não sejam permitidos;
* Verificar informações duplicadas quando for necessario;
* Conferir se os dados seguem as regras do sistema.

### 2.6 Tratamento de erros

O sistema também precisa estar preparado para quando alguma coisa não funcionar como esperado.

Por exemplo, se for feita uma consulta de um registro que não existe ou for enviado algum dado incorreto, o Back-end deverá informar o problema através de uma resposta adequada.

Também serão utilizados os códigos HTTP correspondentes para cada situação.

### 2.7 Integração com o banco de dados

A criação e a organização do banco de dados ficará com outro integrante do grupo.

Mesmo assim, o Back-end precisará fazer a comunicação com o banco para conseguir cadastrar, consultar, alterar e excluir as informações utilizadas pelo sistema.

Essa parte será feita de acordo com a estrutura do banco que for definida pelo responsável por essa etapa.

### 2.8 Testes

Durante o desenvolvimento serão realizados testes para verificar se o Back-end está funcionando corretamente.

Serão testados principalmente:

* Os endpoints da API;
* A validação dos dados;
* O processamento das informações;
* O tratamento de erros;
* A comunicação com o banco de dados.

### 2.9 Documentação

Também será feita uma documentação da API para facilitar o entendimento do projeto.

Nessa documentação serão colocadas informações sobre:

* Endpoints disponíveis;
* Métodos utilizados;
* Dados que precisam ser enviados;
* Respostas esperadas;
* Possíveis erros.

## 3. Divisão das responsabilidades

A minha parte no projeto ficará focada no desenvolvimento do Back-end, incluindo a criação da API, implementação das regras do sistema, validação dos dados, tratamento de erros, integração com o banco e realização dos testes.

A parte de modelagem e organização do banco de dados ficará com outro integrante do grupo.

Mesmo com essa divisão, será necessario manter uma comunicação entre as duas partes para que o Back-end consiga trabalhar corretamente com o banco.

## 4. Resultado esperado

Ao final do desenvolvimento, o Back-end deverá estar funcionando como a parte responsável pelo processamento das informações do sistema.

Ele deverá receber as solicitações do Front-end, verificar os dados, realizar os processos necessários, acessar o banco de dados quando for preciso e devolver uma resposta adequada para o sistema.
