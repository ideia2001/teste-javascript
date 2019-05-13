# Teste para candidatos à vaga mobile Ideia 2001

![logo](https://user-images.githubusercontent.com/13858601/49169002-eff2c280-f31f-11e8-810b-1ee26c850718.png)

## O que fará na empresa
Atuará na empresa desenvolvendo aplicativos mobile para o ramo de Auto Peças utilizando JavaScript, Cordova e SQL.

## Como fazer o teste
Clone este repositório, desenvolva seu código e envie a pasta do projeto compactada para o email vagas@ideia2001.com.br com o assunto "DEVMOBIDEIA". Enviar também currículo atualizado. Favor se identificar.

## O que Fazer
O teste é dividido em duas partes. No teste [Javascript](#JavaScript) você deverá criar um pequeno projeto web que irá mostrar uma lista de dados no estilo mobile. Enquanto que no projeto [SQL](#SQL) você deverá extrair os dados das tabelas pré definidas.

## JavaScript

### Você poderá (opcional):

- Criar uma classe no JavaScript para manipular o componente de modal ou a lista de dados.

- Utilizar Flexbox.

- Utilizar a estrutura e quantidade de arquivos da forma que achar necessário.

- Adicionar libs de sua preferência para as tarefas.

- Utilizar pré-processadores css.

- Minificar arquivos (envie também os arquivos não minificados).

Este teste foi desenvolvido utilizando HTML, CSS e Javascript ES5 puro.

Para iniciar o projeto, crie o arquivo index.html (este será o arquivo de entrada para avaliação). Crie e importe o arquivo index.js para poder trabalhar com JavaScript na aplicação.

Este repositório contém o arquivo produtos.json, nele está contido um array de objetos que representam os produtos que utilizaremos como teste para desenvolver a aplicação. À fim de facilitar o carregamento desses dados, disponibilizamos também o arquivo produtos.js que poderá ser importado no cabeçalho do index.html. Caso opte pelo segundo caso, o array de produtos estará disponível dentro da variável global ```window.produtos```.

1. No arquivo HTML você deverá criar um [header](#header) de posição fixa no topo da tela.

2. Crie um botão no centro da área restante da tela. Esta parte será representada pela área total da tela menos a altura do header. O botão deverá estar sempre centralizado nesta área, independente do tamanho da tela.

3. Detecte o evento de click no botão criado anteriormente. Quando o evento for disparado, você deverá exibir uma tela de [modal](#modal) contendo a lista de produtos que foi carregado anteriormente do arquivo ```produtos.json```. Para cada produto, crie uma linha na lista e exiba as informações contidas no objeto.

| <b>Ex.:</b> | Descricao | Quantidade |
| ----------- | --------- | ---------- |
| | Disco de Freio | 5 |

4. Crie um header para o componente de modal.

5. Quando um produto da lista receber o evento de click sua linha deverá mudar de cor.

6. Quando um outro produto da lista for clicado, você deverá adicionar o valor da quantidade deste segundo produto dentro da quantidade do primeiro produto. Depois disso, remova o segundo produto da lista de produtos e ordene novamente a lista de todos os produtos de acordo com a quantidade. É interessante destacar aonde o produto selecionado anteriormente ficou posicionado após a ordenação da lista.

<b>Exemplo:</b>

<b>Clique 1:</b>
- Seleciona o primeiro produto.

<b>Clique 2:</b>
- Adiciona a quantidade do produto 2 ao produto 1.
- Remove o produto 2 da lista de produtos.
- Reordena a lista de produtos.
- Mostre por 1 segundo o posicionamento do produto 1 após a ordenação da lista.

<b>Importante:</b> O processo do click 1 e 2 poderá ser repetido até restar apenas um produto na lista.

7. Sempre que ocorrer um agrupamento, armazenar:
- o produto que foi selecionado (produto 1)
- o produto que foi removido da lista (produto 2)
- a quantidade total do produto 1 após a soma

8. Criar um botão no header do modal que quando clicado exibirá as informações armazenadas no passo 7.

### Regras
- Os produtos deverão estar sempre ordenados na lista de acordo com a propriedade "Quantidade" do objeto. Ordene também após os agrupamentos dos produtos.

- Um produto não pode somar a sua própria quantidade e nem salvar ação no histórico nesta situação.

- Quando restar apenas um produto, ele não poderá ser selecionado na lista. Sendo assim, sempre haverá um único produto no final com a quantidade somada de todos os outros produtos.

### Referência

<b id="header">Header:</b> É um cabeçalho posicionado de forma fixa no topo da tela. pode ser chamado também de barra de navegação.

<b id="modal">Modal:</b> Modal é um elemento div que se sobrepõe a qualquer página do html e ocupa o tamanho total da tela, tanto em largura quanto altura.

## SQL
Para o teste SQL você deverá criar os seguintes SELECTs:

1. Todos os ```Produtos``` (Código e Descrição), e ```Montadoras``` (Descrição) / ```Veiculos``` (Descrição) / ```ObsProdutoVeiculo``` correspondentes - Ordenação: Primeiro o veículo "MONZA", depois o "FOCUS" e o restante em ordem alfabética por Descrição de "Produto, Montadora, Veiculo".

2. SELECT ```Produto``` (Código e Descrição) - Apenas para produtos com veículos.

3. SELECT ```Produto``` (Código e Descrição), ```Veiculo``` (Descrição) - Apenas para veículos sem montadora.

4. ```Montadoras``` (Descrição) e a quantidade de produtos para cada montadora.

5. SELECT ```Produto``` (Descrição), ```Veiculo``` (Descrição, Descrição, Descrição, ...) - Todos os produtos, com suas aplicações concatenadas por ```Vírgula```, exemplo: ```Amortecedor Dianteiro, GOLF, POLO, CORSA```.<br />Obs.: Esta query é opcional!!!

| Tabelas |
| ------- |
| PRODUTO |
| VEICULO |
| MONTADORA |
| PRODUTO_VEICULO |

```sql
/* cria_tabelas.sql */

CREATE TABLE MONTADORA(
	CodigoMontadora		INT		NOT Null,
	DescricaoMontadora	VARCHAR(50)	NOT Null,
	PRIMARY KEY(CodigoMontadora));

CREATE TABLE VEICULO(
	CodigoVeiculo		INT		NOT Null,
	DescricaoVeiculo	VARCHAR(50)	NOT Null,
	CodigoMontadora		INT		Null,
	PRIMARY KEY(CodigoVeiculo),
	FOREIGN KEY (CodigoMontadora) REFERENCES MONTADORA(CodigoMontadora));

CREATE TABLE PRODUTO(
	CodigoProduto		INT		NOT Null,
	DescricaoProduto	VARCHAR(50)	NOT Null,
	PRIMARY KEY(CodigoProduto));

CREATE TABLE PRODUTO_VEICULO(
	CodigoProduto		INT		NOT Null,
	CodigoVeiculo		INT		NOT Null,
	ObsProdutoVeiculo	VARCHAR(2000)	Null
	PRIMARY KEY(CodigoProduto,CodigoVeiculo),
	FOREIGN KEY (CodigoProduto) REFERENCES PRODUTO(CodigoProduto),
	FOREIGN KEY (CodigoVeiculo) REFERENCES VEICULO(CodigoVeiculo));
```

## Dados das tabelas (caso necessário)

### MONTADORA
| CodigoMontadora | DescricaoMontadora |
| --------------- | ------------------ |
| 100 | FIAT | 
| 101 | VOLKSWAGEN | 
| 102 | CHEVROLET| |
| 103 | FORD |

### PRODUTO
| CodigoProduto | DescricaoProduto |
| ------------- | ---------------- |
| 1 | Amortecedor Dianteiro |
| 2 | Amortecedor Traseiro |
| 3 | Junta do Motor |
| 4 | Parafuso da Roda |
| 5 | Biela |
| 6 | Farol |
| 7 | Lona |

### VEICULO
| CodigoVeiculo |	DescricaoVeiculo | CodigoMontadora |
| ------------- | ---------------- | --------------- |
| 1 |	GOLF |	101
| 2 |	POLO |	101
| 3 |	CORSA |	102
| 4 |	MONZA |	102
| 5 |	FOCUS |	103
| 6 |	PICKUPS |	NULL

### PRODUTO_VEICULO
| CodigoProduto | CodigoVeiculo | ObsProdutoVeiculo |
| ------------- | ------------- | ----------------- |
| 1 | 1 | NULL |
| 1 | 2 | Todos |
| 1 | 3 | Apenas no 16V |
| 2 | 1 | NULL |
| 2 | 2 | NULL |
| 2 | 3 | NULL |
| 2 | 4 | NULL |
| 2 | 5 | NULL |
| 2 | 6 | NULL |
| 3 | 5 | NULL |
| 3 | 6 | NULL |
| 4 | 4 | Com Roda 4 Furos |
| 5 | 1 | NULL |
| 6 | 1 | NULL |
| 6 | 2 | NULL |
| 6 | 3 | NULL |
| 6 | 5 | NULL |
| 7 | 6 | NULL |
