# Funções no Sass

## Funções Nativas do Sass

### 1. Man# Funções no Sass

## Funções Nativas do Sass

### 1. Manipulação de Cores
O Sass oferece funções poderosas para trabalhar com cores:

#### `lighten()` e `darken()`
**Propósito:** Alterar a luminosidade de uma cor

```scss
$cor-primaria: blue;

a {
  background: $cor-primaria;
  
  &:hover {
    background: lighten($cor-primaria, 20%); // Clareia 20%
    // OU
    background: darken($cor-primaria, 20%);  // Escurece 20%
  }
}
```

**Funcionamento:**
- Valores de 0% a 100%
- Altera no espaço de cor HSL
- Mantém o matiz original

#### `transparentize()`
**Propósito:** Controlar a opacidade da cor

```scss
@use "sass:color"; // Requer importação do módulo

a:hover {
  background: color.transparentize($cor-primaria, 0.5); // 50% transparente
}
```

**Parâmetros:**
1. Cor original
2. Valor de transparência (0 = totalmente opaco, 1 = totalmente transparente)

---

### 2. Funções Matemáticas
Principais funções úteis:
- `percentage()` - Converte para porcentagem
- `round()` - Arredonda números
- `min()` e `max()` - Valores extremos
- `random()` - Número aleatório

---

## Criando Funções Personalizadas

### 1. Conversão para `em`
**Objetivo:** Converter pixels para unidades relativas

```scss
@function em($pixels, $context: 10) {
  @return ($pixels / $context) * 1em;
}

// Uso:
li {
  font-size: em(24); // 24px → 2.4em (24/10)
  margin: em(15);    // 15px → 1.5em
}
```

**Vantagens:**
- Layouts responsivos
- Base ajustável (padrão 10px)
- Cálculos automáticos

---

### 2. Sistema de Grid
**Objetivo:** Criar sistema de colunas flexível

```scss
@function grid($colunas, $total: 16) {
  @return round(($colunas / $total) * 100%);
}

// Uso:
div {
  width: grid(6); // (6/16)*100 = 37.5%
}

section {
  width: grid(12, 12); // (12/12)*100 = 100%
}
```

**Características:**
- Total de colunas customizável
- Arredondamento automático
- Cálculo proporcional

---

## Boas Práticas com Funções

1. **Nomes claros:** Use verbos ou descrições precisas
2. **Parâmetros padrão:** Defina valores padrão úteis
3. **Unidade consistente:** Mantenha uma base de cálculo
4. **Validação:** Adicione checagens de erros (opcional)

```scss
@function em($pixels, $context: 10) {
  @if unit($context) != 'px' {
    @error "Contexto deve ser em pixels";
  }
  @return ($pixels / $context) * 1em;
}
```

---

## Fluxo de Trabalho Recomendado

1. Identifique padrões repetitivos
2. Crie funções para cálculos complexos
3. Use funções nativas sempre que possível
4. Teste com diferentes valores de entrada
5. Documente parâmetros e retorno

**Exemplo de Aplicação Real:**
```scss
@function contrast-color($bg-color) {
  @if (lightness($bg-color) > 50%) {
    @return black;
  } @else {
    @return white;
  }
}

.button {
  background: $cor-primaria;
  color: contrast-color($cor-primaria);
}
ipulação de Cores
O Sass oferece funções poderosas para trabalhar com cores:

#### `lighten()` e `darken()`
**Propósito:** Alterar a luminosidade de uma cor

```scss
$cor-primaria: blue;

a {
  background: $cor-primaria;
  
  &:hover {
    background: lighten($cor-primaria, 20%); // Clareia 20%
    // OU
    background: darken($cor-primaria, 20%);  // Escurece 20%
  }
}
```

**Funcionamento:**
- Valores de 0% a 100%
- Altera no espaço de cor HSL
- Mantém o matiz original

#### `transparentize()`
**Propósito:** Controlar a opacidade da cor

```scss
@use "sass:color"; // Requer importação do módulo

a:hover {
  background: color.transparentize($cor-primaria, 0.5); // 50% transparente
}
```

**Parâmetros:**
1. Cor original
2. Valor de transparência (0 = totalmente opaco, 1 = totalmente transparente)

---

### 2. Funções Matemáticas
Principais funções úteis:
- `percentage()` - Converte para porcentagem
- `round()` - Arredonda números
- `min()` e `max()` - Valores extremos
- `random()` - Número aleatório

---

## Criando Funções Personalizadas

### 1. Conversão para `em`
**Objetivo:** Converter pixels para unidades relativas

```scss
@function em($pixels, $context: 10) {
  @return ($pixels / $context) * 1em;
}

// Uso:
li {
  font-size: em(24); // 24px → 2.4em (24/10)
  margin: em(15);    // 15px → 1.5em
}
```

**Vantagens:**
- Layouts responsivos
- Base ajustável (padrão 10px)
- Cálculos automáticos

---

### 2. Sistema de Grid
**Objetivo:** Criar sistema de colunas flexível

```scss
@function grid($colunas, $total: 16) {
  @return round(($colunas / $total) * 100%);
}

// Uso:
div {
  width: grid(6); // (6/16)*100 = 37.5%
}

section {
  width: grid(12, 12); // (12/12)*100 = 100%
}
```

**Características:**
- Total de colunas customizável
- Arredondamento automático
- Cálculo proporcional

---

## Boas Práticas com Funções

1. **Nomes claros:** Use verbos ou descrições precisas
2. **Parâmetros padrão:** Defina valores padrão úteis
3. **Unidade consistente:** Mantenha uma base de cálculo
4. **Validação:** Adicione checagens de erros (opcional)

```scss
@function em($pixels, $context: 10) {
  @if unit($context) != 'px' {
    @error "Contexto deve ser em pixels";
  }
  @return ($pixels / $context) * 1em;
}
```

---

## Fluxo de Trabalho Recomendado

1. Identifique padrões repetitivos
2. Crie funções para cálculos complexos
3. Use funções nativas sempre que possível
4. Teste com diferentes valores de entrada
5. Documente parâmetros e retorno

**Exemplo de Aplicação Real:**
```scss
@function contrast-color($bg-color) {
  @if (lightness($bg-color) > 50%) {
    @return black;
  } @else {
    @return white;
  }
}

.button {
  background: $cor-primaria;
  color: contrast-color($cor-primaria);
}
