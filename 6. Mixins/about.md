# Mixins no Sass: Guia Prático para Reutilização de Código

Aprenda a criar e usar mixins de forma eficiente para tornar seu código mais organizado e reaproveitável.

---

## 📌 O Básico dos Mixins

### Para que servem?
- **Reutilizar blocos de código** em vários lugares
- **Evitar repetição** de propriedades CSS
- **Organizar** estilos complexos

### Como criar e usar:
```scss
// 1. Criação do mixin
@mixin title-large {
  font-size: 4em;
  font-weight: bold;
  font-family: monospace;
  line-height: 1;
}

// 2. Uso do mixin
h1 {
  @include title-large; // Aplica todas as propriedades do mixin
  color: blue;
}
```

---

## 🛠️ Casos de Uso Comuns

### 1. Prefixos de navegadores
```scss
@mixin border-box {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}

// Uso:
section {
  @include border-box;
  max-width: 600px;
}
```

### 2. Mixins dentro de Mixins (Composição)
```scss
@mixin base-style {
  background-color: aquamarine;
  color: #fff;
}

@mixin special-title {
  @include base-style; // Herda propriedades de outro mixin
  font-size: 3rem;
  text-transform: uppercase;
}
```

---

## 🎯 Trabalhando com Argumentos

### Mixins parametrizáveis:
```scss
// Mixin com parâmetro obrigatório
@mixin separador($cor) {
  &::after {
    content: '';
    display: block;
    width: 100px;
    height: 4px;
    background: $cor;
  }
}

// Uso:
h2 {
  @include separador(#84E); // Passa a cor desejada
}
```

### Valores padrão (default):
```scss
@mixin separador($cor: blue, $largura: 100px) {
  // Se não informar valores, usa blue e 100px
  width: $largura;
  background: $cor;
}

// Uso sem parâmetros:
h3 {
  @include separador; // Usa valores padrão
}
```

---

## 💡 Dicas Avançadas

### 1. Múltiplos valores (Argumentos variáveis)
```scss
@mixin sombras($shadows...) {
  box-shadow: $shadows;
  -webkit-box-shadow: $shadows;
}

// Uso com várias sombras:
.card {
  @include sombras(
    0 2px 4px rgba(0,0,0,0.1),
    0 4px 8px rgba(0,0,0,0.1)
  );
}
```

### 2. Blocos de conteúdo (@content)
```scss
// Mixin para responsividade
@mixin mobile {
  @media (max-width: 600px) {
    @content; // Injeta o bloco de estilo aqui
  }
}

// Uso:
.menu {
  font-size: 1.2rem;

  @include mobile {
    font-size: 1rem; // Só aplica no mobile
    padding: 10px;
  }
}
```

---

## ✅ Melhores Práticas

1. **Nomeie mixins de forma descritiva**  
   `@mixin centralizar-flex` em vez de `@mixin cf`

2. **Use argumentos para variações**  
   Transforme valores fixos em parâmetros flexíveis

3. **Mantenha os mixins focados**  
   Cada mixin deve ter uma única responsabilidade

4. **Documente com comentários**  
   Explique o que o mixin faz e seus parâmetros

---

## 📝 Exemplo Completo
```scss
@mixin card-estilizado($cor: #fff, $raio: 8px) {
  background: $cor;
  border-radius: $raio;
  padding: 20px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  
  @include mobile {
    padding: 10px;
    border-radius: $raio/2;
  }
}

// Uso:
.article-card {
  @include card-estilizado(#f8f8f8, 12px);
}

---

✨ **Lembre-se:** Mixins são como receitas - quanto melhor organizados, mais fácil será manter seu código!
