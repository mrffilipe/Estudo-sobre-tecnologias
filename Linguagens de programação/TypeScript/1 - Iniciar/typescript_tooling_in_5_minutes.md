
# Ferramentas TypeScript em 5 Minutos

TypeScript oferece várias ferramentas que ajudam a melhorar o fluxo de trabalho e a produtividade. Este guia rápido mostra como configurar e usar algumas dessas ferramentas essenciais.

## Configuração do Ambiente

1. **Instalando TypeScript**
   - Instale TypeScript globalmente usando npm.
   ```sh
   npm install -g typescript
   ```

2. **Verificando a Instalação**
   - Verifique se a instalação foi bem-sucedida.
   ```sh
   tsc --version
   ```

## Configurando o Projeto

1. **Criando `tsconfig.json`**
   - O arquivo `tsconfig.json` contém as configurações do compilador TypeScript.
   ```sh
   tsc --init
   ```
   - Este comando cria um arquivo `tsconfig.json` com configurações padrão.

2. **Exemplo de `tsconfig.json`**
   - Um exemplo de configuração básica:
   ```json
   {
     "compilerOptions": {
       "target": "es5",
       "module": "commonjs",
       "strict": true,
       "esModuleInterop": true
     },
     "include": ["src"],
     "exclude": ["node_modules"]
   }
   ```

## Integração com Editores

1. **Visual Studio Code**
   - VS Code tem excelente suporte para TypeScript.
   - Instale a extensão oficial do TypeScript para melhor integração.
   ```sh
   code --install-extension ms-vscode.vscode-typescript-tslint-plugin
   ```

2. **WebStorm**
   - WebStorm também oferece suporte nativo para TypeScript.
   - Configure o compilador TypeScript nas configurações do projeto.

## Compilação Automática

1. **Watch Mode**
   - Use o modo watch para compilar automaticamente o código TypeScript quando houver mudanças.
   ```sh
   tsc --watch
   ```

## Linting com TSLint

1. **Instalando TSLint**
   - Instale o TSLint como uma dependência de desenvolvimento.
   ```sh
   npm install tslint --save-dev
   ```

2. **Configurando TSLint**
   - Crie um arquivo `tslint.json` com as regras de linting.
   ```json
   {
     "defaultSeverity": "error",
     "extends": ["tslint:recommended"],
     "jsRules": {},
     "rules": {
       "quotemark": [true, "double"],
       "semicolon": [true, "always"]
     },
     "rulesDirectory": []
   }
   ```

3. **Executando TSLint**
   - Verifique o código TypeScript com TSLint.
   ```sh
   npx tslint -p tsconfig.json
   ```

## Testes com Jest

1. **Instalando Jest**
   - Instale Jest e os tipos necessários para TypeScript.
   ```sh
   npm install jest ts-jest @types/jest --save-dev
   ```

2. **Configurando Jest**
   - Crie um arquivo de configuração `jest.config.js`.
   ```javascript
   module.exports = {
     preset: 'ts-jest',
     testEnvironment: 'node',
     testMatch: ['**/?(*.)+(spec|test).ts?(x)']
   };
   ```

3. **Escrevendo um Teste**
   - Crie um arquivo de teste, por exemplo, `sum.test.ts`.
   ```typescript
   import { sum } from "./sum";

   test('adds 1 + 2 to equal 3', () => {
     expect(sum(1, 2)).toBe(3);
   });
   ```

4. **Executando os Testes**
   - Execute os testes com Jest.
   ```sh
   npx jest
   ```

## Integração Contínua

1. **Configurando CI com GitHub Actions**
   - Crie um arquivo de workflow `.github/workflows/ci.yml`.
   ```yaml
   name: CI

   on:
     push:
       branches: [ main ]
     pull_request:
       branches: [ main ]

   jobs:
     build:
       runs-on: ubuntu-latest

       steps:
       - uses: actions/checkout@v2
       - name: Set up Node.js
         uses: actions/setup-node@v2
         with:
           node-version: '14'
       - run: npm install
       - run: npm run build
       - run: npm test
   ```

## Dicas de Boas Práticas

1. **Configure um Ambiente de Desenvolvimento Consistente**: Use `tsconfig.json` e `tslint.json` para padronizar a configuração.
2. **Automatize Tarefas com Scripts npm**: Defina scripts no `package.json` para automatizar tarefas comuns.
3. **Use Ferramentas de CI/CD**: Implemente integração contínua para garantir a qualidade do código.
4. **Aproveite o Suporte do Editor**: Use editores com bom suporte para TypeScript para melhorar a produtividade.
