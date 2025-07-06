# Plano de Segurança

| Item                        | Medida prática                                  |
|-----------------------------|--------------------------------------------------|
| Armazenar credenciais       | Usar recurso “Credentials” do n8n (criptografado) |
| Reduzir PII em logs         | Remover campos sensíveis antes de logar         |
| Proteção via HTTPS          | Todo endpoint de webhook protegido via HTTPS    |
| Rate-limit e firewall       | Controlar IPs e limitar chamadas                |
| Backup criptografado        | Dados do n8n devem estar sob backup seguro      |
