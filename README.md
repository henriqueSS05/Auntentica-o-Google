# 🔐 Autenticação com Google

Este projeto implementa autenticação com Google utilizando **Google Identity Services** no front-end e **Node.js** no back-end para validar o token enviado pelo Google.

## 📋 Pré-requisitos

* Node.js 18 ou superior
* Conta Google
* Projeto criado no Google Cloud Console

## 🚀 Configuração do Google Cloud

### 1. Criar um projeto

Acesse o Google Cloud Console e crie um novo projeto.

### 2. Configurar a Tela de Consentimento OAuth

1. Vá em **APIs e Serviços → Tela de Consentimento OAuth**.
2. Escolha o tipo de usuário (Externo ou Interno).
3. Preencha as informações obrigatórias:

   * Nome do aplicativo
   * E-mail de suporte
   * E-mail do desenvolvedor
4. Salve as configurações.

### 3. Criar um ID do Cliente OAuth

1. Acesse **APIs e Serviços → Credenciais**.
2. Clique em **Criar Credenciais**.
3. Selecione **ID do Cliente OAuth**.
4. Escolha **Aplicativo da Web**.
5. Defina um nome para a credencial.

### 4. Configurar as Origens Autorizadas

#### Desenvolvimento

```
http://localhost:3000
```

#### Produção

```
https://seudominio.com
```

### 5. Configurar os URIs de Redirecionamento (caso utilize OAuth tradicional)

#### Desenvolvimento

```
http://localhost:3000/auth/google/callback
```

#### Produção

```
https://seudominio.com/auth/google/callback
```

Após criar a credencial, copie o **Client ID**.

---

# 📦 Instalação

Instale as dependências:

```bash
npm install express google-auth-library
```

---

# 📁 Estrutura

```
projeto/
│
├── public/
│   ├── index.html
│   └── java.js
│
├── server.js (opcional caso tenha banco de dados)
│
├── token.json (Precisa ser criado para uso)
└── README.md
```

---

# 💻 Front-end

Adicione o script do Google Identity Services:

```html
<script src="https://accounts.google.com/gsi/client" async defer></script>
```

Crie o botão de login:

```html
<div
    id="g_id_onload"
    data-client_id="SEU_CLIENT_ID"
    data-callback="handleCredentialResponse">
</div>

<div class="g_id_signin"></div>
```

---

# 🖥️ Back-end

Valide o token recebido utilizando a biblioteca oficial do Google.

Fluxo:

```
Usuário
    │
    ▼
Botão Google
    │
    ▼
Google gera Token
    │
    ▼
Node.js recebe Token
    │
    ▼
Google valida Token
    │
    ▼
Usuário autenticado
```

---

# 🗄️ Banco de Dados (Opcional)

Caso utilize banco de dados, recomenda-se armazenar:

* ID
* Nome
* E-mail
* Foto
* Data de criação

Exemplo:

```sql
CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    email VARCHAR(150) UNIQUE,
    foto TEXT,
    criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Ao autenticar:

1. Verifique se o e-mail já existe.
2. Caso não exista, crie o usuário.
3. Caso exista, apenas realize o login.

---

# 🔒 Segurança

* Nunca confie apenas nas informações enviadas pelo navegador.
* Sempre valide o ID Token no servidor.
* Nunca exponha chaves privadas no front-end.
* Utilize HTTPS em produção.
* Proteja rotas privadas utilizando sessões ou JWT.

---

# 🧪 Desenvolvimento

Execute o servidor:

```bash
npm start
```

ou

```bash
node server.js
```

A aplicação ficará disponível em:

```
http://localhost:3000
```

---

# 📚 Tecnologias

* HTML5
* CSS3
* JavaScript
* Node.js
* Express
* Google Identity Services
* Google Auth Library

---

# 📖 Referências

* Google Identity Services
* Google Cloud Console
* OAuth 2.0
* Node.js
* Express

---

# 👨‍💻 Autor

Henrique Soares Souza
