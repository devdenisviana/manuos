# Código e materiais de terceiros

O ManuOS é distribuído sob a licença MIT. Para manter essa licença válida, **não se copia código de projetos sob GPL** (como Linux e U-Boot) para este repositório. Esses projetos podem ser consultados como referência para entender o hardware, mas a implementação no ManuOS deve ser própria.

Todo arquivo-fonte do projeto deve começar com o cabeçalho:

```c
// SPDX-License-Identifier: MIT
```

Qualquer código aproveitado de outro projeto com licença compatível (por exemplo, MIT ou BSD) deve ser registrado na tabela abaixo, mantendo-se o aviso de copyright original no próprio arquivo.

| Arquivo no ManuOS | Origem | Licença | Observações |
|---|---|---|---|
| — | — | — | Nenhum código de terceiros até o momento |

## Ferramentas utilizadas (não distribuídas com o projeto)

| Ferramenta | Licença | Uso |
|---|---|---|
| U-Boot | GPL-2.0 | Bootloader na placa (programa separado; carrega o ManuOS) |
| Trusted Firmware-A | BSD-3-Clause | Firmware de EL3 na placa (programa separado) |
| GCC / binutils (Arm GNU Toolchain) | GPL-3.0 (libgcc com GCC Runtime Library Exception) | Compilação |
| QEMU | GPL-2.0 | Emulação |
| GDB | GPL-3.0 | Depuração |
