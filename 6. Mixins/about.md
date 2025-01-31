# Mixins

É uma forma de reaproveitar o codigo de um bloco que foi criado.

Exemplo do uso:

@mixin title-large {
	font-size: 4em;
	font-weight: bold;
	font-family: monospace;
	line-height: 1;
}


Para usar voce usa a palavra @includes title-large



----

## Ajuda com prefixos

 @mixin border-box {
	box-sizing: border-box;
	-moz-box-sizing: border-box;
	-webkit-box-sizing: border-box;
}

Usando o mixin:

section {
  max-width: 600px;
  margin: 0 auto;
	@include border-box
}

---


## Mixin dentro de Mixin

@mixin color-template {
	background-color: aquamarine;
	color: #fff;
}

@mixin title-large {
	font-size: 4em;
	font-weight: bold;
	font-family: monospace;
	line-height: 1;
	@include color-template;
}


---


## Argumentos

- Podemos também passar mais de 1 argumento.

Exemplo do seu uso:

@mixin separador($color) {
	&::after {
		content: '';
		display: block;
		width: 100px;
		height: 4px;
		background-color: $color;
	}
}


  h1 {
    color: $cor-primaria;
    font-family: $font-primaria;
    margin-bottom: $gutter;
		@include title-large;
		@include separador(#84E);
  }

---
