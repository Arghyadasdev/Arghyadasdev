# Place this file at: .github/workflows/snake.yml
# inside your Arghyadasdev/Arghyadasdev profile repo

name: Generate Snake Animation

on:
  schedule:
    # Runs every day at midnight UTC
    - cron: "0 0 * * *"
  workflow_dispatch: # Allows manual trigger from GitHub Actions tab

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10

    steps:
      - name: Generate snake animation
        uses: Platane/snk@v3
        with:
          github_user_name: Arghyadasdev
          outputs: |
            dist/github-snake.svg
            dist/github-snake-dark.svg?palette=github-dark

      - name: Push snake to output branch
        uses: crazy-max/ghaction-github-pages@v3
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
