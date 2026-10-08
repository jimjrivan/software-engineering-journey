# 003 — Coesão e Acoplamento

## 1. Objetivo

Aprofundar os conceitos de coesão e acoplamento e entender como eles influenciam a separação de responsabilidades e o design de software.

O objetivo não é apenas conhecer as definições, mas conseguir identificar esses aspectos ao analisar uma solução e utilizá-los como critérios para tomar decisões de design.

## 2. Coesão

Coesão representa o quanto as responsabilidades existentes dentro de um componente estão relacionadas entre si.

Uma boa estrutura busca **alta coesão**, mantendo juntas responsabilidades que realmente pertencem ao mesmo contexto.

Por exemplo, uma classe responsável por pedidos pode conter regras relacionadas ao ciclo de vida e às regras de um pedido, mas não deveria assumir diretamente responsabilidades próprias de pagamento, estoque, envio de e-mails ou emissão de notas fiscais.

Uma responsabilidade pode depender de outra sem precisar ser responsável por implementá-la.

## 3. Acoplamento

Acoplamento representa o grau de dependência entre componentes.

Uma boa estrutura busca **baixo acoplamento**, evitando que um componente conheça detalhes desnecessários de outros componentes ou de suas implementações.

Baixo acoplamento não significa ausência de dependências.

Um componente pode depender de outro para realizar uma determinada capacidade. O objetivo é controlar essa dependência e evitar que detalhes de implementação vazem para quem apenas precisa utilizar a capacidade.

## 4. Alta coesão e baixo acoplamento

Um dos objetivos fundamentais do design de software é buscar:

**Alta coesão + baixo acoplamento**

Isso significa que cada componente deve possuir responsabilidades relacionadas entre si, enquanto suas dependências externas devem ser bem definidas e controladas.

Separar uma classe grande em várias classes pode aumentar a coesão, mas isso, por si só, não garante baixo acoplamento.

É necessário também analisar como essas classes se comunicam e quais conhecimentos cada uma possui sobre as outras.

## 5. Exemplo analisado

Foi analisada uma `OrderService` que realizava diversas atividades:

* validação do pedido;
* cálculo do total;
* persistência no banco;
* consulta de estoque;
* processamento de pagamento;
* envio de e-mail;
* publicação de evento.

Inicialmente, considerei que o fato de as dependências serem recebidas por injeção seria suficiente para caracterizar baixo acoplamento.

Durante a análise, percebi que isso não é necessariamente verdade.

Uma classe pode utilizar Dependency Injection e ainda permanecer fortemente acoplada a detalhes concretos de infraestrutura.

Por exemplo:

```csharp
SqlConnection
SmtpClient
HttpClient
```

continuam sendo detalhes concretos conhecidos pela `OrderService`.

Além disso, quando a própria `OrderService` conhece SQL, URLs de APIs, SMTP e detalhes de comunicação, responsabilidades diferentes estão misturadas.

## 6. Separação de responsabilidades

Uma solução melhor é fazer com que a `OrderService` coordene o caso de uso sem conhecer os detalhes de implementação das responsabilidades externas.

Por exemplo:

```text
OrderService
    |
    +-- IOrderRepository
    +-- IStockService
    +-- IPaymentService
    +-- INotificationService
    +-- IEventPublisher
```

Nesse modelo, `OrderService` sabe quais capacidades precisa utilizar, mas não precisa saber como elas são implementadas.

O pagamento, por exemplo, pode ser realizado por HTTP, gRPC, RabbitMQ ou por outro gateway sem que a `OrderService` precise conhecer esses detalhes.

## 7. Abstrações e contratos

Uma interface pode representar uma capacidade necessária ao sistema.

Por exemplo:

```csharp
public interface IPaymentService
{
    Task<PaymentResult> ProcessAsync(PaymentRequest request);
}
```

A `OrderService` depende do contrato:

```text
OrderService
      |
      v
IPaymentService
```

Enquanto diferentes implementações podem fornecer essa capacidade:

```text
              IPaymentService
                     ^
                     |
        +------------+------------+
        |            |            |
        v            v            v
   PaymentHttp   PaymentGrpc   PaymentRabbitMQ
```

Dessa forma, a `OrderService` não precisa conhecer o mecanismo utilizado para realizar o pagamento.

## 8. Dependency Injection e Dependency Inversion

Também foi reforçada a diferença entre Dependency Injection e Dependency Inversion.

**Dependency Injection** é uma técnica utilizada para fornecer dependências a um componente.

**Dependency Inversion Principle** está relacionado à forma como as dependências são estruturadas: componentes de alto nível não devem depender diretamente de detalhes de baixo nível.

Uma configuração de DI pode definir, por exemplo:

```csharp
services.AddScoped<IPaymentService, PaymentService>();
```

Nesse cenário:

* a arquitetura define que `OrderService` depende de `IPaymentService`;
* a configuração define qual implementação atende esse contrato;
* o container de DI realiza a composição e fornece a implementação.

## 9. Principal aprendizado

Dividir uma classe grande em várias classes não é suficiente para criar uma boa arquitetura.

É necessário:

1. identificar responsabilidades;
2. manter responsabilidades relacionadas juntas;
3. evitar responsabilidades que não pertencem ao componente;
4. identificar as dependências necessárias;
5. controlar essas dependências;
6. utilizar abstrações quando fizer sentido;
7. manter detalhes de implementação separados das responsabilidades que apenas precisam utilizá-los.

A ideia que melhor resume o aprendizado desta etapa é:

> **Modularizar não é simplesmente dividir código; é criar fronteiras de responsabilidade e controlar as dependências entre essas fronteiras.**

## 10. Relação com a próxima etapa

O estudo de coesão e acoplamento mostrou que princípios de design não devem ser tratados isoladamente.

A busca por alta coesão e baixo acoplamento leva naturalmente a conceitos como:

* responsabilidade única;
* abstração;
* Dependency Inversion;
* Dependency Injection;
* separação entre domínio, aplicação e infraestrutura.

O próximo passo da jornada será aprofundar **SOLID**, começando pelo **Single Responsibility Principle (SRP)**.
