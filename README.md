# 📱 Sistema de Assistência Técnica de Celulares

Sistema web desenvolvido para gerenciamento de uma assistência técnica de celulares, permitindo controlar clientes, aparelhos, serviços e agendamentos de manutenção e reparo.

O projeto foi desenvolvido utilizando Python, Flask e MySQL, com foco na organização dos cadastros, integridade dos dados, autenticação de usuários e segurança das informações.

---

## 📋 Funcionalidades

### 🔐 Autenticação e segurança
- Login de usuários com autenticação por senha.
- Proteção das páginas internas contra acessos não autorizados.
- Gerenciamento de sessões com expiração após 30 minutos.
- Armazenamento de senhas utilizando hash com bcrypt.

### 👥 Gerenciamento de clientes
- Cadastro de clientes.
- Consulta e pesquisa por nome ou CPF.
- Edição dos dados cadastrados.
- Validação de CPF.
- Impedimento de CPFs duplicados.
- Armazenamento de CPF utilizando hash bcrypt.

### 📱 Gerenciamento de aparelhos
- Cadastro de aparelhos vinculados a clientes.
- Registro de marca, modelo, IMEI e defeito apresentado.
- Validação de IMEI com 15 dígitos.
- Impedimento de IMEIs duplicados.
- Edição e exclusão de aparelhos.
- Proteção contra exclusão de aparelhos vinculados a agendamentos.

### 📅 Gerenciamento de agendamentos
- Cadastro de agendamentos de serviços.
- Associação entre clientes, aparelhos e serviços.
- Consulta de agendamentos.
- Reagendamento de serviços.
- Ordenação dos agendamentos por data.

---

## 🛠️ Tecnologias utilizadas

| Tecnologia | Finalidade |
|---|---|
| Python 3.10+ | Linguagem principal |
| Flask | Desenvolvimento do sistema web |
| MySQL 8+ | Banco de dados relacional |
| bcrypt | Proteção de senhas e dados sensíveis |
| mysql-connector-python | Conexão com o banco de dados |
| HTML5 | Estrutura das páginas |
| CSS3 | Estilização das interfaces |
| JavaScript | Interatividade das páginas |

---

## 📂 Estrutura do projeto

```text
projeto/
│
├── sistema/
│   ├── app.py
│   ├── autenticacao.py
│   ├── testar_conexao.py
│   ├── requirements.txt
│   ├── templates/
│   ├── static/
│   └── ...
│
├── saep_db.sql
├── documentacao.pdf
├── der.png
└── README.md
```

*Observação: a estrutura acima representa a organização esperada dos principais arquivos. Os diretórios internos podem variar conforme a implementação.*

---

## ⚙️ Pré-requisitos

Antes de executar o projeto, certifique-se de possuir:

- Python 3.10 ou superior.
- MySQL 8.0 ou superior.
- MySQL Server em execução.
- Git (opcional).

---

## 🚀 Instalação e configuração

### 1. Clonar ou baixar o projeto

```bash
git clone URL_DO_REPOSITORIO
```

Ou extraia os arquivos do projeto em uma pasta de sua preferência.

### 2. Acessar a pasta do sistema

```bash
cd sistema
```

### 3. Criar o ambiente virtual

```bash
python -m venv venv
```

Ative o ambiente virtual:

**Windows (CMD):**
```cmd
venv\Scripts\activate
```

**Windows (PowerShell):**
```powershell
.\venv\Scripts\Activate.ps1
```

**Linux/macOS:**
```bash
source venv/bin/activate
```

### 4. Instalar as dependências

```bash
pip install -r requirements.txt
```

As principais dependências incluem Flask, bcrypt e mysql-connector-python.

### 5. Criar o banco de dados

Com o MySQL em execução, acesse a pasta raiz do projeto e execute:

```bash
mysql -u root -p < saep_db.sql
```

O script SQL será responsável pela criação e inicialização do banco de dados `saep_db`.

### 6. Configurar as variáveis de ambiente

Configure as credenciais utilizadas na conexão com o banco de dados e a chave de segurança da aplicação.

**Windows (PowerShell):**
```powershell
$env:DB_USER="root"
$env:DB_PASSWORD="sua_senha"
$env:SECRET_KEY="sua_chave_secreta"
```

**Linux/macOS:**
```bash
export DB_USER=root
export DB_PASSWORD=sua_senha
export SECRET_KEY=sua_chave_secreta
```

Substitua os valores de exemplo pelas configurações do seu ambiente.

### 7. Testar a conexão com o banco

Dentro da pasta `sistema`, execute:

```bash
python testar_conexao.py
```

Resultado esperado:

```text
Conexão OK: {'banco': 'saep_db', 'versao': '8.x'}
```

### 8. Executar o sistema

Ainda dentro da pasta `sistema`, execute:

```bash
python app.py
```

Acesse pelo navegador:

http://localhost:5000

---

## 🔑 Acesso ao sistema

Para o ambiente de demonstração, utilize as credenciais iniciais:

| Campo | Valor |
|---|---|
| Usuário | admin |
| Senha | admin123 |

**Importante:** essas credenciais são destinadas ao ambiente de testes. Em ambientes reais, utilize senhas fortes e altere as credenciais padrão.

---

## 🧪 Testes e validações

O sistema pode ser verificado por meio dos seguintes cenários:

| Módulo | Teste | Resultado esperado |
|---|---|---|
| Login | Credenciais incorretas | Acesso negado |
| Login | Campos vazios | Solicitação de preenchimento |
| Login | Credenciais válidas | Acesso à tela principal |
| Clientes | CPF inválido | Mensagem de validação |
| Clientes | CPF duplicado | Cadastro impedido |
| Clientes | Pesquisa por nome ou CPF | Resultados correspondentes |
| Aparelhos | IMEI inválido | Cadastro impedido |
| Aparelhos | IMEI duplicado | Cadastro impedido |
| Aparelhos | Cadastro sem cliente | Cadastro impedido |
| Agendamentos | Criar agendamento | Registro realizado |
| Agendamentos | Reagendar | Data atualizada |
| Sessão | Acesso sem autenticação | Redirecionamento para login |
| Sessão | Expiração após inatividade | Sessão encerrada |

---

## 🔌 Endpoints de API

O projeto também disponibiliza endpoints para testes e operações via API.

| Método | Endpoint | Finalidade |
|---|---|---|
| POST | `/api/login` | Autenticação |
| GET | `/api/teste-conexao` | Verificação da conexão com o banco |
| GET | `/api/clientes?q=maria` | Pesquisa de clientes |

Exemplo de autenticação utilizando cURL:

```bash
curl -c c.txt -H "Content-Type: application/json" -d "{\"login\":\"admin\",\"senha\":\"admin123\"}" http://localhost:5000/api/login
```

Teste da conexão:

```bash
curl -b c.txt http://localhost:5000/api/teste-conexao
```

Pesquisa de clientes:

```bash
curl -b c.txt "http://localhost:5000/api/clientes?q=maria"
```

---

## 🗄️ Banco de dados

O banco de dados utilizado pelo projeto é o `saep_db`, desenvolvido em MySQL.

Entre as principais entidades estão:

- **Usuários:** informações de autenticação e acesso.
- **Clientes:** dados dos clientes cadastrados.
- **Aparelhos:** informações dos celulares recebidos pela assistência.
- **Serviços:** tipos de serviços disponibilizados.
- **Agendamentos:** registros de serviços programados.

O relacionamento entre as entidades garante a integridade das informações e permite associar clientes, aparelhos e serviços aos respectivos agendamentos.

O arquivo `saep_db.sql` contém o script de criação e população inicial do banco de dados.

---

## 📦 Entrega do projeto

A entrega deve conter os seguintes arquivos:

```text
SeuNomeCompleto.zip
│
├── documentacao.pdf
├── der.png
├── saep_db.sql
└── sistema/
    ├── app.py
    ├── autenticacao.py
    ├── testar_conexao.py
    ├── requirements.txt
    └── ...
```

---

## 👨‍💻 Considerações finais

O Sistema de Assistência Técnica de Celulares tem como objetivo facilitar o gerenciamento das atividades de uma assistência técnica, centralizando informações de clientes, aparelhos e agendamentos em uma única aplicação.

O desenvolvimento contempla conceitos de programação em Python, desenvolvimento web, banco de dados relacionais, autenticação, validação de dados e segurança da informação.
