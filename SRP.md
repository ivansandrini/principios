## Violando o Princípio de Responsabilidade Unica
Classe tem muitas responsabilidades

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

Boa pratica dividir responsabilidades em classes menores

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
