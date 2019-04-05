# ISP - Princípio da segregação de interfaces

## 1. Motivação

O princípio da segregação de interfaces foca em reduzir o impacto de mudanças, através da utilização de interfaces especializadas e de grande estabilidade.

## 2. Descrição

O princípio de segregação de interfaces trata sobre interfaces bem definidas e coesas, que atendem clientes específicos. Este princípio é definido por Robert C. Martin na coluna [_Engineering Notebook_ do _The C++ Report_][1] como:

>  Clientes não devem ser forçados a depender de interfaces que não usam.

Para entender a intenção deste princípio, veja a seguinte estrutura de código (retirada da mesma coluna [1]):

<p align="center">
  <img src="https://user-images.githubusercontent.com/15656072/55520381-6f87f980-5652-11e9-914f-f8180e834d09.png" />
</p>

Nesta imagem, podemos ver que todas as implementações de _Transaction_ dependem da interface de _UI_ que é abstrata, no entanto,  cada _Transaction_ utiliza somente parte das funcionalidades de _UI_ - configurando uma violação do princípio de Segregação de Interfaces.

Este relacionamento funciona mas irá nos trazer problemas: qualquer mudança feita na interface _UI_ causará impacto em todas as implementações de _Transaction_. Ainda no mesmo artigo, Robert C. Martin amplia esta discussão:

> Quando clientes são forçados a depender de interfaces que não utilizam, ficam sujeitos à mudanças destas interfaces. Isto resulta em um acoplamento inadvertido entre todos os clientes. Dito de outra forma, quando um cliente depende de uma classe que contêm interfaces não utilizadas por ele, mas que outros clientes utilizam, então este cliente será afetado por todas as mudanças que estes outros clientes forçarão naquela classe. Nós gostaríamos de evitar este tipo de acoplamento onde possível, então nós queremos separar interfaces onde possível.

A solução sugerida por Robert C. Martin é segregar as interfaces de _UI_ em componentes menores e especializados.

<p align="center">
  <img src="https://user-images.githubusercontent.com/15656072/55520392-80d10600-5652-11e9-906c-ea0e7bfb7ce8.png" />
</p>

Neste novo formato, estes componentes específicos para cada tipo de _Transaction_ são muito mais estáveis, e a possibilidade de mudanças neste contrato é menor pois são utilizadas unicamente no relacionamento com esta entidade. Os componentes que dependem destas _Transaction_ estão acoplando-se com uma classe mais estável que eles!

A visão técnica apresentada por Robert C. Martin é essencial para identificarmos possíveis acoplamentos problemáticos em nossa base de código, mas um outro ponto de vista interessante para construirmos interfaces na granularidade correta em tempo de desenvolvimento pode ser vista no artigo [Role Interfaces](2) de Martin Fowler:

> Uma role interface é definida observando uma interação específica entre provedores e consumidores. Um componente provedor irá geralmente implementar diversas role interfaces, uma para cada padrão de interação.

Ao entender o relacionamento entre provedor e consumidor, podemos construir interfaces mais coesas se focarmos em modelar as interações entre eles. Sempre que uma interface carregar mais funcionalidades do que as utilizadas por uma interação, temos uma violação do Princípio de Segregação de Interfaces.


## 3. Exemplos


#### Violando o Princípio de Segregação de Interface
Considerar um cliente que gostaria de gerar um relatório apenas em TXT
```java
interface GerarRelatorio {
	void gerarExcel();
	void gerarTXT();
}
```

Cliente é obrigado a implementar metodo desnecessário `gerarExcel()`
```java
class RelatorioTorvalds implements GerarRelatorio {
	public void gerarTXT() {
		System.out.println( "Relatório em TXT" );
	}

	public void gerarExcel() {
		// Não é usado
	}
}
```
**Solução** quebrar em interfaces menores, com metodos separados, assim o Cliente escolhe o metodo desejado

```java
interface GerarRelatorioProprietario {
	void gerarExcel();
}

interface GerarRelatorioLivre {
	void gerarTXT();
}
```

## 4. Referências

\[1\] R. C. Martin, “Interface segregation principle,” Google Docs. [Online]. Available: https://drive.google.com/file/d/0BwhCYaYDn8EgOTViYjJhYzMtMzYxMC00MzFjLWJjMzYtOGJiMDc5N2JkYmJi/view. [Accessed: 24-Mar-2019].

\[2\] M. Fowler, “Role Interfaces,” martinfowler.com. [Online]. Available: https://martinfowler.com/bliki/RoleInterface.html. [Accessed: 02-Apr-2019].

[1]: https://drive.google.com/file/d/0BwhCYaYDn8EgOTViYjJhYzMtMzYxMC00MzFjLWJjMzYtOGJiMDc5N2JkYmJi/view
[2]: https://martinfowler.com/bliki/RoleInterface.html

## 5. Colaboradores

- Felipe Cesar Crestani
- Miguel Fontes
- Ivan Henrique Sandrine
