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

Exemplo de `manifest.json` (os apps conferem o formato antes de usar; com o SHA-256 real do instalador no lugar do texto entre `< >`, este exemplo passa na conferência):

```json
{
  "app": "nexo-ai",
  "version": "0.5.1",
  "channel": "stable",
  "published": "2026-09-29",
  "publishedBy": "claude",
  "installer": { "file": "NEXO-AI-0.5.1-x64.exe", "sha256": "<64 caracteres hexadecimais>" },
  "notes": [
    { "type": "new", "text": "Leitura do Claude mais rápida", "authors": ["claude", "rodrigo"] }
  ]
}
```

- `publishedBy`: quem executou a publicação (`rodrigo`, `claude` ou `codex`).
- `notes[].authors`: o primeiro é o autor principal, que explica o item; os demais são coautores.

### Versão obrigatória e versão mínima

As duas impedem o app de abrir e são independentes. As duas exigem o pedido explícito do Rodrigo, registrado em `blockRequestedBy`, e um motivo escrito, que aparece para a pessoa.

```json
{
  "blockRequestedBy": "rodrigo",
  "mandatory": { "reason": "Corrige leitura errada do Claude", "from": "2026-10-03T18:00:00-03:00" },
  "minVersion": "0.5.0",
  "minVersionReason": "Formato de dados novo"
}
```

- `mandatory.from`: a partir de quando a versão é obrigatória. Data e hora completas **com fuso**. Até lá, a pessoa vê um aviso importante.
- `mandatory.immediate: true`: obrigatória na hora, **só para falha grave de segurança**, no lugar de `from`. Sem uma das duas, o manifesto é recusado.
- `minVersion`: abaixo dela o app não abre. Não pode ser maior que `version`. Abaixo da mínima aparece só `minVersionReason`.

## Segurança

- Os apps baixam o manifesto, conferem a **assinatura** com a chave pública embutida e o **SHA-256** do instalador. Se qualquer conferência falhar, nada é instalado.
- Antes de instalar, o app faz backup dos dados; a versão anterior fica guardada por 30 dias e o app volta para ela se o primeiro início falhar.
- A chave privada de assinatura nunca é publicada aqui.

## Canais

- `stable`: versões liberadas para todos.
- `rc`: versões candidatas, só para testadores convidados que escolheram esse canal no app.
