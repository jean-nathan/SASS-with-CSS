# Loops em SASS: `@for`, `@while` e `@each`

## 1. Uso do `@for`

### Exemplo 1: Geração de classes com largura progressiva
```scss
// Configurações iniciais do loop
@for $i from 1 through 6 { // `through` inclui o número final (1 a 6)
  .item-#{$i} {
    width: 200px * $i; // Largura escala de forma linear
  }
}
```
**Resultado CSS:**
```css
.item-1 { width: 200px; }
.item-2 { width: 400px; }
/* ... até .item-6 { width: 1200px; } */
```

**Pontos importantes:**
- `through` vs `to`: `1 through 6` executa 6 vezes, `1 to 6` executaria 5 vezes
- Interpolação de variáveis: `#{$i}` para gerar classes dinâmicas

---

### Exemplo 2: Sistema de Grid (pixels)
```scss
// Variáveis do sistema de grid
$container: 960; // Sem unidade para cálculos matemáticos
$gutter: 20;     // Espaçamento entre colunas
$colunas: 12;    // Número total de colunas

@for $i from 1 through $colunas {
  // Cálculo da largura: (container / total colunas) * colunas usadas - gutter
  $width: ($container / $colunas * $i) - $gutter;
  
  .grid-#{$i} {
    width: $width + px; // Adiciona unidade no final
  }
}
```

**Melhores práticas:**
1. Manter valores numéricos sem unidade para cálculos
2. Adicionar unidades apenas no resultado final
3. Nomes claros para variáveis de configuração

---

## 2. Criação de Valores em Porcentagem

### Exemplo 1: Divisão Simples
```scss
@for $i from 1 through 12 {
  $width: percentage(1/$i); // Converte fração em porcentagem
  .porcento-#{$i} {
    width: $width;
  }
}
```
**Resultado parcial:**
```css
.porcento-1 { width: 100%; }
.porcento-2 { width: 50%; }
.porcento-3 { width: 33.33333%; }
/* ... */
```

---

### Exemplo 2: Grid com Porcentagem (Usando math.div)
```scss
@use "sass:math"; // Import obrigatório para usar math.div

@for $i from 1 through 16 {
  // Uso de math.div para divisão explícita (melhor prática)
  $width: math.div($i, 16) * 100 + "%";
  
  .porcento-#{$i} {
    width: $width;
  }
}
```

**Por que usar math.div?**
- Evita problemas com o operador `/` que pode ser depreciado
- Deixa a intenção do código mais clara
- Melhora a manutenibilidade

---

## 3. Uso do `@while`

```scss
$i: 1; // Variável de controle externa

@while $i <= 6 {
  .type-#{$i} {
    font-size: (16 * $i) + px; // Tamanho de fonte escalável
  }
  $i: $i + 1; // Incremento manual obrigatório
}
```

**Quando usar:**
- Loops complexos com condições não lineares
- Quando o número de iterações não é conhecido antecipadamente

**Cuidados:**
- Risco de loop infinito se não houver incremento
- Geralmente menos eficiente que `@for`

---

## 4. Uso do `@each` para Listas

```scss
$redes-sociais: fc, twt, snap, ist; // Lista de sufixos

@each $rede in $redes-sociais {
  .rede-#{$rede} {
    background: url('img/#{$rede}.png'); // Interpolação em URL
  }
}
```

**Expandindo para Mapas (Melhor Prática):**
```scss
$redes: (
  "facebook": "#1877f2",
  "twitter": "#1da1f2",
  "instagram": "#e1306c"
);

@each $nome, $cor in $redes {
  .btn-#{$nome} {
    background-color: #{$cor};
  }
}
```

**Vantagens:**
- Código mais semântico
- Fácil manutenção e expansão
- Associação chave-valor clara

---

## Checklist de Melhores Práticas
1. **Nomenclatura clara:** `$colunas` vs `$c`
2. **Controle de unidades:** Manter cálculos sem unidades
3. **Modularização:** Usar @use em vez de @import
4. **Segurança em loops:** Garantir condições de saída
5. **Documentação:** Comentar cálculos complexos
6. **Responsividade:** Considerar media queries em sistemas de grid
