# Construindo-Uma-App-Simples-de-Banco-Com-Typescript

Para criar uma aplicação bancária simples usando TypeScript e Node.js, seguindo os padrões REST. Vamos dividir isso em módulos para manter o código organizado e fácil de manter.

**Módulo 1: Configuração Inicial**
Primeiro, você precisa configurar seu ambiente de desenvolvimento Node.js com TypeScript. Isso inclui a instalação do Node.js, npm (ou yarn), e o TypeScript globalmente em seu sistema. Depois, você pode iniciar um novo projeto com `npm init` e instalar as dependências necessárias, como `express` para o servidor e `typescript` para o suporte ao TypeScript.

```bash
npm init -y
npm install express body-parser
npm install typescript ts-node @types/node @types/express --save-dev
```

**Módulo 2: Estrutura do Projeto**
Organize seu projeto em pastas separadas para `models`, `controllers`, `routes`, e `utils`. Aqui está um exemplo de como sua estrutura de diretórios pode parecer:

```
/projeto-banco
  /src
    /controllers
    /models
    /routes
    /utils
  /dist
  tsconfig.json
  package.json
```

**Módulo 3: Modelagem de Dados**
Dentro da pasta `models`, você vai definir as estruturas de dados que representam as contas bancárias e as transações. Por exemplo:

```typescript
// src/models/ContaBancaria.ts
export interface ContaBancaria {
  id: number;
  saldo: number;
}

// src/models/Transacao.ts
export interface Transacao {
  id: number;
  contaId: number;
  valor: number;
  data: Date;
}
```

**Módulo 4: Controladores**
Os controladores serão responsáveis por lidar com a lógica de negócios. Por exemplo, o controlador de contas bancárias pode ter métodos para criar uma nova conta, depositar, sacar e transferir dinheiro.

```typescript
// src/controllers/ContaBancariaController.ts
import { ContaBancaria } from '../models/ContaBancaria';

export class ContaBancariaController {
  // Métodos para criar conta, depositar, etc.
}
```

**Módulo 5: Rotas**
As rotas vão definir os endpoints da sua API REST e conectarão as requisições HTTP aos controladores apropriados.

```typescript
// src/routes/bancoRoutes.ts
import { Router } from 'express';
import { ContaBancariaController } from '../controllers/ContaBancariaController';

const router = Router();
const controller = new ContaBancariaController();

// Definir rotas para criar conta, depositar, etc.

export default router;
```

**Módulo 6: Servidor e Inicialização**
Finalmente, você vai configurar o servidor Express para usar suas rotas e iniciar o servidor.

```typescript
// src/index.ts
import express from 'express';
import bancoRoutes from './routes/bancoRoutes';

const app = express();
app.use(express.json());
app.use('/api/banco', bancoRoutes);

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Servidor rodando na porta ${PORT}`);
});
```

**Módulo 7: Compilação e Execução**
Não se esqueça de configurar o `tsconfig.json` para compilar seu TypeScript para JavaScript. Depois, você pode executar seu projeto com `ts-node` ou compilar e executar o JavaScript gerado.

```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "./dist",
    "strict": true,
    "esModuleInterop": true
  }
}
```

```bash
npx ts-node src/index.ts
```

Esses são os passos básicos para criar uma aplicação bancária simples com TypeScript e Node.js. Lembre-se de adicionar tratamento de erros, validação de dados e segurança conforme necessário para sua aplicação.
