# Condicionais no Sass: Guia Completo

## 1. Controle Temático com Condicionais
**Objetivo:** Alterar variáveis globais baseado em diferentes temas

```scss
$theme: desert; // Variável controladora
$primary-color: black; // Valor padrão
$secondary-color: gray; // Valor padrão

// Lógica de seleção de tema
@if $theme == ocean {
  $primary-color: blue;
  $secondary-color: orange;
} @else if $theme == desert {
  $primary-color: yellow;
  $secondary-color: purple;
} @else {
  // Mantém valores padrão se nenhum tema for encontrado
}
```

**Funcionamento:**
1. Verifica o valor de `$theme`
2. Atualiza as cores conforme o tema selecionado
3. Se nenhum condicional for atendido, mantém os valores iniciais

---

## 2. Mixins com Validação usando `map.get`

### 2.1 O que é `map.get`?
- **Função nativa do Sass** para acessar valores em mapas
- Sintaxe: `map.get($map, $key)`
- Retorna `null` se a chave não existir

### 2.2 Implementação com Validação
```scss
@mixin type-primary($size) {
  // Mapa de valores permitidos
  $sizes: (
    16: 1rem,  // 16px → 1rem
    32: 2rem,  // 32px → 2rem
    48: 3rem,  // 48px → 3rem
  );

  // Busca o valor no mapa
  $size-value: map.get($sizes, $size);
  
  // Validação do resultado
  @if $size-value != null {
    font-size: $size-value;
  } @else {
    @warn "⚠️ Tamanho inválido: '#{$size}'. Use: 16, 32 ou 48";
  }
}
```

**Passo a Passo:**
1. Cria mapa de valores aceitáveis
2. Busca o valor correspondente à chave
3. Verifica se o valor existe:
   - **Existe:** aplica o estilo
   - **Não existe:** emite alerta

**Exemplo de Uso:**
```scss
.texto-grande {
  @include type-primary(48); // Aplica 3rem
}

.texto-invalido {
  @include type-primary(24); // Emite warning
}
```

---

## 3. Breakpoints Responsivos com Condicionais

### 3.1 Mixin de Media Queries
```scss
@mixin responsive($device) {
  // Definição dos breakpoints
  @if $device == m { // Mobile
    @media (max-width: 400px) { @content; }
  } @else if $device == t { // Tablet
    @media (max-width: 600px) { @content; }
  } @else if $device == s { // Small Screens
    @media (max-width: 900px) { @content; }
  }
}
```

### 3.2 Uso Avançado com Aninhamento
```scss
.modal {
  padding: 2rem;
  
  @include responsive(s) {
    padding: 1rem;
    @include type-primary(32);
  }
}
```

**Resultado CSS:**
```css
.modal { padding: 2rem; }

@media (max-width: 900px) {
  .modal {
    padding: 1rem;
    font-size: 2rem;
  }
}
```

---

## 4. Operações Comparativas Avançadas

### 4.1 Comparando Valores
```scss
$padding-base: 20px;

.elemento {
  @if (40px > $padding-base) {
    // Se 40 for maior que 20
    padding: 40px - $padding-base; // 20px
  } @else {
    padding: $padding-base;
  }
}
```

### 4.2 Operadores Disponíveis
| Operador | Descrição           | Exemplo         |
|----------|---------------------|-----------------|
| `==`     | Igualdade           | `10 == 10` ✅   |
| `!=`     | Diferença           | `10 != 5` ✅    |
| `>`      | Maior que           | `15 > 10` ✅    |
| `<`      | Menor que           | `5 < 10` ✅     |
| `>=`     | Maior ou igual      | `10 >= 10` ✅   |
| `<=`     | Menor ou igual      | `5 <= 10` ✅    |

---

## 5. Boas Práticas com `map.get`

### 5.1 Por que usar mapas?
- Centraliza valores permitidos
- Facilita manutenção
- Reduz repetição de código

### 5.2 Exemplo Expandido
```scss
$config: (
  colors: (
    primary: blue,
    secondary: green
  ),
  sizes: (
    small: 8px,
    medium: 16px,
    large: 24px
  )
);

@function get-config($key, $subkey) {
  @return map.get(map.get($config, $key), $subkey);
}

// Uso:
.elemento {
  color: get-config(colors, primary);
  padding: get-config(sizes, medium);
}
```

### 5.3 Tratamento de Erros
```scss
@mixin cor-tema($tipo) {
  $cor: map.get($cores-tema, $tipo);
  
  @if $cor {
    background-color: $cor;
  } @else {
    @error "Cor '#{$tipo}' não existe no mapa!";
  }
}
```

**Diferenças:**
- `@warn`: Alerta mas compila
- `@error`: Para compilação e exibe mensagem

---

## 6. Fluxo de Trabalho Recomendado

1. **Defina mapas** para valores reutilizáveis
2. **Use `map.get`** para acessar valores
3. **Valide sempre** com condicionais
4. **Implemente fallbacks** para valores ausentes
5. **Use `@debug`** para inspecionar valores
6. **Documente** mapas e funções

**Exemplo de Debugging:**
```scss
@mixin exemplo {
  $valores: (inicio: 0, fim: 100);
  @debug map.get($valores, meio); // Output: DEBUG: null
}
```
