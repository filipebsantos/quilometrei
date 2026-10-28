# Requisitos funcionais

Este documento descreve os requisitos funcionais do Quilometrei.
## Convenções

Os requisitos funcionais são identificados pelo prefixo `RF`, seguido do contexto e um número sequencial de três dígitos.

Exemplo: `RF-VEI-001`.

---
## Veículos

### RF-VEI-001 - Cadastro de veículo

O sistema deve permitir o cadastro de veículos pelo usuário.
#### Critérios de aceitação

- Para o cadastro o sistema deve receber os campos `Nome` e `Placa` do veículo.
- O veículo deve estar vinculado ao usuário.
#### Regras relacionadas

- [[regras-de-negocio#RN-VEI-001 - Exclusão de veículos|RN-VEI-001]]

---
## Abastecimentos

### RF-ABA-001 - Registrar abastecimento

O sistema deve permitir registrar os abastecimentos realizados em um veículo.

#### Critérios de aceitação

- Cada abastecimento deve informar `Odômetro`, `Preço do litro`, `Litros abastecidos`, `Data`, `Tipo de rodagem`, `Tipo de combustível` e se o tanque foi completado. 
- Ao informar `Preço do litro` e `Litros abastecidos`, o sistema deve informar o valor total do abastecimento de forma imediata.
#### Regras relacionadas

- [[regras-de-negocio#RN-ABA-001 - Cálculo do consumo|RN-ABA-001]]
- [[regras-de-negocio#RN-ABA-002 - Abastecimento parcial|RN-ABA-002]]
- [[regras-de-negocio#RN-ABA-003 - Ordem dos abastecimentos|RN-ABA-003]]

### RF-ABA-002 - Listar abastecimentos

O sistema deve permitir visualizar o histórico de abastecimentos filtrados por veículos do usuário e por ordem cronológica decrescente, ou seja, o último registro é mostrado primeiro.

---
## Manutenções

### RF-MAN-001 - Registrar troca de óleo

Permitir registrar a troca óleo informando as seguintes informações: 

- Odômetro
- Data do serviço
- Data da próxima troca
- Odômetro da próxima troca
- Filtro de óleo *(opcional)*
- Valor do serviço