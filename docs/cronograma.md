# Cronograma de acompanhamento — ManuOS (TCC)

**Projeto:** ManuOS — sistema operacional educacional bare-metal em modo texto para ARM64 (Orange Pi Zero 2W)
**Repositório:** https://github.com/devdenisviana/manuos
**Documento de referência:** `docs/pre-planejamento-tcc-kernel-arm64.docx` (versão 0.1)
**Última atualização:** 02/10/2026

> **Passo atual:** T0.9 a T0.11 — Extrair os arquivos iniciais no repositório e fazer o primeiro commit

## Legenda

- `[ ]` não iniciado
- `[~]` em andamento (anotar no campo de observações)
- `[x]` concluído (anotar a data)
- `[-]` adiado (motivo no registro de progresso)

## Visão geral das fases

| Fase | Descrição | Semestre | Marco | Status |
|---|---|---|---|---|
| 0 | Preparação: estudo, hardware e ambiente | 1 | M1 — mensagem via UART no QEMU | Em andamento |
| 1 | Boot na placa real | 1 | M2 — mensagem via UART na Orange Pi | Não iniciada |
| 2 | Exceções e interrupções | 1 | M3 — tick periódico no QEMU e na placa | Não iniciada |
| 3 | Gerenciamento de memória | 2 | M4 — memória virtual ativa | Não iniciada |
| 4 | Processos e chamadas de sistema | 2 | M5 — processos de usuário concorrentes | Não iniciada |
| 5 | Sistema de arquivos e shell | 3 | M6 — shell funcional na placa | Não iniciada |
| 6 | Avaliação e fechamento | 3 | M7 — defesa | Não iniciada |

---

## Fase 0 — Preparação (estimativa: 5 a 6 semanas)

Objetivo: deixar tudo pronto para programar (hardware testado, ambiente instalado, repositório organizado) e terminar com o primeiro código do kernel rodando no QEMU.

### Bloco A — Hardware de apoio e itens acadêmicos (semana 1)

- [x] **T0.1** Hardware de apoio — 02/10/2026: adaptador USB-serial CP2102, cabos Dupont, cartão microSD de 64 GB e fonte USB já disponíveis
- [ ] **T0.1b** Comprar o segundo cartão microSD (não bloqueia o andamento)
- [-] **T0.2** Enviar perguntas à coordenação do curso — adiado
- [-] **T0.3** Normas da Estácio e matriz curricular — adiado

### Bloco B — Ambiente de desenvolvimento (semanas 1 e 2)

- [x] **T0.4** Instalar no WSL 2 as ferramentas básicas (git, make, compiladores do host) — 02/10/2026
- [x] **T0.5** Instalar o compilador cruzado AArch64 bare-metal e confirmar a versão — 02/10/2026
- [x] **T0.6** Instalar o QEMU (`qemu-system-aarch64`) e o `gdb-multiarch` — 02/10/2026
- [ ] **T0.7** Instalar um terminal serial no Windows (PuTTY ou Tera Term) para a placa — remanejada para junto do Bloco D
- [x] **T0.8** Testar a cadeia completa com um programa mínimo no QEMU (teste de fumaça do ambiente) — 02/10/2026

### Bloco C — Repositório e documentação (semana 2)

- [~] **T0.9** Criar o repositório no GitHub com a estrutura de diretórios do pré-planejamento — repositório criado; estrutura no pacote inicial
- [~] **T0.10** Adicionar README, licença e `.gitignore` — no pacote inicial
- [~] **T0.11** Colocar em `docs/` o pré-planejamento e este cronograma — no pacote inicial
- [ ] **T0.12** Criar os modelos de ADR (registro de decisão) e do diário de desenvolvimento
- [ ] **T0.13** Registrar as primeiras ADRs: linguagem C, U-Boot como firmware, initrd

### Bloco D — Hardware (quando o adaptador chegar)

- [ ] **T0.14** Gravar uma imagem pronta (oficial da Orange Pi ou Armbian) num cartão microSD
- [ ] **T0.15** Ligar o adaptador serial na placa (GND, TX e RX cruzados; sem ligar o VCC)
- [ ] **T0.16** Ver o log de boot completo no terminal serial (U-Boot + Linux) a 115200 baud
- [ ] **T0.17** Acessar o prompt do U-Boot pela serial e explorar comandos básicos (`help`, `bdinfo`, `printenv`)

### Bloco E — Estudo dirigido (semanas 2 a 4, em paralelo)

- [ ] **T0.18** OSTEP: capítulos introdutórios de virtualização da CPU (processos, API, execução direta limitada)
- [ ] **T0.19** AArch64: registradores, instruções básicas, convenção de chamada (AAPCS64)
- [ ] **T0.20** AArch64: níveis de exceção (EL0 a EL3) e como o processador chega ao kernel
- [ ] **T0.21** Linker scripts e o processo de boot de um binário bare-metal
- [ ] **T0.22** Tutorial raspberry-pi-os: lição 1 (estudar, não necessariamente executar)
- [ ] **T0.23** Iniciar fichamento para a fundamentação teórica do TCC

### Bloco F — Primeiro código (semanas 4 a 6)

- [ ] **T0.24** Escrever o código de entrada em Assembly (`boot.S`): pilha, zerar BSS, parar núcleos secundários
- [ ] **T0.25** Escrever o linker script do kernel
- [ ] **T0.26** Escrever o driver mínimo da UART PL011 (QEMU)
- [ ] **T0.27** Escrever o `kernel_main` em C imprimindo uma mensagem
- [ ] **T0.28** Criar o Makefile com os alvos `all`, `run` (QEMU), `debug` (QEMU + GDB) e `clean`
- [ ] **T0.29** Depurar o boot com GDB no QEMU (pausar na entrada e avançar passo a passo)
- [ ] **T0.30** Configurar a CI no GitHub Actions compilando o kernel a cada commit
- [ ] **🏁 M1** Mensagem exibida via UART no QEMU, com o código no repositório e a CI passando

---

## Fases seguintes (detalhadas quando chegarmos nelas)

### Fase 1 — Boot na placa real
- [ ] Compilar o U-Boot para a Zero 2W ou usar o da imagem pronta
- [ ] Driver da UART 16550 do H618
- [ ] Primeira versão da HAL (console genérico com implementações QEMU e Orange Pi)
- [ ] Carregar o kernel pelo U-Boot e executar
- [ ] **🏁 M2** Mensagem via UART na Orange Pi

### Fase 2 — Exceções e interrupções
- [ ] Transição EL2 → EL1
- [ ] Tabela de vetores de exceção e tratamento de erros
- [ ] Driver do GIC-400
- [ ] Timer genérico com tick periódico
- [ ] Texto do TCC 1 (se aplicável ao calendário do curso)
- [ ] **🏁 M3** Tick periódico no QEMU e na placa

### Fase 3 — Gerenciamento de memória
- [ ] Alocador de páginas físicas
- [ ] Tabelas de tradução e ativação da MMU
- [ ] Heap do kernel
- [ ] **🏁 M4** Kernel com memória virtual ativa

### Fase 4 — Processos e chamadas de sistema
- [ ] Estrutura de processo e troca de contexto
- [ ] Escalonador preemptivo round-robin
- [ ] Execução em EL0
- [ ] Chamadas de sistema via `svc`
- [ ] **🏁 M5** Vários processos de usuário em execução concorrente

### Fase 5 — Sistema de arquivos e shell
- [ ] Leitor de initrd (tar/USTAR) e VFS
- [ ] Carregador ELF
- [ ] Shell e utilitários
- [ ] **🏁 M6** Shell funcional na placa

### Fase 6 — Avaliação e fechamento
- [ ] Medições (boot, footprint, troca de contexto, syscalls)
- [ ] Extensões opcionais, se houver tempo
- [ ] Escrita final e preparação da defesa
- [ ] **🏁 M7** Defesa

---

## Registro de progresso

| Data | Tarefa | Observações |
|---|---|---|
| 02/10/2026 | — | Pré-planejamento aprovado (v0.1); cronograma criado |
| 02/10/2026 | Decisão | O projeto segue independente de retorno da universidade; adaptações acadêmicas (formato, normas, orientador) serão feitas depois. T0.2 e T0.3 adiados |
| 02/10/2026 | T0.1 | Concluída: CP2102, cabos Dupont, cartão de 64 GB e fonte USB disponíveis. Segundo cartão a comprar (T0.1b) |
| 02/10/2026 | Ambiente | Decidido usar WSL 2 (não o Windows nativo): a Fase 1 exige Linux para compilar o U-Boot e o ambiente fica igual ao da CI. VS Code no Windows com a extensão WSL |
| 02/10/2026 | Ambiente | Ubuntu 26.04.1 LTS instalado no WSL 2 e definido como distribuição padrão. Erro `Wsl/Service/E_UNEXPECTED` resolvido com `wsl --update` + reinício do Windows |
| 02/10/2026 | T0.4 | Concluída: gcc 15.2.0, GNU Make 4.4.1, git 2.53.0. Trabalhar sempre em `~` (sistema de arquivos Linux), nunca em `/mnt/c` |
| 02/10/2026 | T0.5 | Concluída: Arm GNU Toolchain 15.2.Rel1 (`aarch64-none-elf-gcc` 15.2.1) em `~/toolchains`, adicionado ao PATH via `~/.bashrc` |
| 02/10/2026 | T0.6 | Concluída: QEMU 10.2.1 e gdb-multiarch 17.1 (pacotes do Ubuntu) |
| 02/10/2026 | Ambiente | VS Code no Windows conectado ao Ubuntu pela extensão WSL |
| 02/10/2026 | T0.8 | Concluída: programa mínimo em Assembly escreveu na UART PL011 (0x09000000) da máquina `virt`, ligado em 0x40080000. Cadeia compilador → linker → QEMU validada. T0.7 remanejada para o Bloco D |
| 02/10/2026 | Decisão | Nome do sistema: **ManuOS** (homenagem a Emanuele, "Manu"; em latim, *manu* = "à mão", alusão a um kernel feito do zero). Repositório público `manuos` no GitHub; nome confirmado como disponível |
| 03/10/2026 | T0.9 | Git configurado no Ubuntu (usuário `devdenisviana`, branch padrão `main`); GitHub CLI autenticado (HTTPS, escopos `repo` e `workflow`); repositório público `devdenisviana/manuos` criado e clonado em `~/projetos/manuos` |
| 03/10/2026 | Decisão | Licença **MIT** (permissiva, mesma do xv6). Regras: nenhum código GPL copiado para o projeto (Linux/U-Boot apenas como referência), cabeçalho `SPDX-License-Identifier: MIT` em todo arquivo-fonte, código de terceiros registrado em `docs/terceiros.md` |
