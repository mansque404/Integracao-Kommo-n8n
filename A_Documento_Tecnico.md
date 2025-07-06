# Documento Técnico – Integração n8n ↔ Kommo CRM

## 1. Arquitetura do Workflow n8n

**Gatilhos**:
- Webhook (para eventos como resposta positiva ou pagamento)
- Cron (verificações periódicas)
- Fila (opcional para escala)

**Sequência de nós**:
Webhook → Function (validação) → HTTP Request (GET lead) → IF (score) → PATCH lead → Error Handler

```
[Webhook]
    ↓
[Function: valida entrada]
    ↓
[HTTP GET: buscar lead]
    ↓
[IF: condição atendida?]
 ┌───────────────┐
 ↓               ↓
[Atualiza Lead] [Ignora]
    ↓
[Sucesso ou Erro]
```

## 2. Autenticação no Kommo

- **Método:** OAuth 2.0
- **Armazenamento:** n8n Credentials (criptografado)
- **Renovação:** automático via refresh_token

## 3. Chamadas à API do Kommo

- Listar pipelines: `GET /api/v4/leads/pipelines`
- Obter lead: `GET /api/v4/leads/{id}`
- Atualizar lead: `PATCH /api/v4/leads/{id}`

**Exemplo de corpo:**
```json
{
  "pipeline_id": "123456",
  "status_id": "678901"
}
```

**Paginação/Rate-limit:** usar cabeçalhos, retry com back-off

## 4. Mapeamento de Dados

**Campos de entrada**:
- lead_id, scoring, status

**Tratamento**:
- Validar campos obrigatórios (Function)
- Condicionais para campos opcionais

## 5. Tratamento de Erros e Retry

- Retry com back-off: 1s → 3s → 10s
- Error Trigger → Slack ou e-mail
- Leads com erro → fila manual

## 6. Segurança e Conformidade

- Logs: sem PII
- Criptografia: tokens via n8n
- Conformidade LGPD: consentimento, auditoria

## 7. Observabilidade

**Métricas**:
- Sucesso vs erro
- Duração média

**Logs JSON**:
```json
{
  "timestamp": "2025-07-05T14:00:00Z",
  "lead_id": 1234,
  "action": "stage_update",
  "result": "success",
  "duration_ms": 820
}
```

## 8. Teste e Validação

**Cenários**:
- Happy path
- Token expirado
- Status inválido
- Lead não encontrado

## 9. Extensibilidade

- Suporte a notas, tarefas, negócios
- Sub-flows reutilizáveis
- Isolar lógica por tipo de evento
