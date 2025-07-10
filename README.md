# Integração n8n ↔ Kommo CRM

Este projeto apresenta a solução completa para o desafio técnico da vaga de Desenvolvedor(a) de Integrações e Automação, com foco em automatizar o movimento de leads no Kommo CRM usando o n8n.

## 📁 Conteúdo

| Arquivo                      | Descrição |
|-----------------------------|-----------|
| `A_Documento_Tecnico.md`    | Explicação detalhada da arquitetura, autenticação, chamadas à API, segurança e testes |
| `B_Workflow_n8n.json`       | Versão simples em pseudo-código do fluxo |
| `B_Workflow_n8n_Real.json`  | **Versão real importável** do workflow com integração Kommo + Telegram |
| `C_Plano_Seguranca.md`      | Medidas práticas de segurança, LGPD e proteção de dados sensíveis |
| `D_Checklist_Testes.md`     | Tabela de cenários de teste com entradas e saídas esperadas |
| `Diagrama_n8n.pdf`          | Diagrama referente ao fluxo de trabalho automatizado de processamento de leads com n8n |
| `README.md`                 | Este arquivo com instruções gerais de uso |

## 🚀 Importando o Workflow

1. Acesse o painel do n8n local ou em nuvem.
2. Clique em **Importar** (ícone de pasta no canto superior direito).
3. Envie o arquivo `B_Workflow_n8n_Real.json`.
4. Configure as **credenciais Kommo** e **Telegram Bot** conforme descrito abaixo.

## 🔐 Configurando as Credenciais (n8n)

### Kommo (OAuth2)
1. Vá em *Credenciais* → **Criar nova credencial** → **HTTP Request OAuth2**.
2. Preencha com:
   - Client ID / Secret do app Kommo
   - Auth URL: `https://yourdomain.kommo.com/oauth2/authorize`
   - Token URL: `https://yourdomain.kommo.com/oauth2/access_token`
   - Scope: `leads pipelines`

### Telegram Bot
1. Crie um bot via [@BotFather](https://t.me/BotFather) no Telegram.
2. Copie o **Token do Bot**.
3. Vá em *Credenciais* → **Telegram Bot API** → insira o token.
4. Obtenha seu chat ID com o bot (usando @userinfobot ou enviando mensagem para o bot e capturando via `getUpdates`).

## ✅ Testes Recomendados

Execute os testes descritos em `D_Checklist_Testes.md` para validar:

- Credenciais válidas
- Atualização de lead com score ≥ 80
- Mensagens de sucesso e erro no Telegram

## 🛡️ Segurança

- Tokens e dados são armazenados criptografados pelo n8n
- Dados pessoais são tratados conforme a LGPD
- Logs não devem conter informações sensíveis (ex.: nomes, e-mails)

---

Para estender este fluxo, basta adicionar novos ramos condicionais, sub-flows reutilizáveis e manipulação de tarefas, notas ou negócios usando os endpoints da API Kommo.

