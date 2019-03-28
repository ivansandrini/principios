## Violando o Princípio de Liskov
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