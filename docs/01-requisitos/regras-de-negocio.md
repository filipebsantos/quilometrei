# Regras de negócio

Este documento descreve as regras de negócio que condicionam o comportamento deo Quilometrei
## Veículos

### RN-VEI-001 - Exclusão de veículos

Um veículo pode ser excluído, contudo todos os registros relacionados a esse veículo também devem ser apagados.

---
## Abastecimentos

### RN-ABA-001 - Cálculo do consumo 

Uma nova medição de consumo em `km/L` somente deve ser calculada quando ocorrer um abastecimento que complete o tanque do veículo e existir um abastecimento de tanque cheio anterior. 

O cálculo deve considerar a distância percorrida entre os dois abastecimentos de tanque cheio e a soma dos litros abastecidos após o primeiro abastecimento até o segundo, inclusive.

### RN-ABA-002 - Abastecimento parcial 

Abastecimentos parciais devem ser contabilizados normalmente nos custos do veículo.

Um abastecimento parcial não gera uma nova medição de consumo. Os litros abastecidos devem ser considerados na próxima medição de consumo, quando o tanque for novamente completado.

### RN-ABA-003 - Ordem dos abastecimentos

Os abastecimentos devem ser registrados em ordem cronológica, não sendo permitido o registro retroativo de abastecimentos.

A `Data` de um novo abastecimento não pode ser anterior a data do último abastecimento registrado para o mesmo veículo.

O `Odômetro` informado não pode ser interior ao odômetro o último abastecimento registrado para o mesmo veículo.

---
## Manutenções

