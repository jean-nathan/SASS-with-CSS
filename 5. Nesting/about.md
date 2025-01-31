
# Nesting no Sass: Guia Simplificado
Aprenda a usar o aninhamento de forma organizada sem complicações!

---

## 📌 Regra Básica: 3 Níveis no Máximo

**Por quê?**  
- Código mais fácil de ler  
- Evita confusão na hora de editar  
- Previne problemas de especificidade no CSS  

**Exemplo Prático:**  
```scss
ul {                     // 1º nível
  li {                   // 2º nível
    a {                  // 3º nível (ideal)
      &:hover {          // 4º nível (já é demais!)
        /* ... */
      }
    }
  }
}
```

---

## 🎯 Operador `&` - Para Que Serve?

**Use para:**  
1. **Estados do elemento**  
   ```scss
   button {
     &:hover { /* estilo do hover */ }
     &:active { /* estilo quando clicado */ }
   }
   ```

2. **Criar classes combinadas**  
   ```scss
   .card {
     &--destaque { /* variação do card */ }
   }
   // Gera: .card--destaque
   ```

3. **Elementos pseudo**  
   ```scss
   .item {
     &::before { /* conteúdo antes do elemento */ }
   }
   ```

---

## ⚠️ Cuidado com Excesso!

**Problemas comuns:**  
```scss
// ❌ Exemplo Ruim (muito profundo)
nav {
  ul {
    li {
      a {
        span {
          /* 5 níveis! Difícil de manter */
        }
      }
    }
  }
}
```

**Solução:**  
```scss
// ✅ Versão Simplificada
.menu-link {
  /* estilos do link */
  &__icon {
    /* estilo do ícone */
  }
}
// Use classes diretas no HTML
```

---

## 🛠️ Nesting de Propriedades (Dica Extra)

**Funciona bem para:**  
- Fontes  
- Margens/Paddings  
- Backgrounds  

**Como usar:**  
```scss
// Antes
p {
  font-size: 16px;
  font-family: Arial;
  font-weight: bold;
}

// Depois (com nesting)
p {
  font: {
    size: 16px;
    family: Arial;
    weight: bold;
  }
}
```

---

## ✅ Dicas Rápidas de Ouro

1. **Pense em "3 andares"**  
   Se passar disso, crie uma nova classe

2. **Nomeie classes de forma clara**  
   `.menu-link` em vez de `nav ul li a`

3. **Use & só quando necessário**  
   Não precisa usar em tudo!

4. **Teste o CSS gerado**  
   Às vezes o nesting cria seletores muito longos

---

✨ **Lembre-se:** O objetivo é manter seu código fácil de entender, não mostrar quantos níveis você consegue aninhar!
