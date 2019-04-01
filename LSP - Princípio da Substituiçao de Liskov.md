# Princípio da Substituição de Liskov

## 1. Motivação

O princípio da substituiçao de Liskov leva o nome da sua criadora Barbara Liskov, que o apresentou no artigo "Family Values: A Behavioral Notion of Subtyping" [1].

O princípo se tornou popular quando foi amplamente usado por Robert Martin em seus livros como Clean Code[2] e Refactoring [3].

## 2. Descrição

O princípio da Substituição de Liskov pode ser definido como

```
Uma classe base deve poder ser substituída pela sua classe derivada.
```
Uma subclasse deve sobrescrever os métodos da superclasse de forma que a funcionalidade continue a mesma.



## 3. Exemplos

O exemplo mais simples da violaçao do LSP é quando uma classe herda métodos que alterem a funcionalidade de forma errada como o exemplo abaixo:

```Java
public class Retangulo {
    void altura(int altura);
    void largura(int largura);
}
```

```Java
public class Quadrado extends Retangulo {
    @Override 
    void altura(int altura);
    @Override 
    void largura(int largura);
}
```
Uma forma fácil de identificar a violaçao de LSP substituindo o conceito de herença por "É um". Onde no exemplo temos "O quadrado <b>é um</b> retangulo".

Apesar de na vida real um quadrado ser um retangulo, na programaçao orientada a objetos não é uma verdade absoluta, pois se alterarmos somente a largura de um quadrado estamos violando o LSP.

## 4. Referências

[1] Barbara Liskov. <b>Family Values: A Behavioral Notion of Subtyping</b>
https://www.cs.cmu.edu/~wing/publications/LiskovWing94.pdf

[2] Clean Code: A Handbook of Agile Software Craftsmanship

[3] Refactoring: Improving the Design of Existing Code 


## 5. Colaboradores

- Felipe Cesar Crestani
- Miguel Fontes
- Ivan Henrique Sandrine

