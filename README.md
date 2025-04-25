name: Main Guardian

# Aciona o workflow em eventos de pull request direcionados à branch 'main'
on:
  pull_request:
    branches:
      - main # Ou a(s) branch(es) que você deseja proteger

# Define as permissões necessárias para o job
permissions:
  contents: read
  pull-requests: write

jobs:
  analyze_code_changes:
    name: Analisar Alterações do PR
    runs-on: ubuntu-latest
    steps:
      - name: Executar Análise do Guardião da Main
        uses: Ispx/Main-Guardian@v1.0.1
        with:
          gemini-api-key: ${{ secrets.GEMINI_API_KEY }}
          github-token: ${{ secrets.MY_PAT }}