<div align="center">

![Quilometrei](.github/logo_horizontal.svg)

</div>

- [Sobre o Quilometrei](#sobre-o-quilometrei)
    - [Contexto de desenvolvimento](#contexto-de-desenvolvimento)
- [Arquitetura](#arquitetura)
    - [Visão geral](#visão-geral)
        - [Back-End](#back-end)
        - [Front-End](#front-end)
        - [Persistência de dados](#persistência-de-dados)
    - [Decisões arquiteturais](#decisões-arquiteturais)
        - [Modelagem orientada ao domínio](#modelagem-orientada-ao-domínio)
        - [Separação dos contêiners](#separação-dos-contêineres)
        - [Desenvolvimento do aplicativo móvel](#desenvolvimento-do-aplicativo-móvel)

## Sobre o Quilometrei

O Quilometrei surgiu da necessidade de substituir as planilhas utilizadas para acompanhar o consumo de combustível do meu carro, especialmente quando passei a precisar registrar também os abastecimentos da minha moto.

Com o tempo, o uso de planilhas se mostrou pouco prático, principalmente no controle de abastecimentos parciais, que exigem considerar múltiplos registros para calcular corretamente o consumo médio de combustível (km/L).

O projeto também passou a contemplar o registro de manutenções preventivas e corretivas, permitindo acompanhar o histórico de serviços e obter uma visão mais completa dos custos de manutenção dos veículos.

### Contexto de desenvolvimento

O Quilometrei é um projeto de uso real, desenvolvido também como trabalho de conclusão do curso de Full Cycle do programa Geração Tech 4.0 e das atividades do App Clicks, do IFCE Campus Paracuru.

Além de implementar as funcionalidades da aplicação, o desenvolvimento busca aplicar os conhecimentos adquiridos durante as formações, abrangendo desde o levantamento de requisitos e planejamento da solução até a organização do código, as decisões arquiteturais, a conteinerização e os processos de implantação.

As escolhas técnicas são orientadas pelas necessidades do projeto, priorizando simplicidade, manutenção, segurança e possibilidade de evolução.

## Arquitetura

### Visão geral

O Quilometrei é composto por uma API REST, responsável pelo processamento das regras de negócio e persistência dos dados, e um aplicativo móvel, responsável pela interação com o usuário.

A comunicação entre os componentes ocorre por meio de requisições HTTP à API, permitindo que a interface e o back-end sejam desenvolvidos de forma independente.

#### Back-end

O back-end é desenvolvido em PHP, utilizando o framework Slim para disponibilizar os endpoints da API REST.

A aplicação é executada pelo PHP-FPM, enquanto o Nginx atua como servidor HTTP e encaminha as requisições PHP ao serviço responsável pelo processamento. Ambos são executados em contêineres independentes.

#### Front-end

O aplicativo móvel é desenvolvido utilizando a plataforma low-code FlutterFlow, que consome os endpoints da API REST para apresentar e manipular os dados dos veículos.

#### Persistência de dados

O PostgreSQL é usado como banco de dados relacional para armazenar a informações veículos, abastecimentos e manutenções.

### Decisões arquiteturais

As decisões arquiteturais do Quilometrei consideram o escopo da aplicação, os requisitos identificados e a necessidade de equilibrar simplicidade, manutenção e evolução do sistema.

#### Modelagem orientada ao domínio

A aplicação adota uma abordagem simplificada de Domain-Driven Design (DDD), aproveitando conceitos de modelagem do domínio sem implementar integralmente seus padrões.

A decisão busca organizar e isolar as regras de negócio, evitando que fiquem diretamente acopladas aos mecanismos de persistência ou à camada HTTP.

#### Separação dos contêineres

A infraestrutura utiliza contêineres independentes para Nginx e PHP-FPM, em vez de executar ambos os processos em um único contêiner utilizando o `supervisord` para orquestrar o processos.

Essa separação estabelece responsabilidades distintas para cada serviço, simplifica o gerenciamento individual dos processos e permite modificar suas configurações de maneira independente.

Como contrapartida, exige configurações adicionais de comunicação entre os contêineres e de disponibilização dos arquivos da aplicação.

#### Desenvolvimento do aplicativo móvel

A escolha do **FlutterFlow** está relacionada à proposta do curso App Clicks, voltado ao desenvolvimento rápido de aplicações utilizando ferramentas no-code e low-code.

Considerando o escopo do Quilometrei, a plataforma permite concentrar os esforços na implementação das funcionalidades e na experiência do usuário, enquanto as regras de negócio e a persistência permanecem sob responsabilidade da API.