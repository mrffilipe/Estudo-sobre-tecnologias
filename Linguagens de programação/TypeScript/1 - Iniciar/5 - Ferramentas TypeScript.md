
# Ferramentas do TypeScript em 5 Minutos

## Introdução

TypeScript é uma linguagem de programação poderosa que se integra bem com várias ferramentas de desenvolvimento, facilitando a criação, compilação e depuração de projetos.

## Primeiros Passos

1. **Instalação do TypeScript**
   ```bash
   npm install -g typescript
   ```
   Este comando instala o compilador TypeScript globalmente.

2. **Configuração do Projeto**
   - Crie um novo projeto e inicialize o npm:
     ```bash
     mkdir my-project
     cd my-project
     npm init -y
     ```

3. **Instalação de Dependências**
   - Adicione TypeScript e ts-node como dependências de desenvolvimento:
     ```bash
     npm install typescript ts-node --save-dev
     ```

## Arquivo `tsconfig.json`

O arquivo `tsconfig.json` configura o compilador TypeScript para o seu projeto. Crie um arquivo `tsconfig.json` com o seguinte conteúdo:

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "outDir": "./dist"
  },
  "include": ["src/**/*"]
}
```

## Estrutura do Projeto

Organize seu projeto com uma pasta `src` para o código fonte TypeScript e uma pasta `dist` para os arquivos compilados.

```
my-project/
├── src/
│   └── index.ts
├── dist/
├── package.json
└── tsconfig.json
```

## Scripts de Build e Execução

Adicione scripts no `package.json` para compilar e executar o projeto:

```json
"scripts": {
  "build": "tsc",
  "start": "ts-node src/index.ts"
}
```

- **Build**: Compila os arquivos TypeScript.
  ```bash
  npm run build
  ```

- **Start**: Executa o arquivo `index.ts` usando `ts-node`.
  ```bash
  npm start
  ```

## Debugging com VS Code

O Visual Studio Code oferece excelente suporte para TypeScript, incluindo funcionalidades de depuração.

1. **Instalação da Extensão TypeScript**
   - Certifique-se de ter a extensão TypeScript instalada no VS Code.

2. **Configuração do Debugger**
   - Crie uma configuração de depuração em `.vscode/launch.json`:
     ```json
     {
       "version": "0.2.0",
       "configurations": [
         {
           "type": "node",
           "request": "launch",
           "name": "Launch Program",
           "skipFiles": ["<node_internals>/**"],
           "program": "${workspaceFolder}/src/index.ts"
         }
       ]
     }
     ```

3. **Uso do Debugger**
   - Coloque breakpoints no código TypeScript e inicie a depuração pelo VS Code.

## ESLint para TypeScript

Utilize o ESLint para garantir a qualidade do código. Instale as dependências necessárias:

```bash
npm install eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin --save-dev
```

Configure o ESLint criando um arquivo `.eslintrc.json`:

```json
{
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint"],
  "extends": ["eslint:recommended", "plugin:@typescript-eslint/recommended"],
  "rules": {
    // Adicione regras específicas aqui
  }
}
```

## Boas Práticas

- **Organização de Projeto**: Mantenha a estrutura do projeto organizada com pastas separadas para código fonte e arquivos compilados.
- **Scripts Automatizados**: Utilize scripts npm para automatizar tarefas comuns como compilação e execução.
- **Depuração Eficiente**: Aproveite o suporte de depuração do VS Code para encontrar e corrigir erros rapidamente.
- **Linting**: Use ferramentas como ESLint para manter a qualidade e consistência do código.
