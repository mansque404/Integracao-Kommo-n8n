# Check-list de Testes

| Caso | Entrada simulada | Resultado Esperado | cURL |
|------|------------------|--------------------|------|
| 1    | lead_id válido, score 85 | Lead atualizado | `curl -X POST https://seusite.com/kommo-hook -d '{"lead_id": 123, "scoring": 85}'` |
| 2    | Token expirado | Token renovado, requisição refeita | - |
| 3    | status_id inválido | Erro 400 | - |
| 4    | lead_id inexistente | Erro 404 capturado | - |
