# DIP - Princípio de Inversão de Dependência

## 1. Motivação

Este princípio garante a estrutura necessária para e pela aplicação do OCP e do LSP, a abstração e controle das dependẽncias de um módulo.

## 2. Descrição

Em coluna do _Engineering Notebook_ do _The C++ Report_ entitulada [The dependency inversion principle](1), Robert C. Martin descreve o príncipio de Inversão de dependência como:

> Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações.
> Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações.

O princípio de Inversão de dependência foca no desacoplamento, utilizando-se de abstrações que invertam e direção da dependência - construindo componentes de fácil extensão e manutenção, e possibilidade de reuso. Para visualizarmos este prinícpio em ação, considere a seguinte estrutura abaixo (retirada da mesma coluna [1]):

<p align="center">
  <img src="https://user-images.githubusercontent.com/15656072/55523549-35255900-5660-11e9-9542-bef06ee7e814.png" />
</p>

O módulo _copy_ executa a operação de cópia dos caracteres do teclado, para uma impressora. Ambos os módulos de baixo nível, _Read Keyboard_ e _Write Printer_  são reusáveis, mas o módulo _Copy_ não: ele apenas consegue funcionar com estes dois submódulos. Se precisarmos ler de outra fonte, ou escrever em outro destino isto seria impossível. Além disso, mudanças nos módulos inferiores poderão forçar mudanças no módulo _Copy_! Ainda em [The dependency inversion principle](1), Robert C. Martin cita que:

> Considere as implicações de módulos de alto nível que dependem de módulos de baixo nível. São os módulos de alto nível que contêm as importantes regras de negócio e modelos de negócio de uma aplicação. São estes modelos que possuem a identidade da aplicação. Ainda assim, quando estes módulos dependem dos módulos de nível inferior, então mudanças aos módulos de nível inferior poderão ter efeitos indiretos neles; e poderão força-los a mudar.

Sabemos que o core de uma aplicação está no domínio, nas camada de negócio. É nesta camada que está a geração de valor, e é esta camada que deve ser 'servida' pelas demais camadas da aplicação - não o inverso! Devemos, então, aplicar o princípio de inversão de dependẽncias:

<p align="center">
  <img src="https://user-images.githubusercontent.com/15656072/55523557-42424800-5660-11e9-8a25-bd244870fa7c.png" />
</p>

Com esta alteração, isolamos a lógica de ambos os módulos, garantindo que o módulo _Copy_ possa funcionar com qualquer origem e destino, que implemente as abstrações _Reader_ e _Writer_. Ganhamos reusabilidade.

Ampliando nossa visão, Maurício Aniche em [Orientação a Objetos e SOLID para Ninjas, 2.9][2] coloca esta implementação de abstrações de outra forma:

> [...] sempre que uma classe for depender de outra, ela deve depender sempre de outro módulo mais estável do que ela mesma.

Se uma classe precisa de um serviço externo, de outro módulo de mesma ou outra camada, este ponto de contato deve ser feito através de um componente mais estável que ela: geralmente uma interface.

No post [The Clean Architecture](3), Robert C. Margin fala sobre o padrão arquitetural _Hexagonal_ ou _Ports and Adapters_ que utiliza de forma intensa o princípio de inversão de dependẽncias. Ao descrever as vantagens de utilizar esta arquitetura, ele cita que os sistemas produzidos por ela são:

> 1. Independentes de Frameworks
> 2. Testáveis
> 3. Independentes de UI
> 4. Independente de Databases
> 5. Independente de agentes externos

Os items 1, 3, 4, e 5 podem ser identificado como as diferentes camadas da uma aplicação. Seguindo o Princípio de Inversão de Dependência, este padrão arquitetural consegue desacopla-los através do uso de contratos chamados portas: uma camada de abstrações que definir as interações executadas entre as camadas.

<p align="center">
  <img src="https://user-images.githubusercontent.com/15656072/55523565-4d957380-5660-11e9-95a7-bb541fe7497e.jpg" />
</p>

Com o uso da Inversão de Dependência é possível controlar o impacto de mudanças, ampliar a possibilidade de reuso e garantir que as camadas de nível inferior da aplicação (mais próximo da infraestrutura) sofrerão mudanças quando as superiores (mais próximo do domínio) mudarem.

## 3. Exemplos

#### Violando o Princípio de Inversão de Dependência

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

## 4. Referências

\[1\] R. C. Martin, “Interface segregation principle,” Google Docs. [Online]. Available: https://drive.google.com/file/d/0BwhCYaYDn8EgOTViYjJhYzMtMzYxMC00MzFjLWJjMzYtOGJiMDc5N2JkYmJi/view. [Accessed: 24-Mar-2019].

\[2\] R. C. Martin, “The Clean Architecture.” [Online]. Available: http://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html. [Accessed: 03-Apr-2019].

\[3\] M. Aniche, Livro de Orientação a Objetos Solid para Ninjas - Casa do Código.

[1]: https://drive.google.com/file/d/0BwhCYaYDn8EgOTViYjJhYzMtMzYxMC00MzFjLWJjMzYtOGJiMDc5N2JkYmJi/view
[2]: https://www.casadocodigo.com.br/products/livro-oo-solid
[3]: http://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html

## 5. Colaboradores

- Felipe Cesar Crestani
- Miguel Fontes
- Ivan Henrique Sandrine
