# Instalação do SASS

## **1. Baixar e Instalar o Node.js**
Para utilizar o SASS via Node.js, é necessário ter o Node.js instalado na sua máquina. 

- Baixe o instalador do Node.js no site oficial:  
  [https://nodejs.org/](https://nodejs.org/)
- Instale o Node.js e verifique se foi instalado corretamente executando no terminal:
  ```bash
  node -v
  ```
  Se retornar a versão do Node.js, a instalação foi concluída com sucesso.

## **2. Criar o arquivo `package.json`**
No diretório do seu projeto, execute o seguinte comando para criar um `package.json`:

```bash
npm init -y
```
Isso irá gerar um arquivo `package.json` com configurações padrão.

## **3. Instalar o SASS**
Agora, instale o SASS como dependência de desenvolvimento:

```bash
npm install sass --save-dev
```

Isso irá adicionar o `sass` no diretório `node_modules` e atualizar o `package.json`.

## **4. Adicionar um Script para Compilar o SASS**
Abra o arquivo `package.json` e adicione o seguinte trecho dentro de `"scripts"`:

```json
"scripts": {
  "sass:g": "node_modules/sass/sass.js",
  "sass": "sass src/styles/style.scss dist/style.css",
  "sass:watch": "sass --watch src/styles/style.scss:dist/style.css"
}
```

## **5. Executar o SASS**
Agora você pode rodar o seguinte comando para compilar o SASS automaticamente:

```bash
npm run sass
```

Se desejar assistir as alterações em tempo real, use:
```bash
npm run sass:watch
```
