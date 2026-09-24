# Sistema de recomendação de cursos de especialização

## 1) Descrição do sistema

Este sistema tem como objetivo apoiar candidatos a cursos de especialização na escolha do melhor programa, com base em perfil, objetivos de carreira, disponibilidade, orçamento e contexto de mercado. A ideia é reduzir a desistência e o abandono por meio de recomendações mais alinhadas ao candidato, evitando que ele escolha um curso por influência superficial, falta de informação ou excesso de opções.

O sistema funciona como um assistente de decisão para estudantes ou profissionais que querem evoluir em carreira, trocar de área ou aprofundar uma especialização sem assumir riscos desnecessários. Ele agrega dados do perfil do usuário, preferências acadêmicas, histórico profissional, metas de carreira, custo e disponibilidade, além de informações sobre cursos disponíveis, avaliações e demanda de mercado.

### Escopo

- Cadastro e atualização de perfil do usuário
- Coleta de objetivos de carreira e grau de urgência
- Sugestão de cursos com ranking e justificativas
- Comparativo entre cursos por custo, duração, carga horária, modalidade e reputação
- Acompanhamento do processo de decisão e inscrição
- Sugestões de próximos passos para quem está indeciso

### Nível da visão

A visão principal é de um sistema de apoio à decisão orientado por dados e IA. Não se trata de uma plataforma de ensino completa, e sim de um mecanismo de recomendação e orientação que pode ser integrado a um portal acadêmico, consultoria de formação ou canal de relacionamento com instituições.

### Limites e responsabilidades

O sistema deve ser responsável por:

- recomendar cursos com base em regras e dados estruturados
- explicar por que um curso foi sugerido
- indicar trade-offs entre opções
- permitir a revisão manual e a decisão humana

O sistema não deve:

- substituir a escolha final do estudante
- garantir matrícula ou aprovação em curso
- assumir responsabilidade legal por decisões educacionais
- atuar como único critério para formação profissional sem contexto humano

### Integrações

- Catálogo de cursos de instituições parceiras
- Base de dados de mercado de trabalho (salário, demanda, competências em alta)
- Sistema de autenticação e perfil do usuário
- Painel administrativo para gestão de cursos e regras de recomendação
- Eventual integração com e-mail, WhatsApp ou CRM para acompanhamento

### Restrições e lacunas

- Não há garantia de atualização em tempo real do mercado de trabalho
- Os dados de cursos podem variar em qualidade e formato entre instituições
- A recomendação precisa lidar com dados incompletos do usuário
- Pode haver conflito entre objetivo de carreira e preferências pessoais (ex.: custo vs prestígio)
- O sistema não resolve problemas de acessibilidade, ritmo de estudo e perfil individual de aprendizagem sem dados adicionais

## 2) Visão do sistema em linguagem natural

O sistema funciona como um “consultor de formação” digital. Um usuário informa seu perfil, os objetivos desejados e o contexto de decisão. O sistema combina isso com dados do catálogo de cursos e indicadores de mercado para gerar recomendações ordenadas por relevância.

A experiência essencial é: a pessoa entra no sistema, responde algumas perguntas, recebe recomendações, compara opções e pode receber orientações em linguagem natural sobre por que um curso é mais adequado para ela. Essa abordagem reduz a incerteza e aumenta a confiança na escolha.

O sistema tem duas camadas principais: uma camada de dados e regras de negócio e uma camada de experiência orientada por IA. A primeira organiza o catálogo, perfil, histórico e métricas; a segunda interpreta o contexto do usuário e entrega uma recomendação útil e explicável.

## 3) Diagrama estrutural (Mermaid)

Abaixo está uma visão estrutural inspirada em containers, com foco na separação entre a experiência do usuário, o motor de decisão, os dados e a gestão do catálogo.

```mermaid
flowchart LR
    subgraph Cliente[Cliente / Usuário]
        U[Aluno ou profissional em busca de especialização]
    end

    subgraph Frontend[Aplicação de experiência]
        WEB[Portal Web / App]
        IA[Assistente de recomendação]
    end

    subgraph Core[Camada de domínio]
        API[API de recomendação]
        RL[Motor de ranking e explicações]
        PERF[Perfil e preferências do usuário]
        DEC[Regras de decisão / filtros]
    end

    subgraph Dados[Camada de dados]
        CAT[Catálogo de cursos]
        MK[Dados de mercado / renda / demanda]
        HIST[Histórico de decisões e inscrições]
        AUTH[Autenticação e autorização]
    end

    subgraph Admin[Gestão]
        ADM[Operações administrativas]
    end

    U --> WEB
    WEB --> IA
    WEB --> API
    IA --> API

    API --> PERF
    API --> DEC
    API --> RL

    RL --> CAT
    RL --> MK
    RL --> HIST

    PERF --> AUTH
    CAT --> ADM
    MK --> ADM
    HIST --> ADM

    ADM --> CAT
    ADM --> DEC
```

### Ajustes que fiz ao diagrama gerado

- Mantive uma visão simples e adequada ao objetivo de descoberta, em vez de um desenho excessivamente detalhado de microserviços.
- Incluí explicitamente a camada de “dados de mercado”, porque ela é crucial para decidir entre cursos com custo, retorno e demanda diferentes.
- Separei o componente de explicação e ranking do componente de API, para deixar claro que a recomendação não é apenas um filtro bruto, mas uma decisão com interpretação.
- Dei destaque ao papel do administrador, que participa da curadoria do catálogo e da evolução das regras de decisão.

## 4) Diagrama comportamental (Mermaid)

A seguir, um diagrama de sequência ilustrando uma jornada crítica: um candidato busca uma recomendação para um curso de especialização com base em objetivo, orçamento e disponibilidade.

```mermaid
sequenceDiagram
    actor C as Candidato
    participant P as Portal Web
    participant A as API de Recomendação
    participant R as Motor de Ranking
    participant D as Dados de Cursos e Mercado
    participant E as Explicador de Recomendação

    C->>P: Preenche perfil e objetivos de carreira
    P->>A: Solicita recomendação
    A->>R: Envia perfil, preferências e contexto
    R->>D: Busca cursos compatíveis
    D-->>R: Catálogo, custo, duração, reputação e demanda
    R->>E: Calcula justificativas e priorização
    E-->>R: Ranking + explicações em linguagem natural
    R-->>A: Lista de recomendações
    A-->>P: Resultado com comparativo e justificativas
    P-->>C: Mostra cursos sugeridos e trade-offs
    C->>P: Escolhe um curso ou pede outra comparação
    P->>A: Solicita nova recomendação refinada
    A->>R: Reprocessa com filtros adicionais
    R-->>A: Resultado final revisado
    A-->>P: Recomendação ajustada
    P-->>C: Entrega decisão final com contexto
```

### Ajustes no comportamento

- A sequência foi desenhada para refletir uma decisão humana e iterativa, não um processo instantâneo. O usuário pode refinar escolhas e receber um novo ranking.
- Mantive a camada de explicação separada do motor de ranking, para tornar a recomendação mais transparente e útil para a decisão.
- O fluxo mostra que a recomendação depende de múltiplos dados, e não de um único critério como “curso mais popular”.

## 5) Decisões e ajustes em relação ao modelo gerado

O modelo foi útil para formar a base da arquitetura e identificou corretamente os elementos centrais:

- usuário
- catálogo de cursos
- dados de mercado
- API de recomendação
- interface de experiência

No entanto, precisei ajustar alguns pontos para aproximar a solução da realidade de uso:

1. A recomendação precisa ser explicável, não apenas “classificada”. Essa é uma exigência importante para ganhar confiança do usuário.
2. O sistema não é apenas um motor de IA; precisa de catalogação, regras e dados estruturados para funcionar de forma previsível.
3. A presença de um papel administrativo foi importante, porque não é qualquer pessoa que deve decidir sobre cursos permitidos ou regras de recomendação.
4. O sistema deve permitir refinamento incremental: o usuário pode mudar objetivo, orçamento, disponibilidade ou foco profissional e receber uma nova recomendação.

## 6) O que faltaria para um agente construir o sistema sem inventar decisões

Para que um agente de desenvolvimento implementasse o sistema com aderência à arquitetura documentada, faltariam alguns pontos importantes:

- definição do público alvo: estudantes de pós-graduação, profissionais em transição ou candidatos em geral
- regras de priorização: quais critérios pesam mais (preço, objetivo de carreira, reputação, tempo de conclusão, disciplina etc.)
- modelo de dados do usuário e do curso
- critérios de atualização do catálogo e do mercado
- regras de privacidade, consentimento e armazenamento de dados sensíveis
- requisitos de autenticação, autorização e roles administrativas
- definição da experiência de IA: recomendações com justificativa, comparação de alternativas ou conversas guiadas
- arquitetura de integração com fontes de dados externas e indicadores de mercado
- critérios de usabilidade para acessibilidade e suporte à decisão

## 7) Requisitos funcionais

A seguir, a arquitetura foi complementada com requisitos funcionais mínimos para evitar ambiguidades na implementação.

- RF01: o usuário deve conseguir criar e editar seu perfil profissional e acadêmico.
- RF02: o sistema deve permitir informar objetivos de carreira, disponibilidade e orçamento.
- RF03: o sistema deve consultar o catálogo de cursos e filtrar opções por modalidade, custo, duração e requisitos.
- RF04: o sistema deve gerar uma recomendação ordenada por relevância com base em perfil, objetivos e mercado.
- RF05: cada recomendação deve incluir justificativa em linguagem natural, com trade-offs e explicações de priorização.
- RF06: o usuário deve poder comparar duas ou mais opções lado a lado.
- RF07: o sistema deve permitir refinamento da recomendação após nova entrada do usuário.
- RF08: o sistema deve registrar histórico de recomendações, aceitação e rejeição para melhorar o contexto futuro.
- RF09: um administrador deve conseguir cadastrar, revisar e atualizar cursos e regras de recomendação.
- RF10: o sistema deve indicar claramente quando os dados são incompletos ou quando há baixa confiabilidade na recomendação.

## 8) Requisitos não funcionais

- RNF01: o sistema deve responder às recomendações em tempo útil para UX em web/mobile, preferencialmente em até alguns segundos em cenários típicos.
- RNF02: a arquitetura deve permitir escala horizontal para aumentar volume de usuários, cursos e integrações.
- RNF03: as integrações com dados de mercado devem ser resilientes, com fallback e logs quando uma fonte externa falhar.
- RNF04: os dados pessoais devem ser protegidos por políticas de acesso e armazenamento seguro.
- RNF05: a recomendação deve ser explicável e auditável, permitindo rastrear critérios que influenciaram a priorização.
- RNF06: o sistema deve manter a consistência do catálogo, evitando duplicidade de cursos e inconsistência de registros.
- RNF07: a solução deve ser acessível e seguir critérios básicos de usabilidade para usuários com diferentes perfis e níveis de digitalização.
- RNF08: a manutenção deve ser simples, com separação clara entre regras de negócio, integração de dados e experiência do usuário.

## 9) Segurança, privacidade e conformidade

A arquitetura também precisa tratar as exigências de segurança e privacidade para ser adequada a um sistema realista.

- Autenticação: login com autenticação forte para usuários e administradores.
- Autorização: roles distintas para aluno, administrador, analista e instituição parceira.
- Proteção de dados: uso de criptografia em trânsito e em repouso para dados sensíveis.
- Consentimento: coleta de consentimento explícito para uso e armazenamento de dados pessoais.
- Auditoria: registro de acessos e alterações em regras e catálogos.
- Minimização de dados: armazenar somente o necessário para recomendação e suporte à decisão.
- Retenção: política definida para expurgo de dados não mais necessários.
- Tratamento de vieses: os critérios de recomendação devem ser revisados para evitar discriminação ou favorecimento indevido.

## 10) Modelo de dados resumido

A base de dados deve refletir as entidades principais que sustentam a recomendação.

```mermaid
erDiagram
    USUARIO ||--o{ PERFIL : possui
    USUARIO ||--o{ RECOMENDACAO : recebe
    USUARIO ||--o{ FAVORITO : salva
    CURSO ||--o{ RECOMENDACAO_CURSO : aparece_em
    CURSO ||--o{ CURSO_CATEGORIA : pertence
    RECOMENDACAO ||--o{ RECOMENDACAO_CURSO : contem
    ADMINISTRADOR ||--o{ CURSO : curadoria
    ADMINISTRADOR ||--o{ REGRA_RECOMENDACAO : ajusta
    MERCADO ||--o{ CURSO : influencia

    USUARIO {
        string id PK
        string nome
        string email
        datetime criado_em
    }

    PERFIL {
        string id PK
        string usuario_id FK
        string objetivo
        string nivel_experiencia
        decimal orçamento
        string disponibilidade
    }

    CURSO {
        string id PK
        string nome
        string instituicao
        string modalidade
        decimal custo
        int duracao_meses
        string nivel
    }

    RECOMENDACAO {
        string id PK
        string usuario_id FK
        datetime criada_em
        string status
    }

    RECOMENDACAO_CURSO {
        string id PK
        string recomendacao_id FK
        string curso_id FK
        decimal score
        text justificativa
    }

    MERCADO {
        string id PK
        string area
        decimal demanda
        decimal salario_medio
        datetime atualizado_em
    }

    ADMINISTRADOR {
        string id PK
        string nome
        string email
    }

    REGRA_RECOMENDACAO {
        string id PK
        string administrador_id FK
        string nome_regra
        text descricao
        decimal peso
    }
```

## 11) Riscos e mitigação

- Dados incompletos: usar fallback e classificação de confiança da recomendação.
- Mercado em mudança: atualizar indicadores com frequência e manter histórico de versões.
- Viés de recomendação: revisar pesos e critérios periodicamente.
- Falta de confiança do usuário: priorizar explicações e comparação entre alternativas.
- Problemas de privacidade: aplicar minimização, consentimento e controles de acesso.

## 12) Estrutura do repositório

Este repositório foi organizado para manter a documentação enxuta, profissional e útil como contexto para agentes de desenvolvimento.

- README.md: visão geral, escopo e diagramas da arquitetura
- AGENTS.md: instruções rápidas para consumo por IA ou agentes
- docs/architecture.md: visão resumida dos componentes e fluxos
- docs/adr-001.md: decisão central de arquitetura sobre explicabilidade da recomendação
- docs/requirements.md: requisitos funcionais e não funcionais
- docs/security.md: segurança, privacidade e governança
- .gitignore: ignora artefatos locais e temporários

## 13) Resumo executivo

Essa documentação propõe uma solução de recomendação de cursos de especialização como um sistema de apoio à decisão, com foco em clareza, explicabilidade e alinhamento entre perfil e objetivo de carreira. O uso de diagramas em Mermaid permite versionar a arquitetura, revisar decisões e fornecer contexto útil para futuras implementações com IA.

Com a adição de requisitos funcionais, critérios de qualidade, segurança e modelo de dados, a arquitetura deixa de ser apenas um desenho conceitual e passa a ser uma base muito mais sólida para uma implementação real e para uso com agentes de desenvolvimento.
