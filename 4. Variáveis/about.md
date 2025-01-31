# Ordem de Prioridade e Boas Práticas com Variáveis no Sass

## 📌 Por que a Ordem de Importação Importa?

O Sass processa os arquivos **na ordem em que são importados**, seguindo um fluxo "top-down". Isso significa que:
- Variáveis devem ser declaradas **antes** de serem utilizadas em outros arquivos.
- A redefinição de variáveis **substitui** o valor anterior (a última definição prevalece).

---

## 🛠️ Estruturação de Variáveis

### 1. **Variáveis Centralizadas**
Defina variáveis em um arquivo dedicado (ex: `_variaveis.scss`) para facilitar a manutenção:
```scss
// _variaveis.scss
$cor-primaria: #3498db;
$fonte-principal: 'Arial', sans-serif;
```

### 2. **Uso em Múltiplos Arquivos**
Importe o arquivo de variáveis primeiro para garantir disponibilidade:
```scss
// main.scss
@import 'variaveis'; // 📌 Deve vir primeiro!
@import 'botoes';
@import 'cabecalho';
```

---

## ⚠️ Exemplo de Conflito por Ordem Incorreta

**Cenário Problemático**:
```scss
// main.scss (ORDEM ERRADA!)
@import 'botoes'; // ❌ Usa $cor-primaria antes de ser definida
@import 'variaveis';
```

**Resultado**:
```scss
// botoes.scss
.botao {
  background-color: $cor-primaria; // Erro: variável não definida!
}
```

---

## 🎯 Regra de Precedência de Variáveis

A **última declaração** de uma variável sobrescreve as anteriores:
```scss
// _variaveis.scss
$cor-primaria: blue;

// _tema.scss
$cor-primaria: red; // 🔄 Esta será a cor efetiva

// main.scss
@import 'variaveis';
@import 'tema'; // A última definição prevalece
```

---

## ✅ Boas Práticas

1. **Organização de Arquivos**:
   ```
   styles/
   ├── _variaveis.scss
   ├── _mixins.scss
   ├── _botoes.scss
   └── main.scss
   ```

2. **Importação em Ordem**:
   ```scss
   // main.scss
   @import 'variaveis';
   @import 'mixins';
   @import 'botoes';
   @import 'cabecalho';
   ```

3. **Evite Redefinições**:
   ```scss
   // _variaveis.scss
   $cor-primaria: blue !default; // Permite sobrescrita controlada
   ```

---

## 📝 Resumo dos Pontos-Chave

- **Variáveis primeiro**: Garanta que arquivos com variáveis sejam importados no início.
- **Precedência**: A última declaração de variável prevalece.
- **Estrutura clara**: Separe variáveis, mixins e componentes em arquivos distintos.
- **!default**: Use para temas personalizáveis (ex: bibliotecas).
