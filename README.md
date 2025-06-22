#NestJS

Para criar um projeto NestJS no VS Code, siga os passos abaixo. O NestJS é um framework moderno para Node.js que utiliza TypeScript e é bastante usado para criar APIs robustas e escaláveis.

---

## ✅ Pré-requisitos

Antes de começar, você precisa ter instalado:

1. **Node.js** (versão LTS)
   👉 Baixe em: [https://nodejs.org](https://nodejs.org)
   Verifique no terminal:

   ```bash
   node -v
   npm -v
   ```

2. **npm** (vem com o Node.js) ou **yarn**

3. **Nest CLI** (Interface de linha de comando do NestJS):
   Instale com:

   ```bash
   npm i -g @nestjs/cli
   ```

4. **Visual Studio Code** instalado
   👉 [https://code.visualstudio.com/](https://code.visualstudio.com/)

---

## 🚀 Criando o Projeto

1. **Abra o terminal no VS Code** ou terminal do sistema.

2. Execute o comando para criar o projeto:

   ```bash
   nest new nome-do-projeto
   ```

   Exemplo:

   ```bash
   nest new recording
   ```

3. **Escolha o gerenciador de pacotes** (`npm` ou `yarn`) quando solicitado.

4. O NestJS criará a estrutura básica do projeto com os seguintes diretórios:

   ```
   src/
   ├── app.controller.spec.ts
   ├── app.controller.ts
   ├── app.module.ts
   ├── app.service.ts
   └── main.ts
   ```

---

main.ts Esse código é o ponto de entrada principal de uma aplicação NestJS

## ▶️ Rodando o Projeto

Entre na pasta do projeto:

```bash
cd recording
```

Execute o projeto com:

```bash
npm run start:dev
```

> O servidor estará rodando em `http://localhost:3000`

---

## 🧪 Testando no Navegador ou Postman

Abra `http://localhost:3000` no navegador.
Você verá:

```
Hello World!
```

---

## 🧩 Dica: Extensões Úteis no VS Code

- **ESLint** – para boas práticas de código
- **Prettier** – para formatação automática
- **NestJS Snippets** – autocompletar para NestJS

---

## 📦 Estrutura típica do NestJS

```
src/
├── main.ts
├── app.module.ts
├── app.controller.ts
├── app.service.ts
```

# main.ts

Esse código é o **ponto de entrada principal** de uma aplicação NestJS — normalmente está no arquivo `main.ts`. Vamos analisar linha por linha:

---

### 📦 Código

```ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
```

- **`NestFactory`**: É uma classe do NestJS usada para **criar uma instância da aplicação Nest**.
- **`AppModule`**: É o **módulo raiz** da aplicação — onde os controladores, serviços e outros módulos são registrados.

---

### 🚀 Função `bootstrap()`

```ts
async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(process.env.PORT ?? 3000);
}
```

- **`bootstrap()`**: Função que **inicializa a aplicação**.
- `NestFactory.create(AppModule)`: Cria a aplicação Nest usando o módulo principal.
- `app.listen(...)`: Coloca o servidor para escutar requisições HTTP na porta especificada.

A linha:

```ts
await app.listen(process.env.PORT ?? 3000);
```

- Verifica se existe uma variável de ambiente chamada `PORT` (útil para ambientes de produção como Heroku).
- Se não houver, usa a **porta padrão 3000**.

---

### 🏁 E por fim:

```ts
bootstrap();
```

- **Chama a função `bootstrap()`** para rodar o servidor.

---

### 🧠 Em resumo:

Esse código:

✅ Cria a aplicação Nest
✅ Usa o `AppModule` como módulo principal
✅ Inicializa o servidor HTTP
✅ Escuta na porta definida

---

# app.module.ts

Esse código define o **módulo principal** da aplicação NestJS, chamado `AppModule`.

Vamos entender **parte por parte**:

---

### 📦 Código completo

```ts
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

---

## 🧩 Explicando passo a passo

### 🔹 `import { Module } from '@nestjs/common';`

- Importa o **decorador `@Module()`**, que é usado para definir um **módulo NestJS**.

### 🔹 `AppController` e `AppService`

- **`AppController`**: Controlador responsável por lidar com as requisições HTTP (como rotas GET, POST etc).
- **`AppService`**: Serviço responsável pela **lógica de negócio**, chamado dentro do controller.

---

### 🔹 Decorador `@Module({ ... })`

Esse decorador define as **dependências e estruturas** que o módulo usará:

```ts
@Module({
  imports: [], // Outros módulos que esse módulo depende
  controllers: [AppController], // Controladores que lidam com requisições
  providers: [AppService], // Serviços e injeções de dependência
})
```

- **`imports`**: Lista de módulos que esse módulo importa (ex: `TypeOrmModule`, `HttpModule`, etc).
- **`controllers`**: Define quais controladores fazem parte deste módulo.
- **`providers`**: Define os **serviços (e outras classes)** que serão injetáveis (injeção de dependência).

---

## 🧠 Em resumo:

A classe `AppModule`:

✅ Organiza a estrutura do projeto
✅ Conecta controladores e serviços
✅ É o **módulo raiz**, ou seja, o ponto inicial da organização da aplicação

> Tudo no NestJS gira em torno de **módulos**, e `AppModule` é o primeiro deles.

---

# app.controller.ts

Esse código define um **controller no NestJS**, que é responsável por lidar com requisições HTTP — como se fosse o "porta-voz" entre o mundo externo (navegador, Postman, etc) e a lógica interna da aplicação.

---

## 📦 Código analisado

```ts
import { Controller, Get } from '@nestjs/common';
import { AppService } from './app.service';

@Controller()
export class AppController {
  constructor(private readonly appService: AppService) {}

  @Get()
  getHello(): string {
    return this.appService.getHello();
  }
}
```

---

## 🧩 Explicação linha por linha

### 🔹 `import { Controller, Get } from '@nestjs/common';`

- `Controller`: Decorador que marca a classe como um **controlador HTTP**.
- `Get`: Decorador que define um **endpoint HTTP GET**.

---

### 🔹 `@Controller()`

- Define que essa classe vai **responder a requisições HTTP**.
- O parâmetro vazio (`@Controller()`) indica que a **rota base** é `/`.

> Se fosse `@Controller('usuarios')`, o endpoint responderia a `/usuarios`.

---

### 🔹 `constructor(private readonly appService: AppService)`

- O Nest injeta automaticamente o `AppService` aqui.
- Isso é **injeção de dependência** — o controller pode usar os métodos do serviço sem precisar criá-lo manualmente.

---

### 🔹 `@Get()`

- Define que o método abaixo vai responder a **requisições HTTP GET** na **rota base `/`**.

---

### 🔹 `getHello()`

- É o **método que responde à requisição**.
- Ele chama `this.appService.getHello()` — ou seja, delega a resposta ao serviço.

---

### 🔹 `appService.getHello()`

- Esse método geralmente retorna `"Hello World!"` — está definido no `AppService`:

```ts
getHello(): string {
  return 'Hello World!';
}
```

---

## ✅ Em resumo:

Esse controller:

| Rota | Método | Resposta                      |
| ---- | ------ | ----------------------------- |
| `/`  | GET    | `"Hello World!"` (por padrão) |

---

# app.service.ts

Esse código define um **serviço no NestJS** chamado `AppService`. Serviços são usados para conter **lógica de negócio** e podem ser **injetados em controladores ou outros serviços**.

---

## 📦 Código analisado

```ts
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```

---

## 🧩 Explicando parte por parte

### 🔹 `import { Injectable } from '@nestjs/common';`

- Importa o decorador `@Injectable`, que marca a classe como **"injeção de dependência" compatível**.
- Ou seja, o Nest pode **instanciar e fornecer essa classe** automaticamente em outros lugares (ex: controllers, outros services).

---

### 🔹 `@Injectable()`

- Diz ao Nest que essa classe **pode ser injetada em outras classes**.
- É essencial para que o Nest consiga gerenciar e injetar dependências.

---

### 🔹 `export class AppService`

- Define uma **classe pública** chamada `AppService`, que pode ser usada em outros arquivos com `import`.

---

### 🔹 Método `getHello()`

```ts
getHello(): string {
  return 'Hello World!';
}
```

- Um método simples que **retorna a string "Hello World!"**.
- Pode ser chamado de um controller para responder a uma requisição HTTP, como vimos anteriormente.

---

## ✅ Em resumo:

Esse serviço:

- É um **componente reutilizável** que contém a lógica `getHello`.
- Pode ser **injetado** no controller (`AppController`) ou em qualquer outro lugar com:

```ts
constructor(private readonly appService: AppService) {}
```

---

# Teste com Jest

## src/app.controller.spec.ts

Esse código é um **teste automatizado** feito para o NestJS utilizando o **Jest**, que é o framework de testes padrão no Nest.

---

## 🧪 O que esse código faz?

Ele **testa a funcionalidade do controller** `AppController`, verificando se o método `getHello()` está retornando corretamente a string `"Hello World!"`.

---

## 🧩 Explicando o código

```ts
import { Test, TestingModule } from '@nestjs/testing';
import { AppController } from './app.controller';
import { AppService } from './app.service';
```

- Importa utilitários para testes do NestJS e as classes que serão testadas (`AppController`, `AppService`).

---

### 🔹 `describe('AppController', () => { ... })`

- Define um **bloco de testes** para `AppController`.

---

### 🔹 `beforeEach(async () => { ... })`

- Esse bloco roda **antes de cada teste**.
- Cria um **módulo de teste isolado** (`TestingModule`), simulando a aplicação real:

```ts
const app: TestingModule = await Test.createTestingModule({
  controllers: [AppController],
  providers: [AppService],
}).compile();
```

- Depois, pega a instância real do `AppController`:

```ts
appController = app.get<AppController>(AppController);
```

---

### 🔹 `describe('root', ...)` e `it(...)`

```ts
it('should return "Hello World!"', () => {
  expect(appController.getHello()).toBe('Hello World!');
});
```

- Define um **caso de teste**.
- Verifica se `appController.getHello()` retorna a string `"Hello World!"`.

---

## ▶️ Como rodar esse teste no NestJS?

1. Certifique-se de que o projeto foi criado com o CLI (`nest new nome-do-projeto`) — ele já inclui o Jest.

2. No terminal, execute:

```bash
npm run test
```

Ou, para ver em tempo real com recarregamento automático:

```bash
npm run test:watch
```

---

## 📁 Onde salvar esse teste?

Por convenção, o arquivo deve ser salvo como:

```
src/app.controller.spec.ts
```

Ou seja, o nome do arquivo termina com `.spec.ts` para indicar que é um **teste unitário**.

---

## ✅ Em resumo

Esse código:

- Cria um **teste unitário para o controller**
- Simula o NestJS real (módulo, injeção de dependência)
- Verifica se `getHello()` retorna `"Hello World!"`
- Pode ser executado com `npm run test`

---

# teste E2E

Excelente! Esse código é um **teste E2E (fim a fim)** no NestJS, salvo geralmente no arquivo `test/app.e2e-spec.ts`.

Enquanto os testes unitários verificam pedaços isolados da aplicação (como um método), os testes **E2E simulam requisições reais HTTP** e testam **a aplicação como um todo**, como se fosse um usuário acessando a API.

---

## 📦 Código analisado

```ts
import { Test, TestingModule } from '@nestjs/testing';
import { INestApplication } from '@nestjs/common';
import * as request from 'supertest';
import { App } from 'supertest/types';
import { AppModule } from './../src/app.module';
```

### O que está sendo importado?

- `Test`, `TestingModule`: Utilitários para criar um ambiente de testes.
- `INestApplication`: Interface da aplicação Nest.
- `request`: Função do **Supertest**, usada para fazer **requisições HTTP simuladas**.
- `AppModule`: Módulo principal da aplicação Nest (importado da pasta `src/`).

---

## 🧩 Bloco de testes

```ts
describe('AppController (e2e)', () => {
  let app: INestApplication<App>;
```

- Define um **bloco de testes** para `AppController`.
- Cria uma variável `app` que será a aplicação Nest inicializada.

---

### 🔹 `beforeEach(...)`

```ts
beforeEach(async () => {
  const moduleFixture: TestingModule = await Test.createTestingModule({
    imports: [AppModule],
  }).compile();

  app = moduleFixture.createNestApplication();
  await app.init();
});
```

- Antes de cada teste, um módulo completo é criado com o `AppModule`.
- A aplicação Nest é inicializada com `.createNestApplication()`.
- `await app.init()` faz com que a aplicação esteja pronta para ser testada.

---

### 🔹 O teste em si

```ts
it('/ (GET)', () => {
  return request(app.getHttpServer())
    .get('/')
    .expect(200)
    .expect('Hello World!');
});
```

- Faz uma **requisição GET para `/`** (rota raiz).
- Verifica se o status é `200 OK` e o corpo da resposta é `"Hello World!"`.

Esse teste simula o que acontece quando um **usuário real acessa a API**, testando a **integração entre controller, service e configuração do app**.

---

## ▶️ Como rodar o teste E2E?

No terminal, execute:

```bash
npm run test:e2e
```

> Por padrão, esse comando procura por arquivos `*.e2e-spec.ts` na pasta `test/`.

---

## ✅ Em resumo

Esse teste:

| Característica           | Explicação                                                        |
| ------------------------ | ----------------------------------------------------------------- |
| Tipo                     | E2E (fim a fim)                                                   |
| Ferramenta de requisição | `supertest`                                                       |
| O que ele testa          | Se a API responde corretamente a uma requisição GET na raiz (`/`) |
| Expectativa              | Status 200 + `"Hello World!"`                                     |
| Como executar            | `npm run test:e2e`                                                |

---

# Prettier e ESLint

Você está usando duas ferramentas essenciais para manter a qualidade e o estilo do código em projetos TypeScript/NestJS:

- `Prettier` → formata automaticamente o código.
- `ESLint` → analisa o código em busca de **erros e más práticas**.

Vamos entender **cada um dos arquivos** que você mostrou:

---

## 📄 `.prettierrc`

Esse arquivo configura o **Prettier**, que serve apenas para **formatar o código automaticamente** (não faz verificação de erros).

```json
{
  "singleQuote": true,
  "trailingComma": "all"
}
```

### O que essas opções significam?

| Chave                    | Significado                                                                |
| ------------------------ | -------------------------------------------------------------------------- |
| `"singleQuote": true`    | Usa aspas simples (`'`) em vez de aspas duplas (`"`)                       |
| `"trailingComma": "all"` | Adiciona vírgula no final de listas, objetos, etc. — mesmo na última linha |

**Exemplo de código formatado com essas regras:**

```ts
const user = {
  name: 'Leonardo',
  email: 'leo@email.com',
};
```

---

## 📄 `eslint.config.mjs`

Esse arquivo configura o **ESLint**, que é responsável por:

- Verificar erros de sintaxe
- Aplicar boas práticas
- Integrar com o TypeScript
- (Com o plugin) forçar a formatação do Prettier

---

### 📌 Trechos importantes explicados

#### ✅ Ativa o modo TypeScript com tipagem completa:

```ts
import tseslint from 'typescript-eslint';
...
...tseslint.configs.recommendedTypeChecked
```

Isso permite ao ESLint **analisar seu código com o mesmo entendimento do TypeScript**, incluindo checagem de tipos.

---

#### ✅ Integração com Prettier:

```ts
import eslintPluginPrettierRecommended from 'eslint-plugin-prettier/recommended';
```

- Faz o ESLint também aplicar as regras do Prettier.
- Assim, você vê **avisos de formatação no terminal/VS Code** (não só no salvar).

---

#### ✅ Define variáveis globais válidas:

```ts
globals: {
  ...globals.node,
  ...globals.jest,
}
```

- Informa ao ESLint que você usa:

  - Node.js
  - Jest (testes)

---

#### ✅ Regras personalizadas:

```ts
rules: {
  '@typescript-eslint/no-explicit-any': 'off',
  '@typescript-eslint/no-floating-promises': 'warn',
  '@typescript-eslint/no-unsafe-argument': 'warn',
}
```

| Regra                        | Explicação                                     |
| ---------------------------- | ---------------------------------------------- |
| `no-explicit-any: off`       | Permite o uso do tipo `any`                    |
| `no-floating-promises: warn` | Avisa se você esquecer de `await` em `Promise` |
| `no-unsafe-argument: warn`   | Avisa se um argumento pode causar erro de tipo |

---

## ✅ Em resumo

| Arquivo             | Serve para...                         | Impacto no código                                          |
| ------------------- | ------------------------------------- | ---------------------------------------------------------- |
| `.prettierrc`       | Formatar código                       | Aspas simples, vírgulas finais, etc.                       |
| `eslint.config.mjs` | Analisar erros, boas práticas e tipos | Detecta problemas e impõe padrão com TypeScript e Prettier |
