🛡️ Main Guardian Agent
Proteja a sua branch main com a ajuda da IA Gemini, analisando mudanças propostas em Pull Requests e recebendo comentários automáticos com insights, sugestões de melhorias e detecção de potenciais problemas.

📋 O que essa action faz?
Esta GitHub Action analisa as diferenças entre a branch principal (main) e as mudanças propostas em uma Pull Request usando a API do Google Gemini. Ela:

Compara os arquivos alterados no PR com a versão atual na main

Envia essas diferenças para o Gemini com instruções específicas

Recebe um relatório com:

Detecção de bugs e vulnerabilidades

Sugestões de refatoração

Avaliação do impacto das alterações

Score de aprovação de 0 a 10

Comenta automaticamente o relatório no próprio PR

🚀 Como usar
Adicione a action ao seu workflow YAML dentro de .github/workflows/:

yaml
Copiar
Editar
name: Analyse PR with Main Guardian Agent

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  guardian-analysis:
    runs-on: ubuntu-latest

    steps:
      - name: Run Main Guardian Agent
        uses: Ispx/Main-Guardian@v1.0.7
        with:
          gemini-api-key: ${{ secrets.GEMINI_API_KEY }}
          github-token: ${{ secrets.GITHUB_TOKEN }}
🔐 Inputs

Nome	Descrição	Obrigatório	Padrão
gemini-api-key	Sua chave de API do Google Gemini.	✅ Sim	-
github-token	Token do GitHub com permissão de leitura/escrita no repositório.	✅ Sim	${{ github.token }}
🛠️ Requisitos
A action espera que as ferramentas jq e curl estejam instaladas no runner (no GitHub-hosted já vêm por padrão).

🧠 O que a IA analisa?
A IA Gemini é orientada com as seguintes instruções:

Avaliar possíveis bugs, quebras de funcionalidades, ou vulnerabilidades

Sugerir melhorias e refatorações

Emitir um score de aprovação (0 a 10) — caso encontre problemas críticos, o score será 0

Gerar relatório em formato Markdown com ícones para cada tipo de análise (💥 bugs, 🔐 vulnerabilidades, 🧼 refatorações etc.)