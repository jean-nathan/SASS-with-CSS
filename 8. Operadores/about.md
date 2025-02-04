# Operadores no Sass

## **1. Operações Matemáticas**
### Exemplo Original (Problemas Comuns):
```scss
$gutter: 23px;

p {
  font-size: 10px - 6 * $gutter;      // ❌ Problema: Unidades misturadas (px - px*px?)
  width: 100px + 50 - $gutter;        // ❌ Problema: Unidade "px" com número sem unidade (50)
  font-family: $font-primaria;
}
```

### **Solução: Entenda as Regras!**
1. **Ordem de Operações:**  
   O Sass segue matemática básica: multiplicação/divisão primeiro.  
   Exemplo corrigido:
   ```scss
   font-size: 10px - (6 * $gutter);  // Resultado: 10px - 138px = -128px (valor inválido!)
   ```

2. **Unidades Compativeis:**  
   Você só pode operar números com **mesmas unidades** ou **unitless**.  
   Exemplo funcional:
   ```scss
   $gutter: 23px;
   
   p {
     width: (100px + 50px) - $gutter; // ✅ 150px - 23px = 127px
   }
   ```

---

## **2. Operações com Cores (Atualizado)**
### Forma Antiga (Não Use!):
```scss
p {
  background-color: #333 + #777;  // ❌ Não funciona em versões modernas do Sass
}
```

### Forma Correta (Use Funções):
```scss
p {
  background: mix(#333, #777);    // ✅ Mistura 50% de cada cor
}
```

### **Alternativas Úteis:**
| Função              | Exemplo                   | Resultado               |
|---------------------|---------------------------|-------------------------|
| `mix(cor1, cor2)`   | `mix(#333, #777)`         | Cor intermediária       |
| `lighten(cor, %)`   | `lighten(#333, 20%)`      | Cor mais clara          |
| `darken(cor, %)`    | `darken(#777, 30%)`       | Cor mais escura         |
| `rgba(cor, opacidade)` | `rgba(#333, 0.5)`     | Cor com transparência   |

---

## **Dicas para Evitar Erros:**
1. **Parenteses São Seus Amigos:**  
   Sempre use para deixar a ordem clara: `(10px + 5px) * 2`.

2. **Cuidado com Unidades:**  
   Não misture `px`, `em`, `%`, etc., sem conversão explícita.

3. **Prefira Funções de Cor:**  
   São mais intuitivas e seguras do que operações matemáticas diretas.

---

## **Exemplo Prático Corrigido:**
```scss
$gutter: 23px;
$fonte-base: 16px;

p {
  font-size: $fonte-base - 2px;           // ✅ 14px
  width: (100% - $gutter) / 2;           // ✅ (100% - 23px) / 2
  background: mix(#333, #777);            // ✅ Cor #555
  margin: 0 $gutter * 1.5;               // ✅ 0 34.5px
}
