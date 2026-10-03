# ADR 0001: Linguagem de implementação: C e Assembly AArch64

- **Status:** Aceita
- **Data:** 02/10/2026

## Contexto

O kernel precisa de uma linguagem que permita acesso direto ao hardware (registradores mapeados em memória, controle do layout de memória, integração com Assembly) e que seja viável dentro do prazo de três semestres. O autor tem cerca de um ano de experiência profissional com C/C++ em projetos industriais e nunca trabalhou com Rust. O projeto já tem uma fonte relevante de incerteza: o hardware (SoC Allwinner H618, com documentação parcial).

## Decisão

O kernel será escrito em C (padrão C11), com Assembly AArch64 nos pontos em que o C não alcança: ponto de entrada, vetores de exceção, troca de contexto e acesso a registradores de sistema.

## Alternativas consideradas

- **Rust (`no_std`):** oferece segurança de memória verificada pelo compilador e seria um diferencial acadêmico. Foi descartado porque exigiria aprender a linguagem ao mesmo tempo que o hardware, dobrando a incerteza; porque o código mais crítico de um kernel precisa de blocos `unsafe`, o que reduz o ganho de segurança; e porque o material de referência é muito menor.
- **C++ (freestanding):** possível, mas exige desativar exceções e RTTI e controlar cuidadosamente o runtime, sem ganho claro para o escopo do projeto. A maior parte das referências de kernels está em C.

## Consequências

- Produtividade desde o início, aproveitando a experiência prévia.
- Acesso direto a quase todo o material de referência (xv6, Linux, U-Boot, OSDev), que está em C.
- A segurança de memória fica sob responsabilidade do desenvolvedor. Para compensar: compilação com `-Wall -Wextra -Werror`, análise estática (clang-tidy, cppcheck), regras baseadas em um subconjunto do MISRA C e testes no host com AddressSanitizer e UBSan, todos executados na CI.
