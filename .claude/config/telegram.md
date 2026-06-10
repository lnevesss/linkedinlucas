# Configuração do Telegram Bot

Credenciais do bot para envio de notificações do pipeline LinkedInLucas.

> Não compartilhe este arquivo — contém o token do bot.

## Valores

- **BOT_TOKEN:** `8561809125:AAHonpQsbKzkW83dWoTYqn6DtVyQQr7gEuU`
- **CHAT_ID:** `8983818235`

## Como enviar uma mensagem (PowerShell)

```powershell
$token = "8561809125:AAHonpQsbKzkW83dWoTYqn6DtVyQQr7gEuU"
$chatId = "8983818235"
$text = "sua mensagem aqui"
Invoke-RestMethod -Uri "https://api.telegram.org/bot$token/sendMessage" -Method POST -ContentType "application/json" -Body "{`"chat_id`": `"$chatId`", `"text`": `"$text`", `"parse_mode`": `"Markdown`"}"
```
