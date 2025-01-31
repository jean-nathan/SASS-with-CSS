# Uso de Variáveis no Sass e Regras de Prioridade

## 📌 Introdução
As variáveis no Sass são um recurso poderoso que permite reutilizar valores, facilitar manutenção e garantir consistência no design. No entanto, é essencial entender a ordem de prioridade das variáveis e como organizá-las corretamente para evitar conflitos e problemas no código.

---

## 🎨 Vantagens do Uso de Variáveis no Sass

1. **Facilidade de manutenção** – Em vez de modificar uma cor ou espaçamento em vários lugares do código, você pode alterar apenas o valor da variável.
2. **Maior consistência** – Mantém um padrão visual no projeto, garantindo que todas as instâncias de uma cor, espaçamento ou fonte sejam uniformes.
3. **Reutilização eficiente** – Permite o reaproveitamento de valores em diferentes partes do código, evitando repetição.

### Exemplo de Uso de Variáveis:
```scss
// Definição das variáveis
$primary-color: #3498db;
$secondary-color: #2ecc71;
$font-size: 16px;

// Aplicação das variáveis no CSS
body {
  background-color: $primary-color;
  color: $secondary-color;
  font-size: $font-size;
}
```

---

## 📌 Ordem de Prioridade e Organização

### 1️⃣ Ordem Correta dos Arquivos Importados
Quando se utiliza **múltiplos arquivos no Sass**, é importante organizar os imports corretamente para evitar erros. Por exemplo, se um arquivo depende de variáveis definidas em outro, ele deve ser importado **depois** do arquivo que contém as variáveis.

✅ **Boa prática:**
```scss
@use 'variables';  // Primeiro, importar as variáveis
@use 'mixins';     // Depois, importar mixins que podem usar as variáveis
@use 'base';       // Por fim, importar os estilos base
```

❌ **Má prática (pode resultar em erro de variável indefinida):**
```scss
@use 'base';       // Erro: o arquivo base pode tentar usar variáveis não definidas ainda
@use 'variables';  
```


### 2️⃣ Sobrescrita de Variáveis
O Sass segue uma lógica de **cascata**, ou seja, se uma variável for redefinida posteriormente, ela substituirá o valor anterior. Isso significa que a ordem em que as variáveis são declaradas impacta diretamente no estilo final.

```scss
$primary-color: #3498db;  // Primeiro valor
$primary-color: #ff5733;  // Sobrescrevendo a variável

body {
  background-color: $primary-color;  // Resultado: #ff5733
}
```

### 3️⃣ Uso de `!default` para Configuração Padrão
Se quiser definir valores padrão que podem ser sobrescritos posteriormente, use `!default`. Isso permite que a variável seja alterada apenas se ainda não tiver um valor atribuído.

```scss
$primary-color: #3498db !default;  // Será usada apenas se nenhuma outra definição existir
```

---

## 🎯 Conclusão
- Sempre defina as variáveis antes de usá-las.
- O **arquivo de variáveis** deve ser importado **antes de qualquer outro** que dependa dele.
- A ordem de declaração das variáveis influencia a sobrescrita de valores.
- Use `!default` quando quiser permitir a redefinição posterior de uma variável.
