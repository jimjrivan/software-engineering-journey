# 002 — Skills Map

## 1. Objetivo

O objetivo desta etapa foi construir um mapa das minhas competências atuais em Engenharia de Software e Arquitetura de Sistemas.

Em vez de utilizar apenas uma autoavaliação, o diagnóstico foi baseado em situações práticas de arquitetura, desenvolvimento e sistemas distribuídos.

A intenção foi identificar não apenas o que conheço, mas principalmente a diferença entre:

* conhecimentos que já utilizo com segurança na prática;
* conhecimentos que utilizo, mas preciso formalizar;
* conceitos que ainda precisam ser aprofundados.

---

## 2. Resultado geral

O diagnóstico mostrou que minha experiência prática é mais ampla do que a minha familiaridade com a terminologia formal pode indicar.

Em diversas situações consegui chegar intuitivamente a soluções relacionadas a:

* modularização;
* coesão e acoplamento;
* requisitos não funcionais;
* escalabilidade;
* mensageria;
* Outbox Pattern;
* idempotência;
* retry;
* DLQ;
* processamento assíncrono;
* APIs;
* bancos de dados;
* cloud;
* disponibilidade;
* observabilidade;
* sistemas distribuídos.

O principal gap identificado não é necessariamente a ausência de experiência prática, mas a necessidade de estruturar e formalizar esse conhecimento.

---

## 3. Competências identificadas como fortes

### Desenvolvimento de Software

Tenho experiência prática consolidada no desenvolvimento de sistemas corporativos e na transformação de requisitos em soluções de software.

### Linguagens

Possuo experiência prática com:

* C# / .NET;
* Java / Spring Boot;
* Python;
* JavaScript / TypeScript.

O objetivo desta jornada é aumentar a fluência e aprofundar fundamentos e boas práticas nessas linguagens.

### Bancos de dados

Possuo experiência prática com bancos relacionais e não relacionais, incluindo:

* Oracle;
* SQL Server;
* PostgreSQL;
* MySQL;
* MongoDB.

Também demonstrei familiaridade com preocupações relacionadas a índices, volume, particionamento e desempenho.

### APIs

Possuo experiência prática com APIs e com decisões relacionadas a comunicação síncrona e assíncrona.

### Mensageria

Demonstrei conhecimento prático de conceitos como:

* RabbitMQ;
* filas;
* ACK;
* redelivery;
* retry;
* DLQ;
* processamento assíncrono.

### Outbox Pattern

Consegui identificar o problema de dual-write em um cenário envolvendo banco de dados e RabbitMQ e aplicar o Outbox Pattern como solução.

A conclusão formalizada foi:

```text
Transação do banco
    ├── alteração do domínio
    └── registro do evento na Outbox

Depois da transação:

Outbox Publisher
    ↓
RabbitMQ
```

Também foi identificado que a publicação pode gerar duplicidade e, portanto, o consumidor precisa considerar idempotência.

### Idempotência

Demonstrei capacidade de identificar cenários de duplicidade tanto em mensagens quanto em APIs.

Para APIs, reconheci a necessidade de utilizar uma chave de idempotência e manter o estado da operação de forma persistente.

### Sistemas distribuídos

Demonstrei familiaridade prática com problemas relacionados a:

* falhas parciais;
* timeouts;
* duplicidade;
* consistência;
* processamento assíncrono;
* indisponibilidade de dependências externas;
* retries;
* DLQ;
* intervenção manual.

Um ponto importante identificado foi:

> Timeout não significa necessariamente que a operação falhou.

Em uma integração externa, a operação pode ter sido processada mesmo que a resposta não tenha chegado ao sistema solicitante.

---

## 4. Requisitos não funcionais

O diagnóstico mostrou que já utilizo diversos requisitos não funcionais na análise de problemas, mesmo sem sempre utilizar formalmente essa terminologia.

Entre eles:

* volume;
* picos;
* latência;
* disponibilidade;
* performance;
* consistência;
* segurança;
* escalabilidade;
* processamento síncrono ou assíncrono.

Um aprendizado importante foi perceber que esses requisitos devem ser identificados antes da escolha de uma arquitetura ou tecnologia.

---

## 5. Coesão e acoplamento

Foi identificado conhecimento prático sobre modularização e separação de responsabilidades.

Um dos principais pontos de formalização foi:

> **Alta coesão + baixo acoplamento**

Também foi reforçado que simplesmente dividir uma classe grande em várias classes não garante baixo acoplamento.

É necessário criar fronteiras de responsabilidade e controlar as dependências entre essas fronteiras.

---

## 6. SOLID e Design de Software

Foi identificado conhecimento prático, porém com necessidade de formalização em alguns conceitos.

### SRP

O conceito de responsabilidade única já era utilizado intuitivamente.

Foi reconhecido que uma classe que possui diferentes razões independentes para mudança apresenta um problema de design.

### ISP

Foi identificada inicialmente uma interpretação incorreta relacionada à necessidade de interfaces.

O conceito foi posteriormente diferenciado:

> Interface Segregation Principle significa que clientes não devem ser forçados a depender de métodos que não utilizam.

### DIP e DI

Foi identificado inicialmente que Dependency Injection fazia parte diretamente de SOLID.

A distinção foi formalizada:

* **Dependency Inversion Principle (DIP)** é um princípio de design;
* **Dependency Injection (DI)** é uma técnica utilizada para fornecer dependências e pode ajudar a implementar DIP.

Esse é um dos pontos que será aprofundado durante a jornada.

---

## 7. Arquitetura

O diagnóstico mostrou capacidade prática de analisar cenários arquiteturais e propor soluções.

Entretanto, existe necessidade de maior formalização na estrutura utilizada para tomar decisões.

A estrutura que quero desenvolver ao longo da jornada é:

```text
Problema
    ↓
Requisitos funcionais
    ↓
Requisitos não funcionais
    ↓
Restrições
    ↓
Alternativas
    ↓
Trade-offs
    ↓
Decisão
    ↓
Consequências
```

O objetivo é conseguir não apenas propor uma solução, mas explicar por que ela é adequada para determinado cenário.

---

## 8. Microserviços

Foi identificado conhecimento prático sobre microserviços e escalabilidade, mas também uma necessidade de separar conceitos que frequentemente aparecem associados.

Microserviços não são sinônimo de:

* escalabilidade;
* processamento assíncrono;
* alta performance;
* cloud.

Essas características podem estar presentes em uma arquitetura de microserviços, mas não são consequências automáticas dela.

Também foi identificado o conceito de que um **monólito modular** pode ser uma alternativa válida em determinados cenários.

---

## 9. Principais pontos a formalizar

Os principais gaps identificados foram:

* terminologia de Engenharia de Software;
* terminologia de Arquitetura de Sistemas;
* SOLID;
* Dependency Inversion;
* abstrações;
* separação entre domínio, aplicação e infraestrutura;
* trade-offs arquiteturais;
* formalização de System Design;
* estruturação de decisões arquiteturais.

Esses pontos não representam necessariamente ausência de experiência prática, mas principalmente a necessidade de transformar conhecimento empírico em conhecimento estruturado e comunicável.

---

## 10. Mapa inicial de competências

| Área                        | Situação atual                  |
| --------------------------- | ------------------------------- |
| Desenvolvimento de Software | 🟢 Forte                        |
| C# / .NET                   | 🟢 Forte                        |
| Java / Spring               | 🟢 Forte                        |
| Python                      | 🟢 Forte                        |
| Bancos de dados             | 🟢 Forte                        |
| APIs                        | 🟢 Forte                        |
| Mensageria                  | 🟢 Forte                        |
| Outbox Pattern              | 🟢 Forte                        |
| Idempotência                | 🟢 Forte                        |
| Retry / DLQ                 | 🟢 Forte                        |
| Performance                 | 🟢 Prático                      |
| Escalabilidade              | 🟢 Prático                      |
| Sistemas Distribuídos       | 🟢/🟡                           |
| Requisitos não funcionais   | 🟢/🟡                           |
| Coesão e Acoplamento        | 🟢                              |
| SOLID                       | 🟡                              |
| Abstrações                  | 🟡                              |
| Dependency Inversion        | 🟡                              |
| Arquitetura                 | 🟢 Raciocínio / 🟡 Formalização |
| Trade-offs                  | 🟡                              |
| System Design               | 🟡                              |
| Terminologia formal         | 🟡                              |

---

## 11. Conclusão

O principal resultado desta etapa foi perceber que existe uma base prática significativa sobre Engenharia de Software e Arquitetura de Sistemas.

O desafio desta jornada não será começar do zero.

Será organizar, formalizar e aprofundar conhecimentos que já foram adquiridos ao longo da experiência profissional.

A partir daqui, cada novo conceito deverá ser estudado buscando três dimensões:

1. **Entender o conceito.**
2. **Aplicá-lo na prática.**
3. **Ser capaz de explicar e justificar sua utilização.**

Essa abordagem deverá transformar conhecimento prático em conhecimento estruturado e consciente.

O próximo passo será aprofundar os princípios de **Design de Software**, começando por **SOLID**.
