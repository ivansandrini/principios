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

**Preferir** dividir responsabilidades em classes menores

```java
class LeitorDeConteudo {
	void ler(InputStream inputStream) {
		/** ... **/
	}
}

class EscritorDeConteudo {
	void escrever(OutputStream outputStream) {
		/** ... **/
	}
}

class VerificadorDeExistencia {
	boolean existe() {
		/** ... **/
	}
}
``` 
