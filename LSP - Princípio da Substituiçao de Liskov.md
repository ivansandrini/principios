# LSP - Princípio da Substituição de Liskov

## 1. Motivação

O princípio da substituiçao de Liskov leva o nome da sua criadora Barbara Liskov, e foi apresentado no artigo "Family Values: A Behavioral Notion of Subtyping" [1].

O princípo se tornou popular quando foi amplamente usado por Robert Martin em seus livros como Clean Code[2] e Refactoring [3].

## 2. Descrição

O princípio da Substituição de Liskov pode ser definido como

> Uma classe base deve poder ser substituída pela sua classe derivada.

Ja a definição de Robert C. Martin define como:

> Subtipos devem ser substituíveis pelos seus tipos base.

Ou seja, uma subclasse deve sobrescrever os métodos da superclasse de forma que a funcionalidade continue a mesma.


## 3. Exemplos

Ocorre uma violaçao do LSP quando uma classe herda métodos que alterem a funcionalidade da herdada como o exemplo abaixo:

### Violando o Princípio de Liskov

Abstração incorreta
```java
class MeioDeTransporte {
	double obtemVelocidade(){}
	void ligaMotor(){}
}

class Carro extends MeioDeTransporte {
	@Override 
    void ligaMotor(){}	
}
```

Ainda passa
```java
class BicicletaMotorizada extends MeioDeTransporte {
   @Override 
   void ligaMotor(){}	
}
```

Agora pegou...
```java
class Bicicleta extends MeioDeTransporte {
   @Override 
   void ligaMotor(){}	
}
```

**Solução** adicionar mais um nivel de abstração

```java
class MeioDeTransporte {
	double obtemVelocidade(){}
}
class MeioDeTransporteAMotor extends MeioDeTransporte {
	void ligaMotor(){}
}
class MeioDeTransporteSemMotor extends MeioDeTransporte {
}
```

Uma forma fácil de identificar a violaçao de LSP é trocar o conceito de herança por "É um", onde no exemplo temos "A bicicleta é um meio de transporte sem motor".

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

