# ADR 0003: Desenvolvimento primeiro no QEMU, com camada de abstração de hardware

- **Status:** Aceita
- **Data:** 02/10/2026

## Contexto

Testar cada mudança na placa real é lento: a Orange Pi Zero 2W não tem porta Ethernet (o que impede a carga do kernel via TFTP), e a depuração no hardware se limita praticamente a mensagens pela serial. A máquina `virt` do QEMU, configurada com Cortex-A53 e GICv2, compartilha com o H618 o controlador de interrupções (GIC-400/GICv2) e o timer genérico ARM, mas usa outra UART (PL011, enquanto o H618 usa uma UART compatível com 16550).

## Decisão

Cada funcionalidade será desenvolvida e depurada primeiro no QEMU (com GDB) e validada na placa a cada marco. O núcleo do kernel acessará o hardware somente por meio de uma camada de abstração de hardware (HAL), com interfaces genéricas (console, timer, controlador de interrupções, GPIO). Cada plataforma (`platform/qemu-virt` e `platform/opi-zero2w`) fornece sua implementação.

## Alternativas consideradas

- **Desenvolver apenas na placa:** ciclo de teste lento e depuração muito limitada.
- **Desenvolver apenas no QEMU:** não validaria o objetivo de rodar em hardware real e esconderia diferenças de comportamento até o fim do projeto.
- **Usar diretamente a UART do QEMU sem abstração:** mais simples no início, mas exigiria alterar o núcleo ao portar para a placa.

## Consequências

- Ciclo de desenvolvimento rápido, com depuração passo a passo via GDB.
- O porte entre plataformas exige apenas drivers e mapa de memória novos, sem mudanças no núcleo.
- A HAL é uma decisão de arquitetura que pode ser discutida e avaliada no TCC.
- Existe o risco de diferenças entre emulador e hardware; ele é mitigado validando na placa a cada marco, começando pelo marco M2 ainda no primeiro semestre.
