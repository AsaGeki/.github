# .github

Arquivos padrão da conta `AsaGeki`. O GitHub aplica o que está aqui a todo repositório da conta, privado inclusive, que não tenha o próprio arquivo.

O repositório é público porque o GitHub exige isso para arquivos padrão de conta pessoal. Nada sensível entra aqui.

## O que há

| Caminho | O que é |
| --- | --- |
| `.github/pull_request_template.md` | Template de PR padrão. |
| `.github/ISSUE_TEMPLATE/` | Formulários de bug e ideia. Sem `labels:`, porque a label precisa existir em todo repositório que usar o template. |
| `.github/workflows/ci-node.yml` | CI reutilizável de projeto Node com pnpm. |
| `.github/workflows/ci-python.yml` | CI reutilizável de projeto Python com uv, ruff e ty. |
| `.github/workflows/ci-tauri.yml` | CI reutilizável de projeto Tauri (Rust e TypeScript com bun), em `windows-latest`. |
| `.github/workflows/padrao-pr.yml` | Confere título do PR em Conventional Commits e nome da branch. |

## Como um projeto usa o CI

```yaml
jobs:
  ci:
    uses: AsaGeki/.github/.github/workflows/ci-node.yml@main
    with:
      run-tests: true
```

O projeto precisa expor os scripts que o workflow chama: `typecheck`, `lint`, `format:check` e `build` (e `test`, se `run-tests`) no Node; `ruff` e `ty` no grupo `dev` do Python; `typecheck`, `lint` e `format:check` na raiz mais o crate Rust no Tauri.

`CODEOWNERS`, workflows e licença não são herdados pelo GitHub. Quem cria o projeto é o `novo-projeto.ps1` do repositório `projeto-base`.
