
## Violando o Princípio de Segregação de Interface
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