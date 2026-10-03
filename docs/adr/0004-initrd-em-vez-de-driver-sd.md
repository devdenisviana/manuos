# ADR 0004: Sistema de arquivos em initrd, sem driver de cartão SD no escopo mínimo

- **Status:** Aceita
- **Data:** 02/10/2026

## Contexto

O kernel precisa de arquivos (programas de usuário, dados) para que o shell e o carregador ELF tenham o que executar. Ler o cartão SD diretamente exigiria um driver para o controlador MMC do Allwinner, que é trabalhoso e pouco documentado, além de um sistema de arquivos como FAT32.

## Decisão

No escopo mínimo, os arquivos do sistema estarão em uma imagem (initrd) no formato tar/USTAR, carregada na RAM pelo U-Boot junto com o kernel. O kernel lê essa imagem por meio de um sistema de arquivos virtual (VFS) simples. O driver de cartão SD e a leitura de FAT32 ficam como extensões opcionais.

## Alternativas consideradas

- **Driver do controlador MMC e FAT32 desde o início:** alto custo e risco, desviando esforço dos mecanismos centrais do sistema operacional.
- **Arquivos embutidos no binário do kernel:** ainda mais simples, mas acopla os programas de usuário ao kernel e exige recompilá-lo a cada mudança.

## Consequências

- O kernel tem arquivos disponíveis cedo, sem depender de drivers de armazenamento.
- O formato tar é simples de ler e de gerar com ferramentas padrão.
- Os arquivos são somente leitura (ou voláteis, se houver um sistema de arquivos em RAM) e se perdem ao desligar.
- O VFS precisa ser projetado de forma que um driver de SD possa ser acrescentado depois sem mudanças estruturais.
