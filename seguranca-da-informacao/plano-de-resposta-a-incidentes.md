# Plano de resposta a incidentes

O escopo de Segurança da Informação foca principalmente em prevenção. Este documento complementa isso com um ponto que normalmente fica de fora: **o que fazer caso, mesmo com todos os cuidados, algo dê errado**.

## Etapas de resposta a um incidente

Um incidente de segurança (como um acesso indevido a dados de pacientes) segue um fluxo de resposta em etapas, evitando que a reação seja improvisada:

Primeiro vem a **detecção**, quando o problema é identificado, seja por um alerta automático do sistema ou por um relato de usuário. Em seguida, a **contenção**, etapa em que a equipe age rapidamente para isolar o problema, 
como bloquear um acesso suspeito, evitando que o incidente se espalhe. Depois, a **investigação**, buscando entender a origem, o que foi afetado e por quê. A partir do entendimento do incidente, é feita 
a **notificação** às pessoas afetadas e, se necessário, aos órgãos responsáveis, respeitando os prazos exigidos pela LGPD. Na sequência, a **remediação**, corrigindo de fato a causa do problema. 
Por fim, um **retrospecto** (pós-incidente), registrando o que foi aprendido e o que precisa mudar para que não se repita.

**Estrutura de resposta:**
```
Detecção → Contenção → Investigação → Notificação → Remediação → Retrospecto
```

## Funções a serem acionadas

Como o projeto é multidisciplinar, a resposta a um incidente não depende só de quem está em Segurança da Informação.

| Função acionada | Motivo |
|-----------------|--------|
| Back-end | Problema ligado à lógica do sistema |
| Banco de dados | Problema ligado à estrutura ou integridade dos dados |
| Front-end | Problema estiver relacionado à interface, como uma falha que exponha dados na tela ou que permita um ataque através de um formulário mal validado |

>  Ter isso claro evita que, num momento de urgência, a equipe perca tempo decidindo quem deveria estar envolvido.
