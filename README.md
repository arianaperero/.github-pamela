name: Qodana

on:
  push:
  pull_request:

jobs:
  qodana:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Qodana Scan
        uses: JetBrains/qodana-action@v2025.2.1
        with:
          args: ""
          results-dir: ${{ runner.temp }}/qodana/results
          cache-dir: ${{ runner.temp }}/qodana/caches
          use-caches: true
          primary-cache-key: qodana-2025.2-${{ github.ref }}-${{ github.sha }}
          additional-cache-key: qodana-2025.2-${{ github.ref }}
          cache-default-branch-only: false
          upload-result: false
          artifact-name: qodana-report
          use-annotations: true
          pr-mode: true
          post-pr-comment: true
          github-token: ${{ github.token }}
          push-fixes: none
          commit-message: "🤖 Apply Qodana quick-fixes"
          use-nightly: false

