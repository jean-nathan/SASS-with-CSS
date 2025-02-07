# Cenários de Uso em Projetos Reais

## 1. `@for` - Quando Usar:
### a) **Sistemas de Grid**
```scss
// Gerar colunas responsivas
@for $i from 1 through 12 {
  .col-#{$i} {
    width: percentage(math.div($i, 12));
  }
}
```
**Aplicação:** Layouts de e-commerce, cards de produtos, formulários complexos

---

### b) **Escala de Espaçamentos**
```scss
// Gerar margens/paddings múltiplos de 8px
@for $i from 1 through 8 {
  .mt-#{$i*8} {
    margin-top: #{$i*8}px;
  }
}
```
**Aplicação:** Sistemas de design com medidas base (8-point grid), apps mobile

---

### c) **Animações Progressivas**
```scss
// Criar keyframes sequenciais
@for $i from 1 through 10 {
  @keyframes slide-#{$i} {
    #{percentage(math.div($i, 10))} {
      transform: translateX(#{$i * 10}px);
    }
  }
}
```
**Aplicação:** Sequências animadas, efeitos de carregamento

---

## 2. `@each` - Quando Usar:
### a) **Temas de Cores**
```scss
$temas: (
  "dark": #2c3e50,
  "light": #ecf0f1,
  "danger": #e74c3c
);

@each $nome, $cor in $temas {
  .btn-#{$nome} {
    background: $cor;
    border: 2px solid darken($cor, 10%);
  }
}
```
**Aplicação:** Sistemas multi-tenancy, dark mode

---

### b) **Ícones de Redes Sociais**
```scss
$redes: (
  "facebook": "#3b5998",
  "linkedin": "#0077b5",
  "whatsapp": "#25d366"
);

@each $rede, $cor in $redes {
  .icone-#{$rede} {
    background-image: url('/icons/#{$rede}.svg');
    &:hover {
      background-color: #{$cor};
    }
  }
}
```
**Aplicação:** Footers, páginas de contato, compartilhamento de conteúdo

---

### c) **Componentes com Estados**
```scss
$estados: ("success", "error", "warning");

@each $estado in $estados {
  .alert-#{$estado} {
    border-left: 5px solid var(--cor-#{$estado});
    animation: pulse-#{$estado} 2s infinite;
  }
}
```
**Aplicação:** Sistemas de notificação, formulários de validação

---

## 3. `@while` - Quando Usar (Cuidadosamente!):
### a) **Geração Adaptativa**
```scss
$tamanho-fonte: 12;
$nivel: 1;

@while $tamanho-fonte <= 72 {
  .titulo-nivel-#{$nivel} {
    font-size: #{$tamanho-fonte}px;
    line-height: $tamanho-fonte * 1.5;
  }
  $tamanho-fonte: $tamanho-fonte * 1.618; // Razão áurea
  $nivel: $nivel + 1;
}
```
**Aplicação:** Escala tipográfica não-linear, sistemas de design orgânicos

---

### b) **Layouts Dinâmicos**
```scss
$colunas: 1;
$largura-container: 1200px;

@while $colunas <= 5 {
  .layout-#{$colunas}col {
    width: $largura-container;
    grid-template-columns: repeat($colunas, 1fr);
    $largura-container: $largura-container - 200px;
    $colunas: $colunas + 1;
  }
}
```
**Aplicação:** Dashboards adaptativos, sistemas de relatórios

---

## Combinações Poderosas:

### 1. **Grid Responsivo com Breakpoints**
```scss
$breakpoints: ("sm": 576px, "md": 768px, "lg": 992px);

@each $nome, $tamanho in $breakpoints {
  @media (min-width: $tamanho) {
    @for $i from 1 through 12 {
      .col-#{$nome}-#{$i} {
        width: percentage(math.div($i, 12));
      }
    }
  }
}
```

---

### 2. **Temas + Componentes**
```scss
$componentes: (
  "botao": ("padding", "border-radius"),
  "card": ("box-shadow", "background")
);

@each $componente, $propriedades in $componentes {
  @each $prop in $propriedades {
    .#{$componente}-#{$prop} {
      #{$prop}: var(--#{$componente}-#{$prop});
    }
  }
}
```

---

## Quando **NÃO** Usar Loops:
1. **Classes Únicas:** Se vai usar apenas 1-2 instâncias
2. **Código Crítico:** Em elementos que exigem otimização extrema
3. **Projetos Pequenos:** Onde a complexidade não compensa
4. **Estilos Customizados:** Que precisam de ajustes manuais

---

## Fluxograma de Decisão:
```
Preciso gerar múltiplas variações? 
          │
          ├── Sim → Padrão numérico? → @for
          │
          ├── Sim → Lista de valores? → @each
          │
          └── Sim → Condição complexa? → @while
```

Dica final: **Sempre verifique o CSS gerado** para evitar "code bloat" (CSS desnecessariamente grande)!
