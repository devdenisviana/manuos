# ManuOS

Sistema operacional educacional, escrito do zero, em modo texto, para a arquitetura ARM de 64 bits (AArch64). Executa diretamente sobre o hardware (bare-metal) da placa **Orange Pi Zero 2W** e também no emulador **QEMU**.

Projeto desenvolvido como Trabalho de Conclusão de Curso (TCC) em Engenharia de Software.

> **Status:** Fase 0 — preparação do ambiente e da estrutura do projeto. Ainda não há código do kernel.

## Objetivo

Implementar, com práticas de engenharia de software, os componentes fundamentais de um sistema operacional:

- inicialização a partir do U-Boot;
- tratamento de exceções e interrupções (GIC e timer genérico ARM);
- gerenciamento de memória física e virtual (MMU);
- processos em modo usuário, escalonamento preemptivo e chamadas de sistema;
- sistema de arquivos virtual sobre uma imagem carregada em memória (initrd);
- shell e utilitários básicos, acessados pelo console serial (UART).

O ManuOS não pretende competir com sistemas de propósito geral, como o Linux. O foco é ser pequeno, legível e bem documentado.

## Plataformas

| Plataforma | SoC / máquina | CPU | Console |
|---|---|---|---|
| Orange Pi Zero 2W (1 GB) | Allwinner H618 | 4× Cortex-A53 | UART0 (16550) via adaptador USB-serial 3,3 V |
| QEMU | `virt` | Cortex-A53 | UART PL011 |

## Estrutura do repositório

| Diretório | Conteúdo |
|---|---|
| `arch/aarch64/` | Código de boot, vetores de exceção, troca de contexto e MMU |
| `platform/qemu-virt/` | Drivers e mapa de memória da máquina `virt` do QEMU |
| `platform/opi-zero2w/` | Drivers e mapa de memória da Orange Pi Zero 2W |
| `kernel/` | Escalonador, processos, memória e chamadas de sistema |
| `fs/` | Sistema de arquivos virtual e leitor do initrd |
| `user/` | Biblioteca de usuário, shell e utilitários |
| `tests/host/` | Testes unitários executados no computador de desenvolvimento |
| `tests/qemu/` | Testes de integração executados no emulador |
| `docs/` | Documentação do projeto e do TCC |
| `tools/` | Scripts de build, geração do initrd e implantação |

## Ambiente de desenvolvimento

- Ubuntu (nativo ou WSL 2)
- Arm GNU Toolchain 15.2.Rel1 (`aarch64-none-elf`)
- QEMU (`qemu-system-aarch64`)
- `gdb-multiarch`
- GNU Make

Instruções de compilação e execução serão adicionadas junto com o primeiro código do kernel.

## Documentação

Ver [`docs/`](docs/README.md): pré-planejamento, cronograma e registros do projeto.

## Licença

Distribuído sob a licença MIT. Ver [`LICENSE`](LICENSE). Código de terceiros, se houver, é registrado em [`docs/terceiros.md`](docs/terceiros.md).

## Sobre o nome

"Manu" é uma homenagem a Emanuele, esposa do autor. Por coincidência, em latim *manu* significa "à mão", o que combina com um sistema operacional feito do zero.
