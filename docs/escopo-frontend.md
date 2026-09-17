Escopo do Front-end
## 1. Objetivo
O Front-end será responsável pela parte visual e interativa da plataforma web, sendo a parte do sistema que os pacientes e a equipe da clínica vão utilizar diretamente, seja para fazer um agendamento, consultar um resultado ou organizar os atendimentos.
A ideia é que o Front-end transforme as funções do sistema em telas simples, organizadas e fáceis de entender, fazendo com que a comunicação com o Back-end aconteça de forma tranquila e sem travamentos.

##  2. O que o Front-end deverá fazer

2.1 Interface e Navegação
Será desenvolvido todo o fluxo de navegação do site, junto com a estrutura das principais telas do sistema.
O sistema terá interfaces diferentes e personalizadas de acordo com o tipo de usuário que fizer o login na plataforma.

2.2 Área do Paciente
Para os pacientes, o Front-end terá uma área mais simples e voltada para facilitar o acesso às informações de saúde. As principais telas serão:
Um dashboard mostrando os próximos agendamentos e o status dos atendimentos;
Uma seção de histórico, onde será possível consultar as consultas que já foram realizadas;
Uma área para acessar os resultados de exames ou consultas.

2.3 Área do Funcionário
Para a equipe da clínica, como a recepção e a gestão, o Front-end terá ferramentas mais voltadas para a organização e administração dos atendimentos. As principais telas serão:
Um dashboard com a agenda da semana, organizada por dia, horário, paciente e status;
Telas para cadastrar e consultar as informações dos pacientes;
Áreas para registrar os atendimentos realizados e lançar os resultados.

2.4 Consumo da API
O Front-end será responsável por fazer a comunicação com a API criada pelo Back-end.
Ele deverá enviar as ações realizadas pelo usuário na interface, utilizando os métodos GET, POST, PUT e DELETE, além de receber as respostas do servidor e atualizar as informações mostradas na tela.

2.5 Protótipos e Planejamento Visual
Antes de começar a codificação final, a parte de Front-end também inclui a criação dos protótipos das principais telas.
Serão criadas as telas de agendamento, histórico do paciente e painel da clínica;
Isso ajudará a validar o fluxo de navegação do site antes de fazer a conexão com o banco de dados.

2.6 Responsividade e Acessibilidade
A interface deverá funcionar bem em diferentes dispositivos, já que os pacientes podem acessar o sistema pelo celular e os funcionários podem utilizar computadores na clínica.
Por isso, as telas precisam se adaptar aos diferentes tamanhos de tela e continuar sendo fáceis de utilizar.
Além disso, serão consideradas boas práticas de acessibilidade, principalmente para que pacientes que tenham menos familiaridade com tecnologia também consigam utilizar o sistema sem muita dificuldade.

2.7 Validação de dados no lado do cliente
Antes de enviar as informações para o Back-end, o Front-end fará algumas validações rápidas nos formulários.
Algumas dessas verificações serão:
Garantir que os campos obrigatórios de cadastro ou agendamento não fiquem vazios;
Verificar se o formato do e-mail ou telefone foi preenchido corretamente;
Mostrar alertas quando alguma informação estiver preenchida de forma incorreta, antes do usuário tentar salvar.

2.8 Feedback visual e Tratamento de erros
O usuário precisa saber o que está acontecendo enquanto utiliza o sistema, por isso, quando uma ação for concluída com sucesso, como um agendamento, o Front-end mostrará uma mensagem informando que deu certo.
Caso aconteça algum problema, como um horário indisponível ou uma falha na conexão com o Back-end, a interface deverá mostrar uma mensagem clara e fácil de entender, informando o que aconteceu e, quando possível, orientando o usuário sobre o que fazer.

## 3. Divisão das responsabilidades
A minha parte no projeto ficará focada principalmente na estruturação da interface, ou seja, no Front-end. Isso inclui o desenvolvimento dos protótipos das principais telas, a criação do fluxo de navegação e a integração visual das áreas do paciente e do funcionário.
A construção da API, a validação das regras de negócio e a infraestrutura ficarão por conta dos responsáveis pelo Back-end. Já a modelagem das informações ficará com a área de Banco de Dados.
Também será importante manter uma comunicação constante com o desenvolvedor Back-end, principalmente para alinhar como os dados, como a lista de consultas e os resultados, serão enviados e recebidos pela interface.
Se o Front-end não fosse considerado no projeto, a clínica continuaria dependendo de planilhas e controles manuais, além de os pacientes não terem uma forma simples de interagir com o sistema. Dessa forma, continuariam existindo problemas como atrasos, desorganização e falhas na comunicação.


## 4. Resultado esperado
Ao final do desenvolvimento, o Front-end entregará as interfaces interativas do sistema.
A plataforma terá um visual limpo, simples e funcional, permitindo que os pacientes consigam acessar seus agendamentos e outras informações com facilidade, enquanto a equipe da clínica poderá organizar e gerenciar os atendimentos de uma forma mais rápida.
Com isso, a ideia é substituir parte dos controles manuais, planilhas e mensagens por um sistema centralizado, facilitando tanto o trabalho da equipe quanto o acesso dos pacientes às informações.
