# Responsabilidade Única - SRP

## 1. Motivação

O princípio da responsabilidade única foi oficialmente citado pela primeira vez no artigo [Design Principles and Design Patterns de Robert C Martin](https://fi.ort.edu.uy/innovaportal/file/2032/1/design_principles.pdf).

 É considerado um dos princípios mais importantes da orientação a objetos, pois sem sua aplicação os demais princípíos se tornam inviáveis.

## 2. Descrição

O princípio da responsabilidade única pode ser definido como:

> Cada classe deve ter uma única responsabilidade.

Uma classe deve ter um, apenas um, motivo para ser modificada. Se tiver mais de um motivo para a classe ser alterada, provavelmente a classe tem mais de um responsabilidade, tornando-a desconexa (sem coesão).

Exemplos de responsabilidades que devem ser separadas:
- Persistence
- Validation
- Notification
- Error Handling
- Logging
- Class Selection / Instantiation
- Formatting
- Parsing
- Mapping

## 3. Exemplos

#### Violando o Princípio de Responsabilidade Unica

A classe abaixo ManipuladorDeArquivo tem várias responsabilidades como: validar, ler e escrever. Isso fere o princípio de uma classe ter uma única responsabilidade, e acaba deixando o código complexo e com muitas linhas. Outro efeito indesejado é o grande acoplamento e depêndencia entre as classes.

```java
class ManipuladorDeArquivo {
	boolean existe() {
		/** ... **/
	}

	void ler(InputStream inputStream) {
		/** ... **/
	}

	void escrever(OutputStream outputStream) {
		/** ... **/
	}
}
```

Problemas ao utilizar uma classe desconexa:

- Dificuldade no reuso de suas responsabilidades;
- Dificuldades na manutenção (dificuldade em manter e/ou evoluir por conta do excesso de responsabilidades);
- Aumento na rigidez e fragilidade: quando alterar uma responsabilidade, outra pode ser comprometida;
- Alto acoplamento da classe.

Boa pratica dividir responsabilidades em classes menores:

```java
class LeitorDeArquivo {
	void ler(InputStream inputStream) {
		/** ... **/
	}
}

class EscritorDeArquivo {
	void escrever(OutputStream outputStream) {
		/** ... **/
	}
}

class VerificadorDeArquivo {
	boolean existe() {
		/** ... **/
	}
}
``` 

Assim temos um código bem mais coeso, com baixo acoplamento e de fácil manutenção.

## 4. Referências

[1] Robert C. Martin. <b>Design Principles and Design Patterns</b> \
https://fi.ort.edu.uy/innovaportal/file/2032/1/design_principles.pdf


## 5. Colaboradores

- Felipe Cesar Crestani
- Miguel Fontes
- Ivan Henrique Sandrine

