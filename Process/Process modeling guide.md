<script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>

# Process modeling guide

## Introduction
Supply chain experts need to translate their knowledge into training materials to operational teams. Modeling the processes in question can help a lot with the translation. The 
following document will delineate a procedure to do exactly that.  

## Process variant definition
The first step is to isolate and caracterize the process variant to be mapped. Operational processes can have many flavors. Let's consider the picking as an exemple. Pickings can be done by unit, box or pallet, in batch or by client order. Besides, no matter the conceptual model, the implementation done by each company will differ.

Exemple:
*Process variant*  
- Picking by box and multiple client orders.

## Process flow
The second step is to identify the sequence of activities. At this point, only the activity name and it's connections with the others activities are needed. The modeling should be done using the mermaid syntax.

Segue a syntax a ser utilizada:  
- inicie um bloco de código com ```mermaid
- defina o tipo de gráfico (graph TD).
- Represente cada atividade por uma letra maiúscula, seguida pelo nome que deve aparecer no gráfico entre colchetes [].
- Represente cada extra por uma letra maiúscula, seguida pelo nome que deve aparecer no gráfico entre colchetes e barras [//].
- Represente decisões por uma letra maiúscula, seguida pelo nome que deve aparecer no gráfico entre chaves {}.
- Represente conexões sequencias entre atividades por -->
- Represente conexões entre atividades e extras por ---
- Represente texto nas conexões por --"Texto--> ou --"Texto"---
- Feche o bloco de código com ```
- Limite o número de componentes a 10, por conta da renderização. Se for necessário, quebre o processo em diferentes blocos, utilizando o componente de ligação ((Número_do_link)) para realizar a conexão visual entre diagramas.

Exemple:
```mermaid
graph TD
	A[Atividade1] --> B[Atividade2]
	B --- C[/Extra1/]
	B --> D{Decisão1}
	D --"Sim"--> E[Atividade3]
	D --"Não"--> F[Atividade4]
	F --> 1((1))
```

## Additional information
Include any information deemed important to understand the process. This information can be at the variant level, or related to one specific activity.
At the process level, use a list (-) to formalize the content. At the activity level, use a table. To make a table, use vertical bar characters to denote cells. Start with column headers, separate with a row of cells with hyphens, then add further rows of cells.

Exemple:

*Overall*
- the picking is performed using a chariot, which ports 2 pallets.
- Each pallet will contains 1 client order.
- Client orders are paired based on the chosen carrier.

*Activities*  

|Activity|Comment|
|:-------|:-------|
|Cola a etiqueta de expedição |A impressora fica próxima da doca 12 |

+++

## Putting all together: Picking by box and multiple client orders.

*Process variant*  
- Picking by box and multiple client orders.

*Overall*
- the picking is performed using a chariot, which ports 2 pallets.
- Each pallet will contains 1 client order.
- Client orders are paired based on the chosen carrier.

```mermaid
graph TD
	A[Recebe o pedido no coletor] --> B[Inicia separação]
	B --> C[Seleciona um palete]
	C --- D[/Seleção de palete/]
	C --> E[Se dirige a primeira posição]
	E --- F[/Entender o layout do armazem/]
	E --> G[Bipa a posição]
	G --> H{Valida?}
	H --"Não"--> I[A etiqueta da posição está errada]
	H --Sim--> 1((1))
```

```mermaid
graph TD
	1((1)) --> I[Bipa a caixa]
	I --> J{Valida?}
	J --"Não"--> L[/Erro na bipagem do produto/]
	J --Sim--> M[Verifica quantidade para selecionar]
	M --> N[Coloca as caixas no palete de picking]
	N --- O[/Como montar um palete/]
	N ---> P[Indica a quantidade separada]
	P --- Q[/Falta de produto/]
	P --- R[/Inner / Master: entender as embalagens/]
	P ---> S[/Valida a separação/]
	S --> 2((2))
```

```mermaid
graph TB
	2((2)) --> S[Tela mostra o próximo item]
	S --> T[Terminar todos os itens]
	T --> U[Vai para a impressora de saida]
	U --> V[Cola a etiqueta de expedição]
	V --- X[/As informações na etiqueta de expedição/]
	V --> Y[Vai para a doca de expedição]
	Y --> Z[Cola a etiqueta de expedição]
	Z --> AA[Vai para a doca de expedição]
	AA --> AB[Bipa o palete]
	AB --> AC[Bipa a doca]
	AC --> AD[Deixa o palete na doca]
```

*Activities*  

|Activity|Comment|
|:-------|:-------|
|Cola a etiqueta de expedição |A impressora fica próxima da doca 12aa |