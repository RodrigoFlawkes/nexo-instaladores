# NEXO — instaladores

Instaladores oficiais dos apps da família NEXO. Este repositório guarda **somente** instaladores assinados e seus manifestos. Não contém código-fonte, chaves, tokens nem dados pessoais.

Ainda não há versões publicadas.

## Como as versões são organizadas

Cada versão é uma *release* com a tag `<app>-v<versão>`, por exemplo `nexo-ai-v0.5.1`. Cada release traz:

| Arquivo | Conteúdo |
|---|---|
| instalador (`.exe`) | o app para Windows |
| `manifest.json` | versão, canal, notas da versão e SHA-256 do instalador |
| `manifest.sig` | assinatura do `manifest.json` |

Exemplo de `manifest.json`:

```json
{
  "app": "nexo-ai",
  "version": "0.5.1",
  "channel": "stable",
  "published": "2026-09-29",
  "installer": { "file": "NEXO-AI-0.5.1-x64.exe", "sha256": "<hash>" },
  "notes": [
    { "type": "new", "text": "Leitura do Claude mais rápida", "authors": ["claude", "rodrigo"], "explainedBy": "claude" }
  ]
}
```

## Segurança

- Os apps baixam o manifesto, conferem a **assinatura** com a chave pública embutida e o **SHA-256** do instalador. Se qualquer conferência falhar, nada é instalado.
- Antes de instalar, o app faz backup dos dados; a versão anterior fica guardada por 30 dias e o app volta para ela se o primeiro início falhar.
- A chave privada de assinatura nunca é publicada aqui.

## Canais

- `stable`: versões liberadas para todos.
- `candidate`: versões de teste, só para quem escolheu esse canal no app.
