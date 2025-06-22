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
