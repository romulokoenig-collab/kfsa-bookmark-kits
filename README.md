# KFSA Bookmark Kits

Kits de bookmarks padrão por OU (Organizational Unit) do Workspace KFSA.

Consumido por `sync-bookmarks.py` (instalado em todos os notebooks via setup-notebook) que roda no logon do Windows.

## OUs

| OU | Arquivo | Bookmarks |
|---|---|---|
| Jurídico | `jsons/juridico.json` | 58 |
| Suporte | `jsons/suporte.json` | 59 |
| Comercial | `jsons/comercial.json` | 50 |
| Financeiro | `jsons/financeiro.json` | 49 |
| Admin | `jsons/admin.json` | 105 |

## Comportamento de sync (merge aditivo)

- **Bookmarks do kit** que o colaborador deletou → repostos no logon (no final, pra não bagunçar a ordem dele)
- **Bookmarks que o colaborador adicionou** → preservados sempre
- **Pastas do kit** atualizadas se o nome bater; novas pastas criadas se não existirem
- **OU detectada** via Service Account + Domain-Wide Delegation no logon (auto-sync com Workspace)

## Estrutura do JSON

Cada arquivo é uma lista do tipo:

```json
[
  {"toplevel_name": "Nome da Pasta KFSA"},
  {"name": "Gmail", "url": "https://mail.google.com"},
  {
    "name": "Sistemas",
    "children": [
      {"name": "Kommo", "url": "https://kfsa.kommo.com"}
    ]
  }
]
```

O primeiro item com `toplevel_name` é metadata (nome da pasta raiz no Bookmark Bar). Demais itens são bookmarks ou pastas (com `children` recursivo).

## Como atualizar

1. Editar JSON da OU no GitHub (web ou local)
2. Commit + push
3. No próximo logon de qualquer colaborador da OU, o sync aplica as mudanças

**Não precisa** rodar deploy. Tudo flui via GitHub raw URLs públicas.
