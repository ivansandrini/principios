# Responsabilidade Única - SRP

## 1. Motivação

O princípio da responsabilidade única foi oficialmente citado pela primeira vez no artigo "Design Principles and Design Patterns" do Robert C Martin (Uncle Bob) [1]

É considerado um dos principais princípios do SOLID, pois se não aplicado não é possível aplicar os outros princípios.

## 2. Descrição

O princípio da responsabilidade única pode ser definido como:

```
Cada classe deve ter uma única responsabilidade.
```

Uma classe deve ter um, apenas um, motivo para ser modificada. 
Se você tem mais de um motivo para alterar a classe, provavelmente a classe tem mais de um responsabilidade.

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

3.1 O que não fazer

A classe abaixo NotaFiscalService tem várias responsabilidades como: emitir, validar, imprimir, cancelar e salvar a nota fiscal. Isso fere o princípio de uma classe ter uma única responsabilidade, e deixar o código complexo com muitas linhas e cria uma grande quantidade de depêndencias de classes como: acesso a banco, geração de relatórios, regras de negócio( validação ).

```Java
public class notaFiscalService{

    public void emite(Nota nota);
    public void valida(Nota nota);
    public void cancela(Nota nota);
    public void imprime(Nota Nota);
    public void salva(Nota nota);
} 
```
3.2 O que fazer

Separar as responsabilidade em classes com uma única responsabilidade.

```Java
//Classe responsável por emitir e cancelar a nota fiscal
public class notaFiscalService{
    public void emite(Nota nota);
    public void cancela(nota nota);
}
```

```Java
//Classe responsável por validar a nota fiscal
public class notaFiscalValidate{
    public void valida(Nota nota);
}
```

```Java
//Classe responsável por gerar relatórios
public class notaFiscalReport{
    public void imprime(Nota nota);
}
```

```Java
//Classe responsável pelas ações no banco de dados 
public class notaFiscalRepository{
    public void salva(Nota nota);
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

