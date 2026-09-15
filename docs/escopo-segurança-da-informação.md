**Projeto:** Plataforma de Gerenciamento de Clínicas  
**Cliente:** Rede Cuidar+  
**Responsável:** Calebe (Segurança da Informação)  
**Data:** Setembro de 2026

---

## 📑 Índice

1. [Autenticação e Controle de Acesso](#1-autenticação-e-controle-de-acesso)
2. [Proteção de Dados](#2-proteção-de-dados)
3. [Proteção do Banco de Dados](#3-proteção-do-banco-de-dados)
4. [Proteção da API](#4-proteção-da-api)
5. [Conformidade LGPD](#5-conformidade-lgpd)
6. [Monitoramento e Logging](#6-monitoramento-e-logging)
7. [Segurança da Infraestrutura](#7-segurança-da-infraestrutura)
8. [Segurança no Front-End](#8-segurança-no-front-end)
9. [Testes de Segurança](#9-testes-de-segurança)
10. [Plano de Resposta a Incidentes](#10-plano-de-resposta-a-incidentes)
11. [Priorização MVP](#-priorização-rápida-mvp)

---

## 1. Autenticação e Controle de Acesso

### 1.1 Autenticação Multi-Fator (MFA)

| Aspecto | Detalhes |
|---------|----------|
| **Para Funcionários** | 2FA obrigatório (SMS, email ou app authenticator) |
| **Para Pacientes** | Opcional no início, obrigatório em breve |
| **Implementação** | JWT com refresh tokens + TOTP (Time-based One-Time Password) |
| **Validade do Token** | Refresh token: 7 dias; Access token: 1 hora |

**Fluxo Recomendado:**
```
1. Usuário insere email e senha
2. Sistema valida credenciais
3. Gera código 2FA e envia (SMS/email/app)
4. Usuário insere código
5. Sistema emite JWT
```

### 1.2 Gestão de Senhas

- ✅ Exigir senhas fortes:
  - Mínimo **12 caracteres**
  - Pelo menos 1 maiúscula, 1 minúscula
  - Pelo menos 1 número e 1 caractere especial
  - Não pode ser igual às últimas 5 senhas

- ✅ **Hashing de Segurança:**
  - Use **bcrypt** ou **Argon2** (NUNCA MD5 ou SHA-1)
  - Salt rounds: 12 (bcrypt) ou padrão Argon2

- ✅ **Rate Limiting de Login:**
  - Máximo **5 tentativas** em **5 minutos**
  - Bloquear IP temporariamente após limite
  - Implementar CAPTCHA na 3ª falha

- ✅ **Recuperação Segura de Senha:**
  - Enviar link com token temporário (válido por **30 minutos**)
  - Token deve ser único e armazenado com hash
  - Invalidar token após primeira utilização

### 1.3 Controle de Acesso Baseado em Função (RBAC)

| Perfil | Acesso | Funcionalidades |
|--------|--------|-----------------|
| **Paciente** | Seus dados apenas | Agendar, visualizar histórico, resultados, reeditar perfil |
| **Recepção** | Todos agendamentos | Gerenciar agenda, confirmar pacientes, check-in |
| **Profissional** | Pacientes atendidos | Prontuário, resultados, prescrições |
| **Gerente** | Dados agregados | Relatórios, análises (sem identificação) |
| **Admin** | Controle total | Usuários, sistema, backups, logs |

**Exemplo de Permissões:**
```javascript
// Paciente: Ler próprios dados
GET /api/v1/pacientes/me

// Profissional: Ler prontuário de pacientes atendidos
GET /api/v1/pacientes/{id}/prontuario

// Gerente: Relatórios (dados anônimos)
GET /api/v1/relatorios/agendamentos?anonimizado=true

// Admin: Gerenciar usuários
POST /api/v1/admin/usuarios
DELETE /api/v1/admin/usuarios/{id}
```

---

## 2. Proteção de Dados

### 2.1 Criptografia em Repouso

**Campos que DEVEM ser criptografados:**

| Campo | Nível | Algoritmo |
|-------|-------|-----------|
| CPF | CRÍTICO | AES-256 |
| RG | CRÍTICO | AES-256 |
| Data de Nascimento | SENSÍVEL | AES-256 |
| Telefone | SENSÍVEL | AES-256 |
| Email | SENSÍVEL | AES-256 |
| Endereço Completo | SENSÍVEL | AES-256 |
| Histórico Médico | SENSÍVEL | AES-256 |
| Diagnósticos | CRÍTICO | AES-256 |

**Implementação:**
- Use **AWS KMS**, **Azure Key Vault** ou **HashiCorp Vault** para gerenciar chaves
- Chaves NUNCA devem estar no código ou variáveis de ambiente diretas
- Rotacionar chaves a cada **90 dias**

### 2.2 Criptografia em Trânsito

```
✅ SSL/TLS 1.3 obrigatório em TODA comunicação
✅ HSTS (HTTP Strict-Transport-Security) - forçar HTTPS
✅ Certificado válido de CA confiável (Let's Encrypt ou comercial)
✅ Perfect Forward Secrecy (PFS) habilitado
```

**Headers de Segurança Recomendados:**
```
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block
Content-Security-Policy: default-src 'self'
```

### 2.3 Classificação de Dados

```
┌─────────────────────────────────────────────────────────────┐
│ 🔴 CRÍTICO (máxima proteção)                               │
│ • CPF, RG, dados de pagamento                              │
│ • Diagnósticos, medicamentos                               │
│ • Dados de login, senhas                                   │
│ Proteção: AES-256, audit log, backup seguro               │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ 🟡 SENSÍVEL (proteção elevada)                             │
│ • Histórico médico completo                                │
│ • Telefone, email, endereço                                │
│ • Data de nascimento                                       │
│ Proteção: Criptografia, controle de acesso rigoroso       │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ 🟢 NORMAL (proteção padrão)                                │
│ • Agendamentos futuros                                     │
│ • Feedback e comentários                                   │
│ • Horários de disponibilidade                              │
│ Proteção: Controle de acesso básico                       │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ ⚪ PÚBLICO (sem restrição)                                 │
│ • Horário de funcionamento da clínica                      │
│ • Especialidades oferecidas                                │
│ • Telefone geral (público)                                 │
│ Proteção: Nenhuma restrição necessária                     │
└─────────────────────────────────────────────────────────────┘
```

---

## 3. Proteção do Banco de Dados

### 3.1 Estrutura Segura

#### ✅ Prevenção de SQL Injection

```javascript
// ❌ NUNCA fazer isso:
db.query(`SELECT * FROM pacientes WHERE id = ${userInput}`);

// ✅ SEMPRE fazer assim:
db.query('SELECT * FROM pacientes WHERE id = ?', [userInput]);

// Usando ORM (Sequelize, TypeORM):
const paciente = await Paciente.findByPk(userId);
```

#### ✅ Validação de Entrada

```javascript
// Exemplo com joi
const schema = Joi.object({
  cpf: Joi.string().length(11).pattern(/^\d+$/).required(),
  email: Joi.string().email().required(),
  telefone: Joi.string().pattern(/^\d{10,11}$/).required(),
  dataNascimento: Joi.date().max('now').required()
});

const { error, value } = schema.validate(userInput);
if (error) {
  return res.status(400).json({ erro: error.details[0].message });
}
```

#### ✅ Soft Delete (Lógico)

```javascript
// Criar coluna deleted_at
ALTER TABLE pacientes ADD COLUMN deleted_at TIMESTAMP NULL;

// Ao deletar, apenas marcar
UPDATE pacientes SET deleted_at = NOW() WHERE id = ?;

// Queries sempre excluem dados "deletados"
SELECT * FROM pacientes WHERE deleted_at IS NULL;
```

### 3.2 Backup e Recuperação

| Aspecto | Especificação |
|---------|---------------|
| **Frequência** | Diário (automático), full + incremental |
| **Horário** | Fora do pico de uso (madrugada) |
| **Retenção** | 5 anos (conforme LGPD) |
| **Armazenamento** | Offline (HD externo) + Cloud (AWS S3, Azure) |
| **Criptografia** | AES-256 com chave separada |
| **Testes** | Teste de recuperação mensal |
| **Documentação** | Procedimento de restore documentado |

**Cronograma Sugerido:**
```
Segunda a Sexta:  Backup incremental diário (22h)
Sábado:           Backup full (22h)
Domingo:          Verificação de integridade
```

### 3.3 Isolamento de Dados (Multi-tenant)

```javascript
// Se plataforma atender múltiplas clínicas:

// ✅ Schema separation (PostgreSQL):
CREATE SCHEMA clinica_001;
CREATE SCHEMA clinica_002;
CREATE TABLE clinica_001.pacientes (...);
CREATE TABLE clinica_002.pacientes (...);

// ✅ Row-level security (RLS):
ALTER TABLE pacientes ENABLE ROW LEVEL SECURITY;

CREATE POLICY pacientes_isolation ON pacientes
  USING (clinica_id = current_setting('app.clinica_id')::uuid);

// ✅ Sempre validar clinica_id em queries
SELECT * FROM pacientes 
WHERE clinica_id = $1 AND id = $2;
```

---

## 4. Proteção da API

### 4.1 Rate Limiting e DDoS

```javascript
// Express Rate Limit
const rateLimit = require('express-rate-limit');

// Limite geral
const limiter = rateLimit({
  windowMs: 1 * 60 * 1000,      // 1 minuto
  max: 100,                       // 100 requisições
  message: 'Muitas requisições, tente novamente mais tarde'
});

// Limite por usuário (endpoints sensíveis)
const loginLimiter = rateLimit({
  windowMs: 5 * 60 * 1000,        // 5 minutos
  max: 5,                         // 5 tentativas
  skipSuccessfulRequests: true    // não contar sucessos
});

app.use('/api/', limiter);
app.post('/api/v1/auth/login', loginLimiter, loginHandler);
app.post('/api/v1/auth/recuperar-senha', loginLimiter, recoveryHandler);
```

### 4.2 Validação de API

```
✅ CORS: Whitelist apenas domínios autorizados
✅ Versionamento: /api/v1/... (facilita rollback)
✅ Content-Type: Validar application/json
✅ User-Agent: Validar requisições suspeitas
✅ API Keys: Usar para integração com terceiros
✅ Helmet.js: Headers de segurança automáticos
```

**Configuração Helmet.js:**
```javascript
const helmet = require('helmet');

app.use(helmet());
app.use(helmet.contentSecurityPolicy({
  directives: {
    defaultSrc: ["'self'"],
    styleSrc: ["'self'", "'unsafe-inline'"],
    scriptSrc: ["'self'"],
    imgSrc: ["'self'", "data:", "https:"]
  }
}));
```

### 4.3 Documentação Segura

```javascript
// ❌ Não expor informações
X-Powered-By: Express      // ❌ Remover
Server: Apache 2.4.41      // ❌ Remover

// ✅ Headers seguros
const app = express();
app.disable('x-powered-by');

// ❌ Versões de dependências
npm ls axios  // Ocultar em produção

// ✅ Dependências desatualizadas
npm audit fix
npm update
```

---

## 5. Conformidade LGPD

### 5.1 Direitos dos Titulares de Dados

| Direito | Implementação | Prazo |
|--------|---------------|--------|
| **Acesso** | Interface para visualizar todos os dados | 0 dias |
| **Correção** | Formulário para atualizar informações | 0 dias |
| **Exclusão** | Opção "Direito ao esquecimento" | 48 horas |
| **Portabilidade** | Download em JSON/CSV | 0 dias |
| **Oposição** | Opt-out de comunicações marketing | 0 dias |

**Exemplos de Endpoints:**
```
GET /api/v1/pacientes/me/dados              # Acessar dados
PATCH /api/v1/pacientes/me                  # Correção
DELETE /api/v1/pacientes/me/solicitar-delecao  # Exclusão
GET /api/v1/pacientes/me/exportar            # Portabilidade
POST /api/v1/pacientes/me/preferencias       # Preferências
```

### 5.2 Consentimento e Privacidade

```
┌──────────────────────────────────────────────────────────────┐
│ Campos Obrigatórios no Cadastro:                            │
├──────────────────────────────────────────────────────────────┤
│ ☐ Li e aceito a Política de Privacidade                     │
│ ☐ Consinto com coleta e uso de meus dados                   │
│ ☐ Desejo receber comunicações sobre minha saúde             │
│ ☐ Desejo receber newsletters sobre saúde (opcional)         │
└──────────────────────────────────────────────────────────────┘
```

**Registro de Consentimento:**
```javascript
{
  userId: "uuid",
  tipoConsentimento: "CADASTRO_INICIAL",
  dataConsentimento: "2026-09-15T10:30:00Z",
  ipAddress: "192.168.1.100",
  userAgent: "Mozilla/5.0...",
  termosConcordados: [
    { id: "privacidade-v1", versao: "1.0", concordou: true },
    { id: "comunicacoes-v1", versao: "1.0", concordou: true },
    { id: "marketing-v1", versao: "1.0", concordou: false }
  ]
}
```

### 5.3 Data Protection Impact Assessment (DPIA)

**Processamentos que Necessitam DPIA:**
- ✅ Coleta de dados de menores de idade
- ✅ Processamento automatizado com decisões sobre pessoas
- ✅ Vigilância em larga escala
- ✅ Dados relacionados a saúde

**Documento DPIA deve conter:**
1. Descrição do processamento
2. Necessidade e proporcionalidade
3. Avaliação de riscos
4. Medidas de mitigação
5. Consulta com DPO (Data Protection Officer)

---

## 6. Monitoramento e Logging

### 6.1 Logs de Segurança

**O que DEVE ser registrado:**

```
📝 AUTENTICAÇÃO:
   ✓ Login bem-sucedido (usuário, IP, timestamp)
   ✓ Falhas de login (IP, tentativas)
   ✓ Logout (usuário, timestamp)
   ✓ Mudanças de senha
   ✓ Redefinição de MFA

📝 ACESSO A DADOS SENSÍVEIS:
   ✓ Quem acessou
   ✓ Qual dado (paciente, tipo de informação)
   ✓ Quando (timestamp)
   ✓ Resultado (sucesso/falha)

📝 MODIFICAÇÕES:
   ✓ Criação de registros
   ✓ Edição de dados sensíveis (antes/depois)
   ✓ Exclusão lógica (soft delete)
   ✓ Quem fez (usuário/admin)

📝 ERROS:
   ✓ Exceções do sistema
   ✓ Tentativas de SQL injection
   ✓ Requisições suspeitas
   ✓ Timeouts de API
```

**Exemplo de Log Estruturado (JSON):**
```json
{
  "timestamp": "2026-09-15T14:35:22.123Z",
  "nivel": "INFO",
  "tipo_evento": "ACESSO_DADOS_SENSIVEL",
  "usuario_id": "user_12345",
  "usuario_email": "dr.silva@clinica.com",
  "acao": "Visualizou prontuário",
  "recurso": "pacientes/pac_67890/prontuario",
  "tipo_dado": "HISTÓRICO_MÉDICO",
  "ip_address": "192.168.1.100",
  "user_agent": "Mozilla/5.0...",
  "resultado": "sucesso",
  "duracao_ms": 45
}
```

### 6.2 Retenção de Logs

| Tipo de Log | Retenção | Armazenamento |
|------------|----------|---------------|
| **Audit (crítico)** | 2 anos | Offline + Cloud |
| **Acesso a dados sensíveis** | 1 ano | Cloud (criptografado) |
| **Operacional** | 90 dias | Disk local |
| **Erro/Debug** | 30 dias | Disk local |

### 6.3 Alertas e Monitoramento

```javascript
// Exemplo com winston + alertas
const logger = createLogger({
  transports: [
    new transports.File({ filename: 'error.log', level: 'error' }),
    new transports.File({ filename: 'combined.log' })
  ]
});

// Alert: múltiplas falhas de login
function checkLoginFailures(userId, ipAddress) {
  const failures = getFailureCount(userId, ipAddress, '5min');
  if (failures > 5) {
    sendAlert({
      tipo: 'MULTIPLE_LOGIN_FAILURES',
      usuario: userId,
      ip: ipAddress,
      severidade: 'HIGH',
      acao: 'Bloquear IP por 30 minutos'
    });
    blockIP(ipAddress, 30 * 60 * 1000);
  }
}

// Alert: exclusão em massa
function checkMassDelete(tabla, qtdDeleted) {
  if (qtdDeleted > 100) {
    sendAlert({
      tipo: 'MASS_DELETE',
      tabela: tabla,
      quantidade: qtdDeleted,
      severidade: 'CRITICAL',
      acao: 'Verificar permissões'
    });
  }
}
```

---

## 7. Segurança da Infraestrutura

### 7.1 Isolamento de Ambiente

```
┌─────────────────────────────────────────┐
│ DESENVOLVIMENTO                         │
├─────────────────────────────────────────┤
│ Dados: Fictícios (NUNCA reais)          │
│ Banco: SQLite / Docker compose          │
│ Credenciais: Locais, não compartilhadas │
│ Acesso: Apenas desenvolvedores          │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ STAGING                                 │
├─────────────────────────────────────────┤
│ Dados: Sanitizados (PII removido)       │
│ Banco: PostgreSQL separado              │
│ Credenciais: Variáveis de ambiente      │
│ Acesso: Dev team + QA                   │
│ Espelho: Idêntico a produção             │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ PRODUÇÃO                                │
├─────────────────────────────────────────┤
│ Dados: Reais (máxima proteção)          │
│ Banco: PostgreSQL gerenciado            │
│ Credenciais: Vault/KMS                  │
│ Acesso: Apenas admins (restrições)      │
│ Backup: Diário + Off-site               │
└─────────────────────────────────────────┘
```

### 7.2 Gerenciamento de Segredos

```
❌ NUNCA fazer:
├─ DB_PASSWORD=senha123 no .env
├─ API_KEY no código
├─ Credentials no Git
└─ Hardcoding de chaves

✅ SEMPRE fazer:
├─ AWS Secrets Manager
├─ HashiCorp Vault
├─ Azure Key Vault
├─ Environment variables em CI/CD
├─ Chaves rotacionadas a cada 90 dias
└─ Acesso limitado (princípio do menor privilégio)
```

**Exemplo com AWS Secrets Manager:**
```javascript
const AWS = require('aws-sdk');
const client = new AWS.SecretsManager({ region: 'us-east-1' });

async function getDatabaseCredentials() {
  try {
    const secret = await client.getSecretValue({ 
      SecretId: 'rede-cuidar/db-prod' 
    }).promise();
    
    return JSON.parse(secret.SecretString);
  } catch (error) {
    logger.error('Falha ao obter credenciais', error);
    process.exit(1);
  }
}
```

### 7.3 Firewall e Rede

```
🔒 FIREWALL (WAF - Web Application Firewall):
   • Detectar/bloquear ataques SQL injection
   • Bloqueio de XSS
   • Proteção contra brute force
   • Rate limiting automático
   • Exemplo: AWS WAF, Cloudflare, ModSecurity

🔒 IP WHITELIST (Administrativos):
   • Apenas IPs da clínica para admin panel
   • VPN obrigatória para acesso remoto
   • Monitoramento de conexões suspeitas

🔒 REDE (VPC):
   • Isolamento em VPC privada
   • Security groups restritivos
   • Apenas portas necessárias abertas
   • SSH com chaves (não senhas)
```

---

## 8. Segurança no Front-End

### 8.1 Proteções Contra Ataques Comuns

#### XSS (Cross-Site Scripting)

```javascript
// ❌ VULNERÁVEL:
<div>{userComment}</div>  // Se userComment = <script>alert('xss')</script>

// ✅ SEGURO (React sanitiza por padrão):
<div>{userComment}</div>

// ✅ Se precisar renderizar HTML:
import DOMPurify from 'dompurify';

const sanitized = DOMPurify.sanitize(userComment);
<div dangerouslySetInnerHTML={{ __html: sanitized }} />
```

#### CSRF (Cross-Site Request Forgery)

```javascript
// ✅ Implementar CSRF tokens:
// Backend:
app.use(csrf());

app.get('/form', (req, res) => {
  res.render('form', { csrfToken: req.csrfToken() });
});

// Frontend:
<form method="POST" action="/submit">
  <input type="hidden" name="_csrf" value="<%= csrfToken %>" />
  <input type="text" name="dados" />
</form>
```

#### Clickjacking

```javascript
// Express
app.use((req, res, next) => {
  res.setHeader('X-Frame-Options', 'DENY');
  // Opções: DENY, SAMEORIGIN, ALLOW-FROM uri
  next();
});
```

### 8.2 Armazenamento de Dados Sensíveis

```javascript
// ❌ NUNCA fazer isso:
localStorage.setItem('auth_token', jwtToken);  // Vulnerável a XSS

// ✅ FAZER ASSIM:
// Backend define cookie com JWT
res.cookie('auth_token', jwtToken, {
  httpOnly: true,      // Inacessível por JavaScript
  secure: true,        // Apenas HTTPS
  sameSite: 'Strict',  // Proteção CSRF
  maxAge: 3600000      // 1 hora
});

// Frontend: Nunca armazena token
// Requisições incluem cookie automaticamente

// Logout: Limpar dados
function logout() {
  // Remover dados locais
  sessionStorage.clear();
  localStorage.clear();
  
  // Chamar backend para invalidar sessão
  fetch('/api/v1/auth/logout', { method: 'POST' });
  
  // Redirecionar
  window.location.href = '/login';
}
```

---

## 9. Testes de Segurança

### 9.1 Testes Automatizados

#### SAST (Static Application Security Testing)

```bash
# SonarQube
npm install -D sonarqube-scanner
sonar-scanner \
  -Dsonar.projectKey=rede-cuidar \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000

# ESLint com plugins de segurança
npm install -D eslint-plugin-security
# .eslintrc.json
{
  "plugins": ["security"],
  "extends": ["plugin:security/recommended"]
}
```

#### DAST (Dynamic Testing)

```bash
# OWASP ZAP
docker run -t owasp/zap2docker-stable \
  zap-baseline.py -t https://cuidar-plus.com

# Burp Suite Community
# Ferramenta interativa para testes manuais
```

#### Dependency Scanning

```bash
# npm audit (nativo)
npm audit
npm audit fix

# Snyk (mais detalhado)
npm install -g snyk
snyk test
snyk monitor
```

### 9.2 Testes Manuais

```
✅ Teste de Penetração:
   Contatar profissional especializado
   Frequência: Anual ou antes de release major
   Escopo: Incluir API, front-end, banco de dados
   Relatório com vulnerabilidades

✅ Revisão de Código Focada em Segurança:
   Checklist de segurança em PRs
   Dois reviewers para código crítico
   Atenção: SQL injection, XSS, autenticação

✅ Teste de Casos Extremos (Boundary Testing):
   Inputs muito grandes (buffer overflow)
   Valores nulos/undefined
   Caracteres especiais e unicode
   Limites numéricos
```

---

## 10. Plano de Resposta a Incidentes

### 10.1 Procedimento

```
╔════════════════════════════════════════════════════════════╗
║ 1️⃣  DETECÇÃO                                              ║
╠════════════════════════════════════════════════════════════╣
║ • Alerta automático do sistema                             ║
║ • Relatório manual de usuário                              ║
║ • Monitoramento de logs                                    ║
║ → Ativar time de resposta                                  ║
╚════════════════════════════════════════════════════════════╝

╔════════════════════════════════════════════════════════════╗
║ 2️⃣  CONTENÇÃO (primeiras 2 horas)                         ║
╠════════════════════════════════════════════════════════════╣
║ • Isolar afetado (desativar usuário, bloquear IP)          ║
║ • Parar a propagação (se malware)                          ║
║ • Aviso interno ao time                                    ║
║ • Iniciar log detalhado                                    ║
╚════════════════════════════════════════════════════════════╝

╔════════════════════════════════════════════════════════════╗
║ 3️⃣  INVESTIGAÇÃO (até 24 horas)                           ║
╠════════════════════════════════════════════════════════════╣
║ • Analisar logs de segurança                               ║
║ • Timeline do incidente                                    ║
║ • Dados potencialmente expostos                            ║
║ • Origem e causa raiz                                      ║
║ • Documentar descobertas                                   ║
╚════════════════════════════════════════════════════════════╝

╔════════════════════════════════════════════════════════════╗
║ 4️⃣  NOTIFICAÇÃO (até 72 horas - LGPD)                    ║
╠════════════════════════════════════════════════════════════╣
║ • Informar usuários afetados                               ║
║ • Comunicado transparente                                  ║
║ • Orientações de proteção                                  ║
║ • Notificar órgãos se necessário                           ║
╚════════════════════════════════════════════════════════════╝

╔════════════════════════════════════════════════════════════╗
║ 5️⃣  REMEDIAÇÃO (até 7 dias)                               ║
╠════════════════════════════════════════════════════════════╣
║ • Corrigir vulnerabilidade                                 ║
║ • Deploy de patch                                          ║
║ • Testes completos                                         ║
║ • Monitoramento intensivo                                  ║
╚════════════════════════════════════════════════════════════╝

╔════════════════════════════════════════════════════════════╗
║ 6️⃣  POST-MORTEM                                           ║
╠════════════════════════════════════════════════════════════╣
║ • Lições aprendidas                                        ║
║ • Melhorias no processo                                    ║
║ • Atualizações de políticas                                ║
║ • Treinamento do time                                      ║
╚════════════════════════════════════════════════════════════╝
```

### 10.2 Time de Resposta

| Papel | Responsável | Contato | Disponibilidade |
|------|-------------|---------|-----------------|
| **Coordenador** | Calebe (Seg. Info) | calebe@rede-cuidar.com | 24/7 em emergência |
| **Dev Lead** | Tayrone (Back-end) | tayrone@rede-cuidar.com | 24/7 em emergência |
| **DBA** | Cristian (BD) | cristian@rede-cuidar.com | 24/7 em emergência |
| **Legal/Compliance** | [a definir] | ... | Horário comercial |

**Procedimento de Escalação:**
```
Incidente Detectado (0h)
     ↓
Contatar Calebe (coordenador)
     ↓ (30 min)
Escalar para Tayrone + Cristian
     ↓ (1 hora)
Iniciar log formal de incidente
     ↓ (2 horas)
Comunicado ao cliente se necessário
     ↓ (24 horas)
Notificação pública/reguladores (72h máx)
```

---

## 📊 Priorização Rápida (MVP)

### 🔴 CRÍTICO (Implementar AGORA)

**Timeline: Até 21/09/2026**

- [ ] **Autenticação segura**
  - [ ] Hash bcrypt para senhas
  - [ ] JWT com refresh tokens
  - [ ] 2FA para funcionários
  - Responsável: **Tayrone**

- [ ] **SSL/TLS**
  - [ ] Certificado válido (Let's Encrypt)
  - [ ] HTTPS em toda aplicação
  - [ ] Headers HSTS
  - Responsável: **Tayrone + Cristian**

- [ ] **Prevenção SQL Injection**
  - [ ] Parameterized queries em todas as queries
  - [ ] Validação de entrada
  - Responsável: **Tayrone + Carlos**

- [ ] **Logs de Acesso**
  - [ ] Registrar acessos a dados sensíveis
  - [ ] Login/logout + IP
  - [ ] Armazenar com timestamp
  - Responsável: **Tayrone**

- [ ] **Backup Automático**
  - [ ] Script de backup diário
  - [ ] Armazenamento seguro
  - [ ] Teste de restauração
  - Responsável: **Cristian**

---

### 🟡 IMPORTANTE (Próximas 2 semanas)

**Timeline: 22/09 - 05/10/2026**

- [ ] **Criptografia de Dados Sensíveis**
  - [ ] AES-256 para CPF, email, etc
  - [ ] Configurar AWS KMS ou similar
  - Responsável: **Calebe + Cristian**

- [ ] **Rate Limiting e CAPTCHA**
  - [ ] Limite de login (5 tentativas/5 min)
  - [ ] CAPTCHA na 3ª falha
  - [ ] Rate limiting global (100 req/min)
  - Responsável: **Tayrone**

- [ ] **Política de Privacidade LGPD**
  - [ ] Documento legal completo
  - [ ] Termo de consentimento
  - [ ] Interface de privacidade no app
  - Responsável: **Calebe + [Legal]**

- [ ] **Validação de Segurança de API**
  - [ ] CORS configurado
  - [ ] Headers de segurança (Helmet)
  - [ ] Content-Type validation
  - Responsável: **Tayrone**

- [ ] **Segurança Front-End**
  - [ ] Sanitização de inputs (DOMPurify)
  - [ ] CSRF tokens
  - [ ] httpOnly cookies
  - Responsável: **Vinicius**

---

### 🟢 COMPLEMENTAR (Depois de Launch)

**Timeline: Após 05/10/2026**

- [ ] Teste de Penetração Profissional
- [ ] WAF (Web Application Firewall)
- [ ] MFA para Pacientes
- [ ] Sistema de Auditoria Completo
- [ ] Monitoramento 24/7
- [ ] Plano de Disaster Recovery
- [ ] Certificação SOC 2 Type II

---

## 📋 Checklist de Deploy Seguro

```
Antes de fazer deploy em produção:

[ ] Todos testes de segurança passando
[ ] Logs configurados e testados
[ ] Backup testado e funcionando
[ ] Certificado SSL válido
[ ] Senhas e chaves rotacionadas
[ ] Firewall/WAF ativado
[ ] Rate limiting ativo
[ ] Monitoramento ligado
[ ] Documentação atualizada
[ ] Time notificado do procedimento
[ ] Rollback plan pronto
[ ] Comunicado ao cliente pronto (se necessário)

Deploy em horário de baixo uso:
- Não antes de sexta à noite
- Não durante manutenção de DB
- Mínimo 2 pessoas no time
```

---

## 📚 Referências e Recursos

### Frameworks e Bibliotecas
- **Express + Helmet.js**: Headers de segurança automáticos
- **bcrypt**: Hashing de senhas
- **jsonwebtoken**: Tokens JWT
- **joi**: Validação de schema
- **cors**: Configuração CORS
- **DOMPurify**: Sanitização HTML
- **winston**: Logging estruturado

### Padrões e Standards
- **OWASP Top 10**: Vulnerabilidades mais críticas
- **NIST Cybersecurity Framework**: Best practices
- **ISO 27001**: Gestão de segurança da informação
- **LGPD**: Lei Geral de Proteção de Dados (Brasil)

### Ferramentas
- **npm audit**: Verificar dependências vulneráveis
- **SonarQube**: Code quality + security
- **OWASP ZAP**: Teste de segurança dinâmico
- **Snyk**: Monitoramento de vulnerabilidades

### Documentos Externos
- [OWASP Top 10 2021](https://owasp.org/Top10/)
- [LGPD - Lei 13.709/2018](https://www.gov.br/cidadania/pt-br/acesso-a-informacao/lgpd)
- [NIST Cybersecurity](https://www.nist.gov/cyberframework)

---

## 📞 Contato e Dúvidas

**Responsável de Segurança:** Calebe  
**Email:** calebe@rede-cuidar.com  
**Escalação:** Tayrone (Dev Lead)

---

**Versão:** 1.0  
**Última Atualização:** Setembro de 2026  
**Status:** ✅ Aprovado para implementação

