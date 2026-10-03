# ADR 0005: Licença MIT e política para código de terceiros

- **Status:** Aceita
- **Data:** 03/10/2026

## Contexto

O repositório do ManuOS é público e precisa de uma licença que defina como o código pode ser reutilizado. O projeto consulta, como referência, código sob GPL (Linux, U-Boot) e código sob licenças permissivas (xv6, sob MIT).

## Decisão

O ManuOS é distribuído sob a licença MIT. Para preservá-la:

- nenhum código de projetos sob GPL é copiado para o repositório; esses projetos são usados apenas como referência para entender o hardware;
- todo arquivo-fonte começa com o cabeçalho `SPDX-License-Identifier: MIT`;
- código aproveitado de projetos com licença compatível é registrado em `docs/terceiros.md`, mantendo o aviso de copyright original.

## Alternativas consideradas

- **GPL (v2 ou v3):** garantiria que versões derivadas permanecessem abertas, mas restringe a reutilização em outros contextos, o que vai contra o objetivo educacional.
- **BSD 2-Clause:** praticamente equivalente à MIT; a MIT foi escolhida por ser a licença do xv6, principal referência de kernel educacional.

## Consequências

- Qualquer pessoa pode estudar, modificar e reutilizar o código, inclusive em outros projetos.
- Ferramentas GPL usadas no desenvolvimento (GCC, GDB, QEMU) e o U-Boot, por ser um programa separado, não afetam a licença do ManuOS. A `libgcc`, se ligada ao kernel, é coberta pela GCC Runtime Library Exception.
- Exige disciplina ao consultar drivers do Linux e do U-Boot: entender o funcionamento e escrever implementação própria.
