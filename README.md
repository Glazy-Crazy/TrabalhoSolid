Diego Careno Rodrigues

Gerenciador de Tarefas – Aplicação dos Princípios SOLID

Este projeto consiste em um gerenciador de tarefas simples, desenvolvido em Java 17, que aplica os cinco princípios do SOLID. O objetivo é demonstrar boas práticas de programação orientada a objetos, promovendo a separação de responsabilidades e a injeção de dependências, sem utilizar um banco de dados externo (todos os dados são mantidos em memória).

Índice

Introdução

Componentes do Sistema

Camada de Domínio

Camada de Serviço

Camada de Apresentação

Classe Principal

Princípios SOLID Aplicados

Introdução

A aplicação possibilita:

Criar novas tarefas: O usuário informa um título e uma prioridade.

Listar todas as tarefas: Apresenta a relação de tarefas com seus respectivos status (concluída ou pendente).

Marcar tarefas como concluídas: Permite ao usuário indicar a finalização de uma tarefa.

Filtrar tarefas por prioridade: Exibe apenas as tarefas com uma determinada prioridade.

A interface da aplicação é baseada no console (terminal), e sua estrutura segue três camadas principais: Domínio, Serviço e Apresentação.

Componentes do Sistema

Camada de Domínio

Task.java

Finalidade: Representa uma tarefa com os atributos title, priority e done, indicando se está concluída.

Princípio Aplicado: Single Responsibility Principle (SRP)A classe é responsável exclusivamente pelos dados e comportamentos relacionados a uma tarefa.

Destaque no Código:Implementa o método toString(), que gera uma representação textual da tarefa, garantindo uma separação clara entre dados e apresentação.

TaskManager.java

Finalidade: Gerencia a lista de tarefas, fornecendo funcionalidades para adicionar, recuperar e filtrar tarefas.

Princípio Aplicado: SRPMantém a lógica central de gerenciamento de tarefas, sem interferir em outras responsabilidades do sistema.

Destaque no Código:O método filterByPriority utiliza streams para tornar o código mais conciso e expressivo.

Completable.java

Finalidade: Define uma interface para classes que podem ser concluídas.

Princípio Aplicado: Interface Segregation Principle (ISP)Garante que apenas classes que realmente precisam dessa funcionalidade implementem essa interface.

Camada de Serviço

TarefasService.java

Finalidade: Contém a lógica de criação, listagem, conclusão e filtragem de tarefas.

Princípios Aplicados: SRP e Dependency Inversion Principle (DIP)A classe gerencia a lógica de negócio sem lidar diretamente com entrada ou saída de dados.

Destaque no Código:O método criarTarefas recebe os dados e cria uma nova instância de Task, mantendo a responsabilidade de entrada de dados separada da lógica central.

ITaskPrinter.java & ConsoleTaskPrinter.java

Finalidade: Define e implementa uma abstração para exibição das tarefas.

Princípios Aplicados:

Open/Closed Principle (OCP): Permite adicionar novas formas de exibição sem modificar o código existente.

Dependency Inversion Principle (DIP): O código depende de abstrações (ITaskPrinter) em vez de implementações concretas.

Destaque no Código:ITaskPrinter define o contrato para exibição das tarefas, enquanto ConsoleTaskPrinter implementa a exibição no console.

Camada de Apresentação

ConsoleMenu.java

Finalidade: Gerencia a interação com o usuário, exibindo menus e capturando entradas.

Princípio Aplicado: SRPSepara a lógica de apresentação da lógica de negócios.

Destaque no Código:Utiliza try-with-resources para gerenciar o Scanner e um switch para processar as opções do menu.

Classe Principal

Main.java

Finalidade: Ponto de entrada do sistema, onde as dependências são instanciadas e o menu principal é acionado.

Princípio Aplicado: Dependency Inversion Principle (DIP)A inicialização do sistema ocorre com injeção de dependências, tornando o código mais modular e testável.

Destaque no Código:O main instancia TaskManager e ITaskPrinter, injetando-os no ConsoleMenu.

Princípios SOLID Aplicados

Single Responsibility Principle (SRP):Cada classe tem uma única responsabilidade bem definida, como Task (dados da tarefa), TaskManager (gerenciamento de tarefas) e ConsoleMenu (interação com o usuário).

Open/Closed Principle (OCP):O uso de interfaces, como ITaskPrinter, permite a adição de novas funcionalidades sem alterar código já existente.

Liskov Substitution Principle (LSP):Classes que implementam interfaces, como ConsoleTaskPrinter, podem ser substituídas sem impacto no sistema.

Interface Segregation Principle (ISP):Interfaces específicas, como Completable, evitam a implementação de métodos desnecessários em classes que não precisam deles.

Dependency Inversion Principle (DIP):O sistema depende de abstrações em vez de implementações concretas, favorecendo a flexibilidade e manutenção.
