# Justificativa técnica 

Toda decisão técnica importante do projeto merece ser registrada, não só implementada. Este documento existe para explicar e justificar por que foi escolhi um banco de dados relacional (SQL) para a 
plataforma da Solutech, mostrando que essa escolha não foi aleatória, mas baseada nas características reais do problema que a Rede Cuidar+ precisa resolver.

# 1. Natureza dos dados do projeto

Os dados da plataforma da Solutech são, por natureza, estruturados e fortemente relacionados entre si. Um paciente está sempre vinculado a agendamentos específicos, cada agendamento pertence a um 
horário, um funcionário responsável e uma unidade da rede, e o histórico de atendimentos depende diretamente dessas relações para fazer sentido. Esse tipo de informação, previsível em formato e com 
conexões claras entre as entidades, é exatamente o cenário em que um banco de dados relacional se destaca.

# 2. Por que um banco relacional (SQL)

Um banco relacional organiza os dados em tabelas com relações bem definidas entre si, o que se encaixa diretamente na forma como o sistema precisa funcionar. 
A relação entre paciente, agendamento, horário e unidade pode ser representada de forma clara por meio de chaves primárias e chaves estrangeiras, garantindo que cada registro esteja sempre corretamente 
vinculado aos demais.

Além disso, bancos relacionais seguem o modelo ACID (atomicidade, consistência, isolamento e durabilidade), o que é especialmente importante para o problema que a Rede Cuidar+ enfrenta hoje. 
Evitar que dois agendamentos ocupem o mesmo horário do mesmo profissional, por exemplo, depende de operações consistentes e confiáveis no banco de dados, algo que o modelo relacional garante de forma 
nativa.

# 3. Por que não optar por um banco não relacional (NoSQL)

Bancos não relacionais (NoSQL) costumam se destacar em cenários com grande volume de dados não estruturados, sem relações fixas entre si, ou que exigem escalabilidade horizontal massiva, como redes sociais ou sistemas de big data. 
Não é o caso deste projeto, onde os dados possuem uma estrutura previsível e as relações entre pacientes, agendamentos e horários são o próprio núcleo do problema a ser resolvido. 
Usar um banco não relacional aqui exigiria recriar, na aplicação, mecanismos que o modelo relacional já garante nativamente, aumentando a complexidade sem necessidade real.

# 4. Comparação resumida

| Critério | Banco relacional (SQL) | Banco não relacional (NoSQL) |
|----------|------------------------|------------------------------|
| Relações entre dados | Nativas e bem definidas (chaves estrangeiras) | Precisam ser tratadas manualmente pela aplicação |
| Consistência dos dados | Alta, garantida pelo modelo ACID | Pode priorizar disponibilidade em vez de consistência |
| Estrutura dos dados | Ideal para dados previsíveis e estruturados | Ideal para dados variáveis ou não estruturados |
| Adequação ao projeto | Alta, dado o volume de relações entre entidades | Baixa, geraria complexidade desnecessária |

# 5. Conclusão

Diante do volume de relações entre pacientes, agendamentos, horários, funcionários e unidades, além da necessidade de garantir consistência para evitar conflitos de horário, o modelo relacional (SQL) 
se mostra a escolha mais adequada para sustentar a plataforma da Solutech, oferecendo uma base sólida e confiável para o restante do sistema ser construído em cima.
