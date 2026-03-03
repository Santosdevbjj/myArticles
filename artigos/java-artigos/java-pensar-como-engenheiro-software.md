## Java na Prática: Orientação a Objetos para Pensar como Engenheiro de Software

   
   Você sabia que dominar os Fundamentos de Java vai muito além de aprender sintaxe?

      Resumo Executivo

   Da teoria à produção: um guia prático de Orientação a Objetos, TDD e BDD em Java.

A jornada de um desenvolvedor Java moderno vai muito além de escrever código.

Ela exige pensar, modelar e validar como um verdadeiro engenheiro de software.

Este artigo apresenta, de forma prática e aplicada, como transformar teoria em solução real.

Usaremos Java, Spring Boot e metodologias de engenharia de software como TDD e BDD.

Ao longo do conteúdo, você encontrará:

• Fundamentos de Orientação a Objetos: Classes, objetos, atributos, comportamentos e construtores com exemplos reais.

•   Modelagem com CRC e Relacionamentos: Técnicas de design como cartões CRC, associação, agregação e composição.

•   Encapsulamento e Proteção de Dados: Como evitar bugs críticos com validação e acesso controlado.

•  Princípios de Design (SOLID): Tell, Don't Ask, baixo acoplamento e Law of Demeter para sistemas flexíveis e seguros.

•   Interfaces e Polimorfismo: Flexibilidade com contratos e múltiplas implementações sem alterar código existente.

• Herança e Reutilização: Hierarquias de classes e o Princípio de Substituição de Liskov.

•  Testes Automatizados com TDD e BDD: Metodologias de qualidade com exemplos práticos usando JUnit, Mockito, Cucumber e RestAssured.

•   Programação Defensiva e Tratamento de Erros: Uso de exceções e Optional para evitar falhas em produção.

•    Membros Estáticos e Compartilhamento de Estado: Diferença entre atributos de instância e de classe.

•   Projeto Funcional no GitHub: Microsserviço completo com Spring Boot, Docker, segurança e testes automatizados.

Ao final, você terá uma visão sólida e aplicada de como construir sistemas Java robustos. Sistemas testáveis e alinhados com os princípios da engenharia de software moderna.

É sobre pensar como um engenheiro de software.Projetar sistemas claros, reutilizáveis e fáceis de evoluir.

Neste artigo, exploraremos de forma detalhada e prática os principais conceitos da programação orientada a objetos em Java.

A base sobre a qual se constroem aplicações robustas.

Vamos do conceito ao código, passando por boas práticas, modelagem e testes automatizados.


  Introdução

Java é essencial para sistemas corporativos, aplicações web, mobile, nuvem e IoT.

Segundo a Statista (2024), permanece entre as linguagens mais populares globalmente. Isso não acontece por acaso.

Sua combinação de orientação a objetos, portabilidade e maturidade tecnológica cria bases sólidas.

Bases para qualquer projeto de software profissional.

Mas aqui está a verdade: **saber sintaxe não é suficiente**.

A diferença entre código funcional e código profissional está nos fundamentos de Orientação a Objetos.

Este artigo mostrará, passo a passo, os fundamentos orientados a objetos em Java.

Com exemplos reais e boas práticas que você pode aplicar hoje.


      Fundamentos de Orientação a Objetos e Classes em Java

A Orientação a Objetos (OO) é um paradigma de programação baseado no conceito de objetos.

Objetos encapsulam dados (atributos) e comportamentos (métodos).

O objetivo é simular entidades e relações do mundo real dentro do código.

Criando sistemas mais intuitivos e manuteníveis.

 Os Quatro Pilares da Orientação a Objetos

Antes de mergulharmos nos exemplos, é fundamental compreender os pilares que sustentam a OO:

| Pilar | Definição | Benefício |
|-------|-----------|-----------|
| **Encapsulamento** | Proteger dados internos, expondo apenas o necessário | Segurança e manutenibilidade |
| **Abstração** | Expor apenas o essencial, escondendo a complexidade | Simplicidade de uso |
| **Herança** | Compartilhar atributos e comportamentos entre classes | Reutilização de código |
| **Polimorfismo** | Mesmo método, comportamentos diferentes | Flexibilidade e extensibilidade |

Esses pilares são a base de tudo que veremos a seguir.

Cada conceito prático que apresentaremos se apoia em um ou mais desses fundamentos.

  Classes na Teoria e em Java

| Conceito | Teoria | Java (Exemplo) |
|----------|--------|----------------|
| **Classe** | Molde para criar objetos. Define estrutura (atributos) e comportamento (métodos). | `public class Carro { ... }` |
| **Objeto** | Instância concreta de uma classe. | `Carro meuCarro = new Carro();` |
| **Atributo** | Características do objeto. | `String cor; double velocidade;` |
| **Estado** | Valores atuais dos atributos. | `meuCarro.cor = "Vermelho"` |
| **Comportamento** | Ações que o objeto executa. | `meuCarro.acelerar()` |
| **Construtor** | Inicializa o objeto no momento da criação. | `public Carro(String cor) { ... }` |

 Exemplo Prático — Classe Carro

```java
public class Carro {
    // Atributos (Estado)
    String cor;
    int ano;
    double velocidadeAtual;

    // Construtor
    public Carro(String cor, int ano) {
        this.cor = cor;
        this.ano = ano;
        this.velocidadeAtual = 0.0;
    }

    // Métodos (Comportamento)
    public void acelerar(double incremento) {
        this.velocidadeAtual += incremento;
        System.out.println("Acelerando. Velocidade: " + 
            this.velocidadeAtual + " km/h");
    }

    public void frear() {
        this.velocidadeAtual = 0.0;
        System.out.println("O carro parou.");
    }

    public String getCor() {
        return cor;
    }
}
```

Classe de Teste:

```java
public class Main {
    public static void main(String[] args) {
        Carro meuCarro = new Carro("Azul", 2022);
        Carro carroVizinho = new Carro("Prata", 2020);

        System.out.println("Meu carro é " + meuCarro.getCor());
        meuCarro.acelerar(50.0);
        
        System.out.println("Carro do vizinho é " + carroVizinho.getCor());
        carroVizinho.acelerar(30.0);
        meuCarro.frear();
    }
}
```

  Conceito-chave: Cada objeto tem seu próprio estado, independente dos demais.

Isso é a essência da orientação a objetos.



   Modelagem com CRC e Relacionamentos

Antes de escrever código, é essencial pensar na estrutura do sistema.

Projetos que falham geralmente começam com design fraco.

Uma técnica simples e poderosa é o Cartão CRC (Classe — Responsabilidade — Colaboração).

  CRC significa:

-  Classe (C) → Nome da entidade (ex.: Carro, Cliente)
-  Responsabilidade (R) → O que a classe sabe e faz
-  Colaboração (C) → Com quais outras classes interage

    Exemplo: Sistema Bancário

  ContaBancaria:

| **Sabe** | **Faz** | **Colabora** |
|----------|---------|--------------|
| Saldo, Número da conta | Depositar, Sacar, Emitir extrato | Histórico de transações |



  Cliente:

| **Sabe** | **Faz** | **Colabora** |
|----------|---------|--------------|
| Nome, CPF, Endereço | Abrir conta, Mudar endereço | ContaBancaria |


     Relacionamentos entre Classes

Os três principais tipos de relacionamento são:

-   Associação — relação "tem um" (Cliente → Conta)
-   Agregação — relação forte, mas independente (Biblioteca agrega Livros)
-   Composição — dependência total (Casa composta por Cômodos)

```java
public class Cliente {
    private ContaBancaria conta;

    public Cliente(ContaBancaria conta) {
        this.conta = conta;
    }
    
    public void realizarDeposito(double valor) {
        this.conta.depositar(valor);
    }
}
```

 Diagrama UML Simples:

```
┌─────────────┐         ┌──────────────────┐
│   Cliente   │───────>│ ContaBancaria    │
├─────────────┤         ├──────────────────┤
│ - nome      │         │ - saldo          │
│ - cpf       │         │ - numeroConta    │
├─────────────┤         ├──────────────────┤
│ + depositar()│         │ + depositar()    │
└─────────────┘         │ + sacar()        │
                        └──────────────────┘
```



 Principais Princípios de Design (SOLID)

Antes de mergulharmos em encapsulamento e interfaces, é importante entender os princípios SOLID. Eles são a base da engenharia de software moderna.

SOLID é um acrônimo para cinco princípios fundamentais:

| Princípio | Sigla | Definição |
|-----------|-------|-----------|
| **Single Responsibility** | SRP | Uma classe deve ter apenas uma razão para mudar |
| **Open/Closed** | OCP | Aberto para extensão, fechado para modificação |
| **Liskov Substitution** | LSP | Subclasses devem substituir superclasses sem quebrar o programa |
| **Interface Segregation** | ISP | Interfaces específicas são melhores que interfaces genéricas |
| **Dependency Inversion** | DIP | Dependa de abstrações, não de implementações concretas |



Ao longo deste artigo, veremos esses princípios em ação.

O SRP aparece no encapsulamento e na separação de responsabilidades.

O OCP é demonstrado no uso de interfaces e polimorfismo.

O LSP é essencial na herança segura.

Vamos começar com o encapsulamento, que é o primeiro passo para aplicar o SRP.



    Encapsulamento: Protegendo seu Código

•  Dica Profissional  
• Essa centralização da lógica de negócio é o primeiro passo para o Princípio da Responsabilidade Única (SRP).

    O Problema Real

Em 2019, um bug em um sistema financeiro causou prejuízo de milhões.

O motivo? Atributos públicos sem validação.

  Código problemático:

```java
// ❌ Vulnerável
public class ContaBancaria {
    public double saldo; // Qualquer código pode modificar!
}

// Em outro lugar...
conta.saldo = -1000; // Nada impede isso!
```

 A Solução: Encapsulamento

Encapsulamento protege os dados internos da classe.

Expõe apenas o necessário por meio de métodos públicos com validação.

```java
// ✅ Seguro
public class ContaBancaria {
    private double saldo;

    public ContaBancaria(double saldoInicial) {
        if (saldoInicial < 0) {
            throw new IllegalArgumentException(
                "Saldo inicial não pode ser negativo");
        }
        this.saldo = saldoInicial;
    }

    public double getSaldo() { 
        return saldo; 
    }

    public void depositar(double valor) {
        if (valor <= 0) {
            throw new IllegalArgumentException("Valor deve ser positivo");
        }
        this.saldo += valor;
    }
    
    public boolean sacar(double valor) {
        if (valor > this.saldo) {
            return false; // Saldo insuficiente
        }
        this.saldo -= valor;
        return true;
    }
}
```

  Benefício: Todo código que usa `ContaBancaria` já está protegido contra valores inválidos.

A validação está centralizada em um único lugar.



    Princípio "Tell, Don't Ask" e Baixo Acoplamento

    O Problema do Alto Acoplamento

Acoplamento alto acontece quando uma classe conhece demais sobre os detalhes internos de outra.

Isso torna o código frágil a mudanças.

```java
// ❌ "Ask" - Alto Acoplamento
public class ProcessadorPedido {
    public void processar(Pedido pedido, Cliente cliente) {
        // Classe externa toma decisões baseadas em dados internos
        if (pedido.getTotal() > 0 && 
            cliente.getCredito() >= pedido.getTotal()) {
            pedido.setStatus("PAGO");
            cliente.setCredito(cliente.getCredito() - pedido.getTotal());
        }
    }
}
```

  Problema: Se `Cliente` ou `Pedido` mudarem sua estrutura interna, `ProcessadorPedido` quebra.

    A Solução: Tell, Don't Ask

```java
// ✅ "Tell" - Baixo Acoplamento
public class Pedido {
    private double total;
    private Cliente cliente;
    private String status;
    
    public boolean podeSerFinalizado() {
        return this.total > 0 && 
               this.cliente.temCreditoSuficiente(this.total);
    }
    
    public void finalizar() {
        if (!podeSerFinalizado()) {
            throw new IllegalStateException(
                "Pedido não pode ser finalizado");
        }
        this.status = "PAGO";
        this.cliente.debitarCredito(this.total);
    }
}

public class ProcessadorPedido {
    public void processar(Pedido pedido) {
        pedido.finalizar(); // Simples e desacoplado!
    }
}
```

  Benefício: Mudanças em `Pedido` ou `Cliente` não afetam `ProcessadorPedido`.

Cada classe gerencia suas próprias responsabilidades.

   Law of Demeter (Princípio do Mínimo Conhecimento)

Evite cadeias longas de chamadas (também conhecido como "Train Wreck").

```java
// ❌ Violação - Conhecimento excessivo
double temp = proprietario.getCarro().getMotor().getVela().getTemperatura();

// ✅ Law of Demeter
double temp = proprietario.obterTemperaturaVela();

// Dentro de Proprietario:
public double obterTemperaturaVela() {
    return this.carro.getTemperaturaVela();
}
```



   Interfaces e Polimorfismo: Flexibilidade sem Caos

    • Nota Importante  
 • Este é um exemplo perfeito do Princípio Aberto-Fechado (OCP): aberto para extensão, fechado para modificação.

   Por Que Interfaces Importam

Imagine que sua empresa precisa adicionar um novo método de pagamento.

Pix, criptomoeda, carteira digital.

Com interfaces, você adiciona funcionalidade sem modificar código existente.

    Abstração: O 4º Pilar da OO

Antes de vermos as interfaces em ação, vamos entender a **Abstração**.

  Abstração significa expor apenas o essencial, escondendo a complexidade.

É como dirigir um carro: você usa o volante e os pedais sem precisar saber como o motor funciona.

Em Java, usamos  interfaces e classes abstratas para criar abstrações.

A interface `Pagavel` que veremos a seguir é um exemplo perfeito de abstração.

Ela define no que deve ser feito (processar pagamento), mas não **como** será feito.

  Definindo o Contrato

```java
public interface Pagavel {
    double getValorAPagar();
    void processar();
}
```

   Implementações Diversas

```java
public class Fatura implements Pagavel {
    private final double valor;

    public Fatura(double valor) { 
        this.valor = valor; 
    }

    @Override
    public double getValorAPagar() {
        return valor;
    }

    @Override
    public void processar() {
        System.out.println("Fatura de R$" + valor + " paga via boleto");
    }
}

public class Salario implements Pagavel {
    private final double valor;

    public Salario(double valor) { 
        this.valor = valor; 
    }

    @Override
    public double getValorAPagar() {
        return valor;
    }

    @Override
    public void processar() {
        System.out.println("Salário de R$" + valor + " pago via PIX");
    }
}
```

    Polimorfismo na Prática

```java
public class ProcessadorPagamento {
    // Aceita QUALQUER implementação de Pagavel
    public void processar(List<Pagavel> itens) {
        double total = 0;
        
        for (Pagavel item : itens) {
            item.processar(); // Comportamento diferente para cada tipo
            total += item.getValorAPagar();
        }
        
        System.out.println("Total processado: R$ " + total);
    }
    
    public static void main(String[] args) {
        List<Pagavel> pagamentos = List.of(
            new Fatura(150.0),
            new Salario(3000.0)
        );
        
        ProcessadorPagamento processador = new ProcessadorPagamento();
        processador.processar(pagamentos);
    }
}
```

  Benefício estratégico: Adicione novos tipos de pagamento criando novas classes.

Sem modificar `ProcessadorPagamento`.

Isso é o **Princípio Aberto-Fechado** em ação.



    Herança: Reutilização com Hierarquia

Herança permite que classes compartilhem atributos e métodos.

Promovendo reutilização de código através de uma relação "é um".

    Exemplo: Hierarquia de Veículos

```java
// Superclasse (Generalização)
public class Veiculo {
    protected int numRodas;
    private double velocidade;

    public Veiculo(int rodas) {
        this.numRodas = rodas;
        this.velocidade = 0.0;
    }

    public void acelerar() {
        this.velocidade += 10;
        System.out.println("Veículo acelerando... Velocidade: " + velocidade);
    }
    
    protected double getVelocidade() {
        return velocidade;
    }
}

// Subclasse (Especialização)
public class Carro extends Veiculo {
    private String modelo;
    
    public Carro(String modelo) {
        super(4); // Carros têm 4 rodas
        this.modelo = modelo;
    }

    // Sobreposição (Override)
    @Override
    public void acelerar() {
        super.acelerar(); // Chama comportamento da superclasse
        System.out.println("Carro " + modelo + " atingiu " + 
            getVelocidade() + " km/h");
    }
    
    public void mostrarRodas() {
        System.out.println("Este veículo tem " + this.numRodas + " rodas");
    }
}
```

    Uso Polimórfico e Princípio de Liskov

```java
public class Main {
    public static void main(String[] args) {
        Veiculo v1 = new Veiculo(2);
        Veiculo v2 = new Carro("Civic"); // Polimorfismo!
        
        v1.acelerar(); // Comportamento de Veiculo
        v2.acelerar(); // Comportamento de Carro (overridden)
    }
}
```

  Conceito-chave: O mesmo método `acelerar()` tem comportamentos diferentes dependendo do objeto real.

Isso é polimorfismo.

  Princípio de Substituição de Liskov: Para que a herança seja segura, toda subclasse deve poder ser substituída pela superclasse.

Sem quebrar o programa.

Esse é um dos princípios SOLID — garantindo que o Override mantém o contrato da superclasse.


    •Transição Importante  
 Agora que entendemos como estruturar o código com classes, objetos, encapsulamento e herança, vamos garantir que ele funcione corretamente.
 
 E que entregue o valor que o usuário espera.

 É aqui que entram o TDD e o BDD — metodologias que transformam boas ideias em software confiável.



    Desenvolvimento Orientado por Testes e Comportamento (TDD & BDD)

Se a Orientação a Objetos ensina como pensar em termos de abstrações, o TDD e o BDD ensinam como transformar esse pensamento em código confiável.

Código evolutivo e à prova de regressões.

Ambos são mais do que testes — são metodologias de design.

Colocam a qualidade no centro do processo de desenvolvimento.

   🔹 O Que é Desenvolvimento Orientado por Testes (TDD)?

O TDD (Test-Driven Development) é uma disciplina de desenvolvimento.

Você escreve o teste unitário ANTES do código de produção.

  Frase-chave: TDD testa unidades individuais de código (classes e métodos).

   O Ciclo do TDD: Red → Green → Refactor

O TDD não é um processo linear, mas um ciclo rigoroso de três etapas:

```
┌────────────┐     ┌────────────┐     ┌──────────────┐
│  Escreve   │     │ Implementa │     │  Refatora e  │
│  um Teste  │ ──▶ │ Código Mín │ ──▶ │ Melhora Código│
│ (RED)      │     │ (GREEN)    │     │ (REFACTOR)   │
└────────────┘     └────────────┘     └──────────────┘
        ▲                                       │
        └───────────────────────────────────────┘
```


| Etapa | Ação | Objetivo |
|-------|------|----------|
| **1. RED (Vermelho)** | Escrever um teste que falha | Pensar no comportamento desejado e definir a API antes de criá-la |
| **2. GREEN (Verde)** | Implementar código mínimo para fazer o teste passar | Fazer a funcionalidade funcionar |
| **3. REFACTOR (Refatorar)** | Melhorar o código mantendo todos os testes verdes | Garantir design de alta qualidade e conformidade com SOLID |


 Exemplo Prático: TDD em Java

Vamos desenvolver um serviço que calcula o preço final com imposto.

Ciclo 1: RED (Escrever Teste que Falha)

```java
// src/test/java/br/com/santosdev/TributoServiceTest.java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;
import java.math.BigDecimal;

public class TributoServiceTest {
    
    @Test
    void deveCalcularImpostoDezPorCento() {
        TributoService service = new TributoService();
        
        // Arrange: Valor base de 100.00
        BigDecimal valorBase = new BigDecimal("100.00");
        
        // Act: Espera 100 + 10% = 110.00
        BigDecimal valorFinal = service.calcularImposto(valorBase);
        
        // Assert
        assertEquals(new BigDecimal("110.00"), valorFinal);
    }
}
```

  Status: ❌ Teste FALHA (RED) — O método `calcularImposto` não existe ainda.

  Ciclo 2: GREEN (Fazer o Teste Passar)

```java
// src/main/java/br/com/santosdev/TributoService.java
import java.math.BigDecimal;

public class TributoService {
    
    public BigDecimal calcularImposto(BigDecimal valor) {
        // CÓDIGO MÍNIMO: Multiplica por 1.10
        return valor.multiply(new BigDecimal("1.10"));
    }
}
```

Status:  Teste PASSA (GREEN) — Funciona, mas o código tem "número mágico".

  Ciclo 3: REFACTOR (Melhorar sem Quebrar)

   • Objetivo do Refactor  
  Substituir o "Número Mágico" (1.10) pela constante `TAXA_IMPOSTO`.

 Isso melhora a legibilidade e aplica o Princípio da Responsabilidade Única (SRP).
 
 Se a taxa mudar, alteramos em um único lugar.

```java
// src/main/java/br/com/santosdev/TributoService.java (Refatorado)
import java.math.BigDecimal;

public class TributoService {
    private static final BigDecimal TAXA_IMPOSTO = new BigDecimal("0.10");
    
    public BigDecimal calcularImposto(BigDecimal valor) {
        // Valor final = valor * (1 + TAXA_IMPOSTO)
        return valor.multiply(BigDecimal.ONE.add(TAXA_IMPOSTO));
    }
}
```

  Status:  Teste continua VERDE — Código agora é limpo e manutenível.

  O poder da Refatoração: A refatoração foi feita com segurança total.

Se algo quebrasse, o teste imediatamente falharia (RED), alertando o desenvolvedor.

   O Chapéu do TDD (George Dinwiddie)

George Dinwiddie compara o TDD a usar dois "chapéus":

- Chapéu do Programador: Foca em fazer o teste passar (GREEN)

- Chapéu do Refatorador: Foca em melhorar o design (REFACTOR)

Essa metáfora reforça que o TDD é uma disciplina de equilíbrio entre produtividade e qualidade.

•  [Leia o artigo original](https://blog.gdinwiddie.com/2012/12/26/tdd-hat/)



 🔹 O Que é Desenvolvimento Orientado por Comportamento (BDD)?

O BDD (Behavior-Driven Development) é uma evolução do TDD.

Foca na validação do comportamento do sistema a partir da perspectiva do 
usuário de negócio.

 Frase-chave: BDD testa **como as unidades funcionam juntas** para entregar valor.

 Fluxo BDD e Linguagem Gherkin

O BDD usa a sintaxe Gherkin com os termos Dado, Quando, Então.

Para escrever cenários de teste em linguagem natural.


| Sintaxe | Tradução de Negócio | Foco |
|---------|---------------------|------|
| **GIVEN (Dado)** | O estado inicial do sistema | Contexto: Quais dados existem antes da ação |
| **WHEN (Quando)** | A ação que o usuário realiza | Evento: A interação |
| **THEN (Então)** | O resultado esperado | Comportamento: A mudança de estado ou resposta |


   Exemplo Prático: BDD para API Bancária

  1. Cenário Gherkin (Arquivo .feature)

```gherkin
# src/test/resources/features/conta_bancaria.feature
Funcionalidade: Gestão de Contas Bancárias

  Cenário: Tentativa de Criar Conta com Saldo Negativo
    Dado que o endpoint de criação está disponível
    Quando eu envio uma requisição POST para /api/contas com:
      | titular    | saldo   |
      | Infrator   | -100.00 |
    Então o código de resposta deve ser 400
    E a mensagem de erro deve conter "saldo não pode ser negativo"
  
  Cenário: Saque com Saldo Insuficiente
    Dado que existe uma conta com saldo de R$ 50,00
    Quando eu tento sacar R$ 100,00
    Então o sistema deve responder com erro 400
    E a mensagem "Saldo insuficiente" deve ser exibida
```

Por que isso é poderoso:  

Este cenário BDD espelha a linguagem de negócio.

"O cliente não pode sacar mais do que possui."  

A comunicação é clara para desenvolvedores, analistas e gestores.

  Eliminando ambiguidades.

   2. Implementação das Etapas (Step Definitions - Java)

```java
// src/test/java/br/com/santosdev/steps/ContaBancariaSteps.java
import io.cucumber.java.pt.*;
import io.restassured.RestAssured;
import io.restassured.response.Response;
import static org.junit.jupiter.api.Assertions.*;

public class ContaBancariaSteps {
    
    private Response ultimaResposta;
    
    @Dado("que o endpoint de criação está disponível")
    public void endpoint_disponivel() {
        RestAssured.baseURI = "http://localhost:8080";
    }
    
    @Quando("eu envio uma requisição POST para /api/contas com:")
    public void envio_post_contas(io.cucumber.datatable.DataTable dados) {
        Map<String, String> conta = dados.asMaps().get(0);
        
        ultimaResposta = RestAssured
            .given()
                .auth().basic("user", "password")
                .contentType("application/json")
                .body(conta)
            .when()
                .post("/api/contas");
    }
    
    @Então("o código de resposta deve ser {int}")
    public void codigo_resposta(int codigoEsperado) {
        assertEquals(codigoEsperado, ultimaResposta
getStatusCode());
    }
    
    @Então("a mensagem de erro deve conter {string}")
    public void mensagem_erro_contem(String textoEsperado) {
        String corpo = ultimaResposta.getBody().asString();
        assertTrue(corpo.contains(textoEsperado));
    }
}
```

    Comparativo: TDD vs. BDD

| Aspecto | TDD (Foco Unitário) | BDD (Foco Comportamento) |
|---------|---------------------|--------------------------|
| **Nível de Teste** | Unidade (classe/método) | Integração/Sistema (API completa) |
| **Linguagem** | Código Java/JUnit | Gherkin (linguagem natural) |
| **Quem Escreve** | Desenvolvedor | Desenvolvedor + Analista + PO |
| **Design de Código** | Força design simples e testável | Guia arquitetura para satisfazer negócio |
| **Documentação** | Testes = documentação técnica | Cenários = documentação de requisitos |
| **Regressão** | Garante que código não quebra | Garante que valor de negócio é entregue |
| **Ferramenta (Java)** | JUnit, Mockito | Cucumber, RestAssured, Selenium |
| **Exemplo** | `ContaBancariaTest.java` | `conta_bancaria.feature` |


 Ambos são essenciais:

 • TDD é a rede de segurança do desenvolvedor no nível da unidade de código

• BDD é a garantia de qualidade no nível da funcionalidade do usuário

   Na Prática: Projeto javaNaPraticaPOO

O projeto [**javaNaPraticaPOO**](https://github.com/Santosdevbjj/javaNaPraticaPOO) aplica ambos os conceitos:


| Conceito | Implementação no Projeto |
|----------|--------------------------|
| **TDD** | `ContaBancariaTest.java` — Testes unitários com JUnit e Mockito |
| **BDD** | `ContaBancariaSteps.java` — Testes de sistema com Cucumber e RestAssured |
| **Integração** | Docker Compose orquestra App + MySQL + RabbitMQ |
| **Segurança** | Spring Security valida autenticação nos testes BDD |
| **Validação** | Bean Validation testada via BDD (cenário de saldo negativo) |


  Essa combinação garante qualidade técnica E valor de negócio.

    Valor dos Casos de Teste na Engenharia de Software

| Finalidade | Explicação |
|------------|------------|
| **Garantir o Contrato** | O teste define o contrato público da classe ou sistema |
| **Facilitar Refatoração** | Testes automatizados dão confiança para mudar código |
| **Documentar Intenção** | Um bom teste explica o que o código faz e por quê |
| **Prevenir Regressão** | Detecta quando novas mudanças quebram funcionalidades antigas |


  O valor se manifesta em:


• Redução de custos de manutenção  
• Tempo de deploy mais rápido  
• Aumento da confiança da equipe  
• Código documentado por si mesmo  
•  Sistema que entrega valor real ao usuário

 Refatoração com SOLID: SRP (Single Responsibility Principle)

**Problema sem SRP:**

```java
// ❌ Classe faz TUDO: validação + persistência + notificação
public class ContaBancariaService {
    public void criar(ContaBancaria conta) {
        // Validação
        if (conta.getSaldo() < 0) throw new Exception();
        
        // Persistência
        entityManager.persist(conta);
        
        // Notificação
        rabbitTemplate.send("fila", conta);
    }
}
```

  Solução com SRP (após refatoração TDD):

```java
// ✅ Cada classe tem UMA responsabilidade

// 1. Validação
public class ContaBancariaValidator {
    public void validar(ContaBancaria conta) {
        if (conta.getSaldo() < 0) {
            throw new IllegalArgumentException("Saldo não pode ser negativo");
        }
    }
}

// 2. Persistência
public class ContaBancariaDAO extends JpaRepository<ContaBancaria, Long> {
    // Spring Data gera automaticamente
}

// 3. Notificação
public class NotificacaoService {
    public void notificar(ContaBancaria conta) {
        rabbitTemplate.send("fila-notificacoes", conta);
    }
}

// 4. Orquestração
public class ContaBancariaService {
    private ContaBancariaValidator validator;
    private ContaBancariaDAO dao;
    private NotificacaoService notificacao;
    
    public void criar(ContaBancaria conta) {
        validator.validar(conta);
        dao.save(conta);
        notificacao.notificar(conta);
    }
}
```

  Benefícios:

• Cada classe é **facilmente testável** isoladamente (TDD)
• Mudanças em validação **não afetam** persistência
• Código **mais fácil de evoluir**

  Ferramentas para TDD e BDD em Java

TDD (Teste Unitário):
​JUnit 5
​Função: Framework padrão para criação e execução de testes unitários e de integração.
​Exemplo: Usa anotações como @Test e @BeforeEach para definir o ciclo de vida dos testes.
​Mockito
​Função: Criação de objetos mock (simulados) para isolar a classe em teste de suas dependências.
​Exemplo: Usa @Mock para criar o objeto mock e when().thenReturn() para definir seu comportamento.
​AssertJ
​Função: Biblioteca que fornece asserções (verificações) ricas, fluentes e mais legíveis.
​Exemplo: assertThat(valor).isEqualTo(100) ou assertThat(lista).containsExactly("a", "b").
​JaCoCo
​Função: Ferramenta de cobertura de código que mede o quanto do seu código de aplicação foi exercido pelos testes.
​Exemplo: Gera um relatório HTML ou XML com a porcentagem de linhas de código testadas.


BDD (Teste de Comportamento):

| Ferramenta | Função | Exemplo |
|------------|--------|---------|
| **Cucumber** | Framework BDD | Executa arquivos `.feature` |
| **RestAssured** | Testes de API REST | `given().when().then()` |
| **Selenium** | Testes de UI web | Automação de navegadores |



  Mensagem Final sobre TDD & BDD

Em projetos modernos, o TDD e o BDD não são apenas ferramentas. São compromissos com a qualidade.

Eles fazem o desenvolvedor pensar antes de codar. Garantem que cada linha entregue valor real.

No fim, o código não é apenas funcional.
É confiável, sustentável e documentado por si mesmo.

• TDD garante que o código funciona. 
• BDD garante que o código entrega valor. 
• Juntos, eles constroem software de classe mundial.


 Exceções e Programação Defensiva

    Tratamento Robusto de Erros

Java fornece mecanismos robustos de tratamento de exceções.

Eles separam lógica de negócio do tratamento de erros.

```java
public class Calculadora {
    public double dividir(double a, double b) {
        if (b == 0) {
            throw new ArithmeticException("Divisão por zero não é permitida");
        }
        return a / b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculadora calc = new Calculadora();
        
        try {
            double resultado = calc.dividir(10, 0);
            System.out.println("Resultado: " + resultado);
        } catch (ArithmeticException e) {
            System.err.println("Erro: " + e.getMessage());
            // O programa continua executando normalmente
        }
        
        System.out.println("Programa finalizado com sucesso");
    }
}
```

   Optional: Eliminando NullPointerException

 •  Dica Profissional  
  Sempre use BigDecimal para cálculos financeiros. O tipo double pode causar erros de precisão.

`NullPointerException` representa cerca de 70% dos erros em produção em projetos Java.

`Optional<T>` elimina essa classe inteira de bugs.

```java
public class RepositorioClientes {
    public Optional<Cliente> buscarPorCPF(String cpf) {
        Cliente cliente = bancoDeDados.consultar(cpf);
        return Optional.ofNullable(cliente); // Nunca retorna null!
    }
}

// Consumo seguro e elegante
repositorio.buscarPorCPF("12345678900")
    .filter(c -> c.getIdade() >= 18)
    .map(c -> c.getNome().toUpperCase())
    .ifPresentOrElse(
        nome -> System.out.println("Cliente encontrado: " + nome),
        () -> System.out.println("Cliente não encontrado ou menor de idade")
    );
```

  Sem Optional (código frágil):

```java
Cliente cliente = repositorio.buscar("12345678900");
if (cliente != null && cliente.getIdade() >= 18) {
    String nome = cliente.getNome();
    if (nome != null) {
        System.out.println(nome.toUpperCase());
    }
}
```

    Quando Ser Defensivo

Aplique programação defensiva nas  fronteiras do sistema:

•  Entrada de dados do usuário
•  APIs públicas
•  Comunicação com sistemas externos

Confie em dados já validados:

- ❌ Não revalide em métodos `private` internos
- ❌ Não valide após testes unitários já garantirem validade



     Atributos e Métodos Estáticos

Membros `static` pertencem à classe, não a instâncias individuais.

```java
public class Carro {
    // Atributo Estático: compartilhado por TODOS os carros
    public static final int NUMERO_RODAS = 4;
    private static int totalCarrosCriados = 0;
    
    // Atributo de Instância: específico de cada carro
    private String cor;
    
    public Carro(String cor) {
        this.cor = cor;
        totalCarrosCriados++; // Incrementa contador compartilhado
    }
    
    // Método Estático: chamado na classe, não no objeto
    public static int getTotalCarros() {
        return totalCarrosCriados;
        // Não pode acessar 'cor' aqui (é de instância)
    }
    
    // Método de Instância: precisa de um objeto
    public void mostrarCor() {
        System.out.println("Cor: " + this.cor);
        System.out.println("Rodas: " + NUMERO_RODAS); // Pode acessar static
    }
}

// Uso:
System.out.println("Rodas: " + Carro.NUMERO_RODAS); // Acesso pela classe
System.out.println("Total: " + Carro.getTotalCarros());

Carro c1 = new Carro("Azul");
Carro c2 = new Carro("Vermelho");
c1.mostrarCor(); // Acesso pelo objeto
System.out.println("Total: " + Carro.getTotalCarros()); // Resultado: 2
```



    Erros Comuns ao Aprender POO

Ao longo da jornada de aprendizado, desenvolvedores frequentemente cometem erros que comprometem a qualidade do código.

Reconhecer esses erros é o primeiro passo para evitá-los:

    1. Tratar Classes como Scripts Procedurais

 ❌ Erro:
```java
public class ProcessadorPedido {
    public void processar() {
        // Lógica procedural sem objetos colaborando
        double valor = 100;
        double imposto = valor * 0.1;
        double total = valor + imposto;
        System.out.println(total);
    }
}
```

• Solução:
```java
public class Pedido {
    private BigDecimal valor;
    
    public BigDecimal calcularTotal() {
        return valor.add(calcularImposto());
    }
    
    private BigDecimal calcularImposto() {
        return valor.multiply(new BigDecimal("0.1"));
    }
}
```

 2. Expor Atributos sem Encapsulamento

 ❌ Erro:
```java
public class ContaBancaria {
    public double saldo; // Qualquer um pode modificar!
}
```

  • Solução:
```java
public class ContaBancaria {
    private double saldo;
    
    public void depositar(double valor) {
        if (valor > 0) {
            this.saldo += valor;
        }
    }
}
```

   3. Testar Manualmente em Vez de Automatizar com TDD

❌ Erro: Executar o programa repetidamente para verificar se funciona.

•  Solução:Escrever testes automatizados que validam o comportamento.

```java
@Test
void deveDepositarValorPositivo() {
    ContaBancaria conta = new ContaBancaria(100);
    conta.depositar(50);
    assertEquals(150, conta.getSaldo());
}
```

 4. Ignorar Comportamento de Negócio ao Projetar

  ❌ Erro: Criar classes apenas como "sacos de dados" (DTOs sem comportamento).

 •  Solução: Usar BDD para mapear regras de negócio em comportamentos testáveis.

```gherkin
Cenário: Cliente tenta sacar mais que o saldo disponível
  Dado que existe uma conta com saldo de R$ 100
  Quando o cliente tenta sacar R$ 150
  Então o sistema deve retornar erro "Saldo insuficiente"
```

 5. Criar Hierarquias de Herança Profundas Desnecessárias

❌ Erro: `Animal -> Mamifero -> Felino -> Gato -> GatoPersa`

•  Solução: Preferir composição e interfaces quando apropriado.

```java
public class Gato implements Animal, Domesticavel {
    private Comportamento comportamento;
    // Composição em vez de herança profunda
}
```



   Todo Este Conhecimento em Código Funcional

Transformei todos os conceitos deste artigo em um projeto completo e funcional:

• Repositório: 
https://github.com/Santosdevbjj/javaNaPraticaPOO



     O Que Você Encontra no Projeto

• Microsserviço completo com Spring Boot + MySQL + RabbitMQ 

• Arquitetura em camadas (Model/DAO/Service/Controller)  

•  Encapsulamento e validações com Bean Validation 

• PreparedStatement via Spring Data JPA (proteção contra SQL Injection)  

•  Testes TDD com JUnit 5 e Mockito  

• Testes BDD com Cucumber e RestAssured  

•  Spring Security com autenticação Basic Auth  

•  Docker Compose para execução com um comando  

•  BigDecimal para precisão financeira  

• Mensageria assíncrona com RabbitMQ  

•  3 manuais completos (README + Técnico + Leigo)  



### 🔗 Conectando Artigo e Código

| Conceito do Artigo | Implementação no Código | Arquivo |
|--------------------|-------------------------|---------|
| **Encapsulamento** | Atributos `private` + validações com Bean Validation | `ContaBancaria.java` |
| **Tell, Don't Ask** | Service encapsula lógica, Controller apenas delega | `ContaBancariaService.java` |
| **Separação de Responsabilidades** | DAO (persistência) / Service (negócio) / Controller (API) | Arquitetura completa |
| **Programação Defensiva** | Validações em múltiplas camadas + `GlobalExceptionHandler` | Todo o projeto |
| **TDD** | Testes unitários com cobertura ampla | `ContaBancariaTest.java` |
| **BDD** | Cenários Gherkin testando API completa | `conta_bancaria.feature` |
| **Interfaces e Polimorfismo** | `JpaRepository` implementado pelo Spring Data | `ContaBancariaDAO.java` |
| **Exceções Customizadas** | Tratamento profissional de erros 400/404 | `GlobalExceptionHandler.java` |
| **BigDecimal** | Precisão financeira (nenhum erro de ponto flutuante) | `ContaBancaria.java` |
| **Mensageria Assíncrona** | Desacoplamento via RabbitMQ | `NotificacaoService.java` |





  Execute em 3 Passos

```bash
# 1. Clone o repositório
git clone https://github.com/Santosdevbjj/javaNaPraticaPOO.git
cd javaNaPraticaPOO

# 2. Inicie a stack completa (App + MySQL + RabbitMQ)
docker-compose up --build -d

# 3. Teste a API
# Aguarde 30s e acesse: http://localhost:8080/actuator/health
# Importe a coleção Postman: api-tests/javaNaPraticaPOO-Collection.json
```

 Explore o código, experimente modificações e veja os fundamentos ganhando vida!



   Arquitetura do Sistema

```
┌─────────────────────────────────────────────────────┐
│                Cliente (Postman/Browser)             │
└─────────────────────┬───────────────────────────────┘
                      │ HTTP REST (Basic Auth)
                      ↓
┌─────────────────────────────────────────────────────┐
│         Spring Boot Application (Port 8080)         │
│                                                      │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────┐  │
│  │ Controller   │→ │  Service     │→ │   DAO    │  │
│  │ (REST API)   │  │ (Negócio)    │  │ (JPA)    │  │
│  └──────────────┘  └──────┬───────┘  └────┬─────┘  │
│                           │                │        │
│                           ↓                ↓        │
│                    ┌──────────────┐  ┌──────────┐  │
│                    │  RabbitMQ    │  │  MySQL   │  │
│                    │  Producer    │  │  Client  │  │
│                    └──────┬───────┘  └────┬─────┘  │
└───────────────────────────┼──────────────┼────────┘
                            │              │
                            ↓              ↓
              ┌─────────────────┐  ┌──────────────┐
              │   RabbitMQ      │  │    MySQL     │
              │   (Port 5672)   │  │  (Port 3306) │
              │   (Port 15672)  │  │              │
              └─────────────────┘  └──────────────┘
```



   Fluxo de uma requisição:

1. Cliente envia `POST /api/contas` com Basic Auth

2. `SecurityConfig` valida credenciais (user/password)

3. `ContaBancariaController` recebe e valida payload (Bean Validation)

4. `ContaBancariaService` aplica regras de negócio

5. `ContaBancariaDAO` persiste no MySQL via JPA

6. `NotificacaoService` envia mensagem assíncrona para RabbitMQ

7. Resposta HTTP 201 (Created) retorna ao cliente


 Princípios OO Aplicados:

- Encapsulamento: Cada camada esconde detalhes internos

- Separação de
Responsabilidades Controller ≠ Service ≠ DAO

- Baixo Acoplamento: Service não conhece detalhes de HTTP ou SQL

-  Colaboração: RabbitMQ permite comunicação assíncrona desacoplada



 Visão de Futuro

Os fundamentos que você aprendeu neste artigo são apenas o começo de uma jornada fascinante.

A engenharia de software moderna em Java possui ainda mais padrões e práticas avançadas.

Nos próximos artigos, exploraremos:

- Padrões de Projeto (Design Patterns): Strategy, Factory, Observer, Singleton e como aplicá-los em situações reais

- Arquitetura Limpa (Clean Architecture): Estruturando aplicações escaláveis e independentes de frameworks

- Microserviços Avançados: Service Discovery, Circuit Breaker, API Gateway

- Programação Reativa: Spring WebFlux e programação assíncrona não-bloqueante

- Domain-Driven Design (DDD): Modelagem rica de domínio com Aggregates, Value Objects e Bounded Contexts


Fique atento para dominar completamente a engenharia de software moderna em Java!




   Conclusão

Os Fundamentos de Java são muito mais do que sintaxe.

Eles ensinam a modelar problemas, projetar sistemas claros e escrever código profissional.

Dominar conceitos como classes, encapsulamento, interfaces, herança, testes (TDD e BDD) e programação defensiva é dominar o "como pensar" em Java.

E isso separa quem escreve código de quem constrói soluções escaláveis.

Soluções que resistem ao tempo e à mudança.

Quando você aplica encapsulamento, evita bugs de milhões de reais.

Quando usa interfaces, prepara seu sistema para evolução sem quebrar código existente.

Quando pratica TDD, garante que cada linha funciona corretamente.

Quando implementa BDD, assegura que o sistema entrega valor real ao usuário final.

Quando escreve testes, dorme tranquilo sabendo que mudanças não causarão regressões silenciosas.

Esses princípios não são teoria acadêmica.

São as ferramentas que empresas como Google, Amazon e Nubank usam para construir sistemas.

Sistemas que atendem milhões de usuários diariamente.

O aprendizado contínuo desses fundamentos é o que transforma desenvolvedores iniciantes.

Em engenheiros de software respeitados e bem remunerados.

  TDD + BDD + SOLID + Orientação a Objetos = Software de Classe Mundial.



  Desafio para Você

Escolha UMA classe do seu projeto atual e responda estas perguntas:

1. Ela protege seu estado interno? (Encapsulamento)

2. Ela faz apenas uma coisa bem feita? (Responsabilidade única - SRP)

3. Outras classes precisam conhecer seus detalhes internos? (Acoplamento)

4. Você consegue testá-la facilmente com TDD? (Testabilidade)

5. O comportamento dela está documentado via BDD? (Valor de negócio)

Se respondeu "não" para qualquer pergunta, você tem uma oportunidade de refatoração.

Uma refatoração que vai melhorar significativamente a qualidade do seu código.

Compartilhe nos comentários:

- Qual princípio de OO você vai aplicar esta semana? 

- Você já pratica TDD? Se não, qual será seu primeiro teste?

- Como você documenta os requisitos de negócio no seu projeto?

Vamos aprender juntos! 

Se este conteúdo te ajudou, curta e compartilhe para fortalecer a comunidade Java. 

  Clone o projeto, experimente o código e veja os fundamentos ganhando vida:  

 • Repositório no GitHub: com o código do microsserviço Spring Boot/Docker:
https://github.com/Santosdevbjj/javaNaPraticaPOO




     Referências Bibliográficas:

Statista (2024). Most used programming languages among developers worldwide. Disponível em: https://www.statista.com/statistics/793628/worldwide-developer-survey-most-used-languages/. Acesso em: out. 2025.

Oracle. Java SE 17 Documentation. Disponível em: https://docs.oracle.com/en/java/javase/17/. Acesso em: out. 2025.

Oracle. Java SE 17 - Optional API Documentation. Disponível em: https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html. Acesso em: out. 2025.

Oracle. Java SE 17 - BigDecimal API Documentation. Disponível em: https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/math/BigDecimal.html. Acesso em: out. 2025.

Dev.java. Plataforma oficial para desenvolvedores Java. Disponível em: https://dev.java/. Acesso em: out. 2025.

Bloch, Joshua. Effective Java. 3rd ed. Addison-Wesley Professional, 2018.

Beck, Kent. Test-Driven Development: By Example. Addison-Wesley Professional, 2002.

North, Dan. Introducing BDD. Better Software Magazine, 2006.

JUnit Team. JUnit 5 User Guide. Disponível em: https://junit.org/junit5/docs/current/user-guide/. Acesso em: out. 2025.

Cucumber. Cucumber Documentation. Disponível em: https://cucumber.io/docs/cucumber/. Acesso em: out. 2025.

Martin, Robert C. Clean Code: A Handbook of Agile Software Craftsmanship. Prentice Hall, 2008.

Fowler, Martin. Refactoring: Improving the Design of Existing Code. 2nd ed. Addison-Wesley Professional, 2018.

Gamma, Erich; Helm, Richard; Johnson, Ralph; Vlissides, John. Design Patterns: Elements of Reusable Object-Oriented Software. Addison-Wesley Professional, 1994.

Dinwiddie, George. The TDD Hat. Blog post. Disponível em: https://blog.gdinwiddie.com/2012/12/26/tdd-hat/. Acesso em: out. 2025.

Stack Overflow. Developer Survey 2024. Disponível em: https://stackoverflow.com/. Acesso em: out. 2025.

Oracle. The Java Tutorials - Object-Oriented Programming Concepts. Disponível em: https://docs.oracle.com/javase/tutorial/java/concepts/. Acesso em: out. 2025.

Spring Framework. Spring Boot Documentation. Disponível em: https://spring.io/projects/spring-boot. Acesso em: out. 2025.







