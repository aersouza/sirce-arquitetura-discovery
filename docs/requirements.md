# Requisitos do sistema

## Requisitos funcionais

- RF01: criar e editar perfil profissional e acadêmico
- RF02: registrar objetivos de carreira, orçamento e disponibilidade
- RF03: consultar catálogo de cursos com filtros por modalidade, custo, duração e requisitos
- RF04: gerar ranking de cursos com base em perfil e contexto de mercado
- RF05: apresentar justificativas em linguagem natural por curso sugerido
- RF06: permitir comparação de alternativas lado a lado
- RF07: registrar histórico de recomendações e decisões do usuário
- RF08: permitir ajustes no ranking após nova entrada do usuário
- RF09: permitir que administradores cadastrem e atualizem cursos e regras
- RF10: indicar incerteza ou baixa confiabilidade quando os dados estiverem incompletos

## Requisitos não funcionais

- RNF01: tempo de resposta adequado para uso web e mobile
- RNF02: escalabilidade horizontal para crescimento de usuários e cadastros
- RNF03: disponibilidade e recuperação de falhas em integrações externas
- RNF04: qualidade de explicação e rastreabilidade da recomendação
- RNF05: usabilidade com acessibilidade básica e clareza de navegação
- RNF06: manutenção simples e modularização clara de componentes
- RNF07: consistência e integridade dos dados do catálogo
- RNF08: observabilidade com logs, métricas e monitoramento

## Critérios de aceite

- O usuário consegue informar perfil e receber recomendações em menos de alguns segundos em cenário típico.
- Cada recomendação apresenta justificativa compreensível.
- O administrador consegue manter o catálogo e as regras de negócio sem afetar outras partes do sistema.
- A solução comunica claramente limitações de dados e incerteza na recomendação.
