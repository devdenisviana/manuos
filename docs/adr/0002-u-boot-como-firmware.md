# ADR 0002: U-Boot e TF-A como firmware de inicialização

- **Status:** Aceita
- **Data:** 02/10/2026

## Contexto

Na Orange Pi Zero 2W, a ROM de boot do H618 carrega o primeiro estágio a partir do cartão SD. Antes que um kernel possa rodar, é preciso inicializar a DRAM, configurar clocks e preparar o ambiente de execução dos núcleos ARM. A inicialização da DRAM do H616/H618 é complexa, depende de parâmetros específicos da placa e é pouco documentada pelo fabricante.

## Decisão

A cadeia de boot usará firmware pronto: ROM de boot → U-Boot SPL (inicializa a DRAM) → Trusted Firmware-A (BL31, em EL3) → U-Boot → ManuOS. O desenvolvimento próprio começa no ponto em que o U-Boot transfere a execução para o kernel, normalmente em EL2.

## Alternativas consideradas

- **Escrever o próprio carregador desde a ROM de boot:** exigiria implementar a inicialização da DRAM e o código de EL3, com alto risco e sem relação com os objetivos de um sistema operacional.
- **Carregar o kernel diretamente pelo SPL, sem o U-Boot completo:** economiza alguns segundos de boot, mas perde os recursos do U-Boot que facilitam o desenvolvimento (carga pela serial, variáveis de ambiente, comandos de diagnóstico).

## Consequências

- O risco técnico mais alto do hardware é eliminado.
- O papel do U-Boot é análogo ao do BIOS/UEFI em PCs, o que justifica academicamente a decisão: sistemas operacionais reais não escrevem o próprio firmware.
- O kernel precisa tratar a transição de EL2 para EL1 logo no início.
- O U-Boot é GPL, mas, por ser um programa separado que apenas carrega o kernel, isso não afeta a licença do ManuOS (ver ADR 0005).
