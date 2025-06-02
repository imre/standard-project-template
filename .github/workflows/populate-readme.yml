name: Populate README

on:
  push:
    paths:
      - '.project'
      - 'README.md'

jobs:
  populate:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.x'

      - name: Install dependencies
        run: pip install python-dotenv

      - name: Replace placeholders in README
        run: python .github/scripts/populate_readme.py

      - name: Commit updated README
        run: |
          git config --global user.name "readme-bot"
          git config --global user.email "actions@github.com"
          git add README.md
          git commit -m "Auto-populated README from .project" || echo "No changes to commit"
          git push

