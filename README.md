# 💰 Finanças Pessoais

Aplicativo de controle financeiro pessoal — 100% client-side, sem dependências, funciona direto no navegador.

## Features

- **Tracker mensal** — acompanhe receitas e despesas mês a mês com navegação por setas
- **Dois períodos** — organize contas do Dia 15 e do Fim do Mês em abas separadas
- **Receitas e despesas pontuais** — adicione entradas avulsas diretamente no tracker
- **Recorrência no cadastro** — ao adicionar uma conta, escolha se ela é 🔁 Recorrente (aparece todo mês) ou 1× Pontual
- **Check de pagamento** — marque itens como pagos/recebidos com um toque
- **Edição inline de valores** — altere o valor real diretamente na linha
- **Resumo automático** — cards de Renda, Gastos e Saldo atualizados em tempo real
- **Contas Recorrentes** — gerencie os templates que populam novos meses automaticamente
- **Relatório mensal** — tabela histórica com gráfico de barras de gastos por mês
- **PWA** — pode ser instalado na tela inicial do celular (Android/iOS)
- **Persistência local** — todos os dados ficam no `localStorage` do navegador, sem servidor

## Como usar

Abra o arquivo `index.html` diretamente no navegador — não precisa de servidor, build ou instalação.

```bash
# Opção 1: abrir direto
open index.html

# Opção 2: servir localmente (evita restrições de Service Worker)
npx serve .
# ou
python3 -m http.server 8080
```

> Para instalar como PWA (ícone na tela inicial), use a opção de servidor local — o Service Worker não funciona via `file://`.

## Estrutura de dados

Os dados ficam no `localStorage` com as seguintes chaves:

| Chave | Conteúdo |
|---|---|
| `fin:m:YYYY-MM` | Dados do mês (receitas + despesas) |
| `fin:tpl` | Templates de contas recorrentes |

### Formato de um mês (`fin:m:YYYY-MM`)

```json
{
  "income": [
    { "id": "abc123", "name": "Salário", "period": "fim", "actual": 3755.08, "done": false, "isExtra": false }
  ],
  "expenses": [
    { "id": "def456", "name": "Internet", "period": "15", "actual": 89.99, "done": true, "isExtra": false, "recurring": true }
  ]
}
```

- `period`: `"15"` (vence dia 15) ou `"fim"` (vence fim do mês)
- `done`: `true` = pago/recebido
- `isExtra`: `true` = item pontual adicionado manualmente (exibe badge `1×` e botão de remover)
- `recurring`: `true` = aparece automaticamente em novos meses

## Períodos

| Período | Quando usar |
|---|---|
| **Dia 15** | Contas com vencimento na primeira quinzena (cartões, financiamentos, seguros) |
| **Fim do Mês** | Contas com vencimento no final do mês (aluguel, escola, energia) |

## Tecnologias

- HTML5 + CSS3 + JavaScript puro (zero dependências)
- `localStorage` para persistência
- `Intl.NumberFormat` para formatação em BRL
- Service Worker + Web App Manifest para PWA

## Licença

Uso pessoal.
