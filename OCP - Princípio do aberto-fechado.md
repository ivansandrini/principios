# Princípio aberto-fechado

## 1. Motivação

O princípio aberto-fechado sugere formas de possibilitar que o comportamento de uma classe seja alterado sem que alterações sejam feitas em seu código fonte, utilizando-se de abstrações.

## 2. Descrição

Na coluna _Engineering Notebook_ do _The C++ Report_ Robert C. Martin parafraseia Bertrand Meyer, definindo o princípio aberto-fechado como:

>  Entidades de software (classes módulos, funções, etc.) devem estar abertas para extensão, mas fechadas para modificação.

Isto significa que deve ser possível alterar o comportamento interno de uma classe, sem alterar o seu código fonte. Para alcançar este objetivo, devemos desenvolver nossos componentes de forma que estes utilizem-se de abstrações para executar seus comportamentos, o que nos possibilita alternar a implementação destas abstrações em tempo de execução.

Tenha em mente que nenhum programa pode estar 100% fechado para mudanças e, por isso, a seleção das abstrações deve ser estratégico: deve-se identificar os pontos com a maior probabilidade de mudança. Ao preparar estes pontos cruciais para serem estendidos, ganhamos velocidade ao incluir novas funcionalidade.

Em [Principles of Package Design](2), Matthias Noback descreve um interssante exemplo. Considere uma aplicação que converte um input em formato Json, XML ou Yaml. Poderíamos ter uma estrutura da seguinte forma:

<p align="center">
  <img src="https://user-images.githubusercontent.com/15656072/55597899-50f33280-5726-11e9-881f-be4f4d1329a3.png" />
</p>

Aqui, a classe `GenericEncoder` está acoplada ao `JsonEncoder` e ao `XmlEncoder`, instanciando e conhecendo os detalhes de implementação de cada uma delas, de acordo com o formato selecionado por seu cliente. A criação de uma nova instância destes _Encoders_ é feita durante a execução de seu método de encoding - desta forma, `GenericEncoder` deverá ser alterado sempre que um novo formato for suportado, Aplicando o princípio do aberto-fechado, podemos utilizar uma abstração para permitir que novos `Encoder` possam ser introduzidos com impacto menor à `GenericEncoder`.

<p align="center">
  <img src="https://user-images.githubusercontent.com/15656072/55597903-52245f80-5726-11e9-8027-be9eaf2c11c0.jpg" />
</p>

Com a introdução desta abstração, os contratos de cada `Encoder` torna-se estável: a classe `GenericEncoder` poderá interagir com qualquer `Encoder` da mesma forma. No entanto, ainda ficamos com o problema de instanciar cada um dos `Encoder`. Devemos então, adicionar uma nova abstração para representar um factory de `Encoder`.

<p align="center">
  <img src="https://user-images.githubusercontent.com/15656072/55597906-53558c80-5726-11e9-9262-9cba398e8db9.jpg" />
</p>

A abstração `EncoderFactoryInterface` garante que um Factory que construa as instâncias de `Encoder` exista e possa ser consumido por `GenericEncoder` deixando de ser sua responsabilidade a decisão de construir a instância de `Encoder` correta: ela será requerida durante sua execução, apenas. `GenericEncoder`  passa a ser aderente também ao Single Responsability Principle.

## 3. Exemplos

## 4. Referências

- \[1\] R. C. Martin, “The Open closed principle,” Google Docs. [Online]. Available: https://drive.google.com/file/d/0BwhCYaYDn8EgN2M5MTkwM2EtNWFkZC00ZTI3LWFjZTUtNTFhZGZiYmUzODc1/view. [Accessed: 24-Mar-2019].

- \[2\]S. B. Online, “2. The Open/Closed Principle - Principles of Package Design: Creating Reusable Software Components.” [Online]. Available: https://matthiasnoback.nl/book/principles-of-package-design. [Accessed: 04-Apr-2019].


[1]: https://drive.google.com/file/d/0BwhCYaYDn8EgN2M5MTkwM2EtNWFkZC00ZTI3LWFjZTUtNTFhZGZiYmUzODc1/view
[2]: https://matthiasnoback.nl/book/principles-of-package-design/
## 5. Colaboradores

- Felipe Cesar Crestani
- Miguel Fontes
- Ivan Henrique Sandrine
