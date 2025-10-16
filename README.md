# Login Page Frontend

## Visão Geral do Projeto
Este projeto é o **frontend** de uma aplicação de login simples, desenvolvido em **Angular**, consumindo a **API Spring Boot** do backend para autenticação de usuários via **JWT token**.  
O objetivo é fornecer uma interface limpa e funcional para login e acesso a rotas protegidas.

---

## Tecnologias Utilizadas
- **Angular 15+**
- **TypeScript**
- **Angular CLI**
- **RxJS**
- **Bootstrap / CSS**
- **HttpClient (Angular)**

---

- **Components:** Contém os componentes da interface, como formulário de login.  
- **Services:** Serviços Angular para comunicação com a API backend.  
- **Guards:** Protege rotas que necessitam de autenticação.  
- **Routing Module:** Gerencia rotas públicas e protegidas.  

---

## Fluxo de Autenticação (JWT)
1. Usuário digita `email` e `password` no formulário de login.  
2. O **LoginComponent** chama o **AuthService** para enviar a requisição POST para o backend:  
POST http://localhost:8080/auth/login

3. Backend retorna um **JWT token** se as credenciais forem válidas.  
4. O token é armazenado no **localStorage** ou **sessionStorage**.  
5. Para acessar rotas protegidas, o **AuthGuard** adiciona o token no header `Authorization: Bearer <token>`.

---

## Serviços Principais
### AuthService
- `login(credentials: {email, password})` → Faz requisição ao backend e salva token.  
- `logout()` → Remove token do storage.  
- `isLoggedIn()` → Retorna true se houver token válido.

### AuthGuard
- Protege rotas que necessitam de autenticação.  
- Redireciona para a página de login caso o usuário não esteja autenticado.

---

## Como Executar o Projeto Localmente

### Pré-requisitos
- Node.js 18+  
- Angular CLI 15+  
- Backend rodando em `http://localhost:8080`  

### Passos para execução
1. Clone o repositório:
```bash
git clone https://github.com/luizgabb/login-page-fullstack.git
Entre na pasta do projeto:

bash
Copiar código
cd login-page-fullstack
Instale as dependências:

bash
Copiar código
npm install
Rode o projeto:

bash
Copiar código
ng serve
Acesse no navegador: http://localhost:4200

Configurações / Variáveis de Ambiente
Crie um arquivo src/environments/environment.ts com a URL do backend:

typescript
Copiar código
export const environment = {
  production: false,
  apiUrl: 'http://localhost:8080'
};
Para produção, use environment.prod.ts com a URL do servidor.

Integração com Backend
Endpoint de login: POST /auth/login

Endpoint de usuário logado: GET /users/me (precisa do header Authorization: Bearer <token>)

O frontend deve armazenar o token retornado e enviar em todas requisições protegidas.

Exemplo de requisição com HttpClient:

typescript
Copiar código
this.http.get(`${environment.apiUrl}/users/me`, {
  headers: { Authorization: `Bearer ${localStorage.getItem('token')}` }
});
Boas Práticas Implementadas
Guardas de rotas para proteger páginas privadas.

Armazenamento seguro do JWT (localStorage).

Serviço único de autenticação para centralizar lógica.

Componentização limpa do formulário de login.

Possíveis Melhorias Futuras
Validação avançada de formulário com mensagens de erro detalhadas.

Tela de cadastro de usuários (integrando com backend).

Refresh token para manter sessão ativa sem login constante.

Design responsivo completo com Angular Material ou Tailwind CSS.

Licença
Este projeto é open source, livre para uso e estudo.
