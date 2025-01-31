# Otimização de Imports no SASS

## Como evitar múltiplas requests no browser

Para garantir que os arquivos SASS sejam compilados em um único arquivo CSS e evitar múltiplas requisições HTTP:

### Use **Partial Files** (Arquivos parciais)
- Crie arquivos parciais com prefixo `_` (ex: `_colors.scss`)
- Esses arquivos não serão compilados individualmente
- São destinados apenas para importação
