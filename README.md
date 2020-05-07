
# Correios Brasil

  

<h4  align="center">

  

<img  src="https://media.giphy.com/media/eRIrROHUPJvgs/giphy.gif"/><br>

  

<b>Descomplicando os Correios!</b> 🦸‍♂️

  

</h4>

  

<p  align="center">

  

<a  href="https://lucasfinoti.netlify.app">

  

<img  alt="Made by Rocketseat"  src="https://img.shields.io/badge/made%20by-LucasFinoti-red">

  

</a>

  

<img  alt="License"  src="https://img.shields.io/badge/license-MIT-red">

  

</p>

  

<p  align="center">

  

[![NPM](https://nodei.co/npm/correios-brasil.png?mini=true)](https://www.npmjs.com/package/correios-brasil/)

  

</p>

  

  

<br>

  

# O que é o Correios Brasil ?

  

O Correios Brasil é uma biblioteca que aparece como alternativa para juntar em um único lugar todas as ferramentas necessárias para você trabalhar com os correios. Otimizar sua loja virtual ou seu serviço com um único pacote capaz de te entregar exatamente o que você precisa !

  
  

## Como instalar

  

```

npm install correios-brasil --save

```

  

## Como consultar um CEP

  

  

``` javascript

const { CorreiosBrasil } = require("correios-brasil");

  

let  args = {
	// Não se preocupe com a formatação dos valores de entrada do cep, qualquer uma será válida (ex: 21770-200, 21770 200, 21asa!770@###200 e etc),

	sCepDestino:  "21770200",
};

cep = new  CorreiosBrasil(args);

cep.consultarCEP().then((response) => {
	console.log(response.json);
});

```

  

  

### Resposta

  

  

Com sucesso:

  

``` javascript

{

cep: '21770-200',

logradouro: 'Rua Claudino Barata',

complemento: '',

bairro: 'Realengo',

localidade: 'Rio de Janeiro',

uf: 'RJ',

unidade: '',

ibge: '3304557',

gia: ''

}

```

  

  

## Como consultar o preço e as demais informações de uma encomenda

  

  

``` javascript

const { CorreiosBrasil } = require("correios-brasil");

  

let  args = {

// Não se preocupe com a formatação dos valores de entrada do cep, qualquer uma será válida (ex: 21770-200, 21770 200, 21asa!770@###200 e etc),

sCepOrigem:  "81200100",

sCepDestino:  "21770200",

nVlPeso:  "1",

nCdFormato:  "1",

nVlComprimento:  "20",

nVlAltura:  "20",

nVlLargura:  "20",

sCdMaoPropria:  "n",

nVlValorDeclarado:  "0",

sCdAvisoRecebimento:  "n",

nCdServico:  "04014",

nVlDiametro:  "0",

};

  

correios = new  CorreiosBrasil(args);

  

correios

.calcularPreço()

  

.then((response) => {

console.log(response.json);

});

```

  

  

### Resposta

  

Com sucesso:

  

``` javascript

{

Codigo: '04014',

Valor: '53,10',

PrazoEntrega: '13',

ValorSemAdicionais: '53,10',

ValorMaoPropria: '0,00',

ValorAvisoRecebimento: '0,00',

ValorValorDeclarado: '0,00',

EntregaDomiciliar: 'S',

EntregaSabado: 'S',

obsFim: 'O CEP de destino está sujeito a condições especiais de entrega pela ECT e será realizada com o acréscimo de até 7 (sete) dias úteis ao prazo regular.',

Erro: '011',

MsgErro: 'O CEP de destino está sujeito a condições especiais de entrega pela ECT e será realizada com o acréscimo de até 7 (sete) dias úteis ao prazo regular.'

}

  

```

  

## Como rastrear uma encomenda (EM DESENVOLVIMENTO)

``` javascript

const { CorreiosBrasil } = require("./classes/correios");

  

let  args = {

codRastreio: ["LB334490757SE"], //futuramente serão aceitas mais de uma encomenda por vez !

};

  

correios = new  CorreiosBrasil(args);

  

correios.rastrearEncomendas().then((response) => {

console.log(response.json);

});

```

  

### Resposta

  

Com sucesso:

``` javascript

{

tipo: 'PO',

status: '01',

data: '20/03/2020',

hora: '10:25',

descricao: 'Objeto postado',

local: 'SUECIA',

codigo: '00752000'

}

```

# Argumentos para a consulta da API

  

-  ``codRastreio`` - **Array[String]**

Array com os códigos de rastreio

  
  

-  ``nCdServico`` - **String**

  
  

Código do serviço:

  

  

- 04014 = SEDEX à vista

  

  

- 04065 = SEDEX à vista pagamento na entrega

  

  

- 04510 = PAC à vista

  

  

- 04707 = PAC à vista pagamento na entrega

  

  

- 40169 = SEDEX12 ( à vista e a faturar)

  

  

- 40215 = SEDEX 10 (à vista e a faturar)

  

  

- 40290 = SEDEX Hoje Varejo

  

  

  

-  ``sCepOrigem`` - **String**

  

  

  

CEP de Origem. Exemplo: **05311900**

  

  

  

-  ``sCepDestino`` - **String**

  

  

  

CEP de Destino

  

  

  

-  ``nVlPeso`` - **String**

  

  

  

Peso da encomenda, incluindo sua embalagem. O peso deve ser informado em quilogramas. Se o formato for Envelope, o valor máximo permitido será 1 kg

  

  

  

-  ``nCdFormato`` - **Inteiro**

  

  

  

Formato da encomenda (incluindo embalagem)

  

  

- 1 = Formato caixa/pacote

  

  

- 2 = Formato rolo/prisma

  

  

- 3 = Envelope

  

  

  

-  ``nVlComprimento`` - **Decimal**

  

  

  

Comprimento da encomenda (incluindo embalagem), em centímetros

  

  

  

-  ``nVlAltura`` - **Decimal**

  

  

  

Altura da encomenda (incluindo embalagem), em centímetros. Se o formato for envelope, informar zero (0)

  

  

  

-  ``nVlLargura`` - **Decimal**

  

  

  

Largura da encomenda (incluindo embalagem), em centímetros

  

  

  

-  ``nVlDiametro`` - **Decimal**

  

  

  

Diâmetro da encomenda (incluindo embalagem), em centímetros

  

  

  

-  ``sCdMaoPropria`` - **String**

  

  

Indica se a encomenda será entregue com o serviço adicional mão própria

  

  

- S = sim

  

  

- N = não **PADRÃO**

  

  

  

-  ``nVlValorDeclarado`` - **Decimal**

  

  

Indica se a encomenda será entregue com o serviço adicional valor declarado. Neste campo deve ser apresentado o valor declarado desejado, em Reais

  

  

  

-  ``sCdAvisoRecebimento`` - **String**

  

  

Indica se a encomenda será entregue com o serviço adicional mão própria

  

  

- S = sim

  

  

- N = não **PADRÃO**

  
###  O que está em desenvolvimento ?

- Realizar a limpeza e reorganização dos códigos  🔴
- Realizar a reorganização arquivos  🔴
- Terminar de desenvolver o rastreio de encomendas  🟡.
- Atualizar o package.json e o README.md 🟢.
 

  

### 👍 Contribuição

  

  

Want to contribute? Great!

  

  

1. Fork it

  

2. Create your feature branch (git checkout -b my-new-feature)

  

3. Commit your changes (git commit -m 'Add some feature')

  

4. Push to the branch (git push origin my-new-feature)

  

5. Create new Pull Request

  

  

### License

  

----

  

  

MIT License

  

  

Copyright (c) 2020 Lucas Finoti

  

  

[See more about the license][LICENSE]

  

  

[LICENSE]: <https://github.com/FinotiLucas/Correios-Brasil/blob/master/LICENSE>