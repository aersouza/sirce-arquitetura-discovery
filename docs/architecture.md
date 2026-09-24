# Arquitetura de descoberta

## Visão resumida

O sistema é um assistente de decisão para candidatos a cursos de especialização. Ele combina perfil do usuário, catálogo de cursos, dados de mercado e regras de recomendação para entregar uma sugestão explicável e comparativa.

## Componentes principais

- Frontend: portal web ou app para cadastro do perfil e visualização das recomendações.
- API de recomendação: expõe endpoints para gerar e refinamento de sugestões.
- Motor de ranking: combina perfil, filtros, regras de negócio e indicadores de mercado.
- Catálogo de cursos: dados de instituição, modalidade, duração, custo e requisitos.
- Dados de mercado: demanda, salário, competências em alta e indicadores de empregabilidade.
- Gestão administrativa: curadoria do catálogo e ajustes de regras.

## Fluxo principal

1. O usuário informa perfil, objetivos e contexto.
2. A API solicita uma recomendação ao motor.
3. O motor busca cursos compatíveis e combina isso com métricas de mercado.
4. O sistema produz um ranking com justificativas.
5. O usuário percebe comparações e pode refinar a recomendação.

## Limites documentados

- O sistema apoia a decisão, mas não substitui a responsabilidade do candidato.
- A recomendação depende da qualidade dos dados disponíveis.
- O mercado pode mudar rapidamente, exigindo atualização periódica dos indicadores.
- O perfil do usuário pode ser incompleto e a recomendação deve refletir isso.

## Decisões de arquitetura importantes

- O sistema deve ser explicável, em vez de operar como caixa-preta.
- O ranking deve considerar múltiplos critérios, não apenas custo ou popularidade.
- A experiência deve permitir refinamento incremental da recomendação.
- O modelo de domínio é mais importante do que a IA isolada. Dados e regras estruturadas são essenciais.
