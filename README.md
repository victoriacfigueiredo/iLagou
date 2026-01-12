<p align="center">
  <img src="./assets/images/logo.png" alt="iLagou logo" width="200" />
</p>

# iLagou

O iLagou é um sistema de previsão de alagamentos para rotas na cidade do Recife. Ele utiliza dados de sensores pluviométricos, previsão do tempo, maré e geocodificação para calcular o risco de alagamento em trajetos definidos pelo usuário (por endereço ou CEP). O objetivo é ajudar pessoas a planejarem rotas mais seguras em dias de chuva, evitando áreas de risco.

## Funcionalidades principais
- Cálculo de risco de alagamento entre dois pontos (endereços ou CEPs)
- Consulta de sensores pluviométricos
- Análise do nível da maré
- Identificação de pontos críticos e geração de alertas 

## Estrutura importante do projeto
- App & navegação
  - [app/_layout.tsx](app/_layout.tsx) — Provedor global e layout raiz.
  - [app/(tabs)/_layout.tsx](app/(tabs)/_layout.tsx) — Layout de abas do app.
  - [app/(tabs)/index.tsx](app/(tabs)/index.tsx) — Tela inicial (dashboard).
  - [app/(tabs)/routes.tsx](app/(tabs)/routes.tsx) — Tela de gerenciamento de rotas.
  - [app/(tabs)/alerts.tsx](app/(tabs)/alerts.tsx) — Lista de alertas.
  - [app/(tabs)/settings.tsx](app/(tabs)/settings.tsx) — Configurações.

- Contextos e hooks
  - `src/contexts/RouteContext.tsx` — Gestão das rotas e integração com a API.
  - `src/contexts/NotificationContext.tsx` — Gestão de alertas e notificações.
  - `hooks/useFrameworkReady.ts` — hook utilitário.

- Serviços
  - `src/services/api.ts` — chama a API externa para obter probabilidade de risco.

- Componentes
  - `components/AlertToast.tsx` — Toast de alerta.
  - `components/RouteCard.tsx` — Cartão de exibição de rota.

- Dados de exemplo
  - `utils/mockData.ts` — rotas e alertas mock para desenvolvimento.

## Como funciona a verificação de risco
Quando uma rota é adicionada/atualizada o fluxo é:
1. Componente chama `addRoute` / `updateRoute`.
2. É chamada a função `getRiskForRoute` que faz POST para a API (URL base definida em `API_BASE_URL`).
3. O contexto atualiza `status`, `riskLevel` e cria alertas via `useNotifications` quando necessário.
