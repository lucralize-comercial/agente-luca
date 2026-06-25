# Agente Luca — Lucralize

Simulador do agente comercial virtual Luca, desenvolvido para o primeiro atendimento de leads da Lucralize via WhatsApp.

## O que é

O Luca é um agente de IA que atua no time comercial da Lucralize. Ele realiza o primeiro atendimento, qualifica o lead, identifica a unidade certa (Tech ou Contabilidade) e conecta ao consultor especializado — tudo de forma natural, como uma conversa real no WhatsApp.

## Como funciona

```
Lead responde no WhatsApp
        ↓
AgendorChat recebe e envia para o proxy (Railway)
        ↓
Proxy consulta o Claude (Anthropic API)
        ↓
Resposta volta para o AgendorChat
        ↓
Lead recebe a mensagem no WhatsApp
```

Este repositório contém o **simulador** — uma interface web para testar o fluxo de conversa antes de ir para produção.

## Simulador

Acesse: **https://lucralize-comercial.github.io/agente-luca/**

## Arquitetura

| Componente | Descrição | Repositório / URL |
|---|---|---|
| Simulador | Interface web para testes | `lucralize-comercial/agente-luca` |
| Proxy | Servidor Flask no Railway | `lucralize-comercial/agendo-proxy` |
| IA | Claude Sonnet (Anthropic API) | `console.anthropic.com` |
| CRM | Agendor | `agendor.com.br` |
| WhatsApp | AgendorChat | — |

## Fluxo do Luca

1. **Boas-vindas** — saudação natural, sem se identificar como IA
2. **Qualificação** — identifica se é tech (dev, startup, SaaS) ou outro setor
3. **Diagnóstico** — entende a principal dor do lead
4. **Apresentação** — apresenta a solução certa (Lucralize Tech ou Contabilidade)
5. **Fechamento** — coleta nome, e-mail e telefone, transfere para consultor

## Prompt

O prompt do Luca está centralizado no `app.py` do proxy (`agendo-proxy`). Qualquer ajuste no comportamento, tom ou informações deve ser feito lá — vale automaticamente para o simulador e para o WhatsApp.

## Como atualizar o prompt

1. Acesse `github.com/lucralize-comercial/agendo-proxy`
2. Edite o arquivo `app.py`
3. Localize a variável `SYSTEM_PROMPT`
4. Faça as alterações e commit
5. O Railway faz o redeploy automaticamente

## Próximos passos

- [ ] Integrar webhook no AgendorChat
- [ ] Agendamento automático via Microsoft Teams (Graph API)
- [ ] Ativar prompt caching para reduzir custos

## Tecnologias

- **Frontend:** HTML, CSS, JavaScript puro
- **Backend:** Python (Flask), hospedado no Railway
- **IA:** Claude Sonnet 4.5 (Anthropic)
- **Hospedagem do simulador:** GitHub Pages
