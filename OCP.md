## Violando o Princípio de Aberto/Fechado

Serviço de desconto vai aumentar e ficar mais complexo a cada novo desconto
```java
public class DescontoPadrao {
    public BigDecimal aplicar(BigDecimal valor) {
    	/** Regra de desconto **/
    }
}

public class DescontoParceria {
    public BigDecimal aplicar(BigDecimal valor) {
    	/** Regra de desconto **/
    }
}
public class ServicoDeDesconto {
    public BigDecimal aplicarDescontoPadrao(BigDecimal valor,DescontoPadrao desconto) {
 		/** Regra de desconto **/
    }
    public BigDecimal aplicarDescontoParceria(BigDecimal valor,DescontoParceria desconto) {
        /** Regra de desconto **/
    }
}
```

**Solução** criar uma interface de Desconto

```java
public interface Desconto {
    BigDecimal apply(BigDecimal valor);
}

public class DescontoPadrao implements Desconto {
    public BigDecimal aplicar(BigDecimal valor) {
    	/** Regra de desconto **/
    }
}

public class DescontoParceria implements Desconto {
    public BigDecimal aplicar(BigDecimal valor) {
    	/** Regra de desconto **/
    }
}
```

Novos descontos serão aplicados sem alterar a classe de Serviço
```java
public class ServicoDeDesconto {
    public BigDecimal aplicarDescontos(BigDecimal valor,Discount[] descontos) {
        BigDecimal valorDoDesconto = valor.add(BigDecimal.ZERO);
        for(Desconto desconto:descontos) {
            valorDoDesconto = desconto.apply(valorDoDesconto);
        }
        return discountPrice;
    }
}
``` 
