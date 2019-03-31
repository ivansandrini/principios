## Violando o Princípio de Inversão de Dependência

Módulo de alto nível dependendo de módulos de baixo nível

```java
public class DesenvolvedorBackend {
    public void escreverJava() {
    }
}
public class DesenvolvedorFrontend {
    public void escreverJavascript() {
    }
}
```

Classe Projeto dependendo de DesenvolvedorBackend e DesenvolvedorFrontend
```java
public class Projeto {
    private DesenvolvedorBackend desenvolvedorBackend = new DesenvolvedorBackend();
    private DesenvolvedorFrontend desenvolvedorFrontend = new DesenvolvedorFrontend();
    public void implementar() {
        backEndDeveloper.escreverJava();
        frontEndDeveloper.escreverJavascript();
    }
}
```

**Solução** detalhes baseado em abstrações

```java
public interface Desenvolvedor {
    void escrever();
}
public class DesenvolvedorBackend implements Desenvolvedor {
    @Override
    public void escrever() {
        escreverJava();
    }
}
public class DesenvolvedorFrontend implements Desenvolvedor {
    @Override
    public void escrever() {
        escreverJavascript();
    }
}
```

Agora a classe `Projeto` depende de abstrações
```java
public class Projeto {
    private List<Desenvolvedor> desenvolvedores;
    public Project(List<Desenvolvedor> desenvolvedores) {
        this.desenvolvedores = desenvolvedores;
    }
    public void implementar() {
        desenvolvedores.forEach(d->d.escrever());
    }
}
```