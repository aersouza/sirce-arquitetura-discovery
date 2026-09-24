# AGENTS.md

Este repositório documenta a arquitetura de um sistema de recomendação de cursos de especialização para apoiar a escolha do melhor curso e reduzir desistência e abandono.

## Objetivo do projeto

O sistema deve ajudar candidatos a:
- entender melhor seu perfil profissional e acadêmico
- definir metas de carreira
- comparar cursos por custo, duração, reputação, demanda de mercado e alinhamento com objetivos
- receber uma recomendação explicável, sem depender apenas de um ranking opaco

## Arquitetura base

A arquitetura documentada neste repositório considera os seguintes blocos:
- Portal web ou app do usuário
- API de recomendação
- Motor de ranking e explicação
- Catálogo de cursos
- Dados de mercado
- Perfil do usuário e preferências
- Gestão administrativa do catálogo e regras

## Regras para implementação futura

1. Ler primeiro o README para entender escopo, limites e visão de negócio.
2. Não inventar regras de negócio que não estejam documentadas.
3. Preservar o princípio de explicabilidade: recomendações devem ter justificativas claras.
4. Tratar o usuário como centro da decisão, não como entrada de um modelo isolado.
5. Considerar que o catálogo e o mercado podem ser incompletos ou inconsistentes.
6. Manter a separação entre dados, decisões e experiência do usuário.

## Contexto estratégico

Este projeto não é uma plataforma completa de ensino. Ele é uma base de apoio à decisão educacional com foco em:
- perfil do candidato
- objetivos de carreira
- custo e disponibilidade
- alinhamento com mercado laboral
- comparação entre alternativas

Qualquer implementação futura deve respeitar essa visão e não ampliar indevidamente o escopo para um LMS completo.
