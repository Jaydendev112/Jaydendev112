<p align="center">
  <a href="https://github.com/khrlmstfa/readme-typing-svg"><img src="https://readme-typing-svg.herokuapp.com?lines=𝐈𝐦+𝐣𝐮𝐬𝐭+𝐍𝐨𝐨𝐛;𝐁𝐮𝐭+𝐈+𝐖𝐢𝐥𝐥+𝐊𝐞𝐞𝐩+𝐋𝐞𝐚𝐫𝐧𝐢𝐦𝐠;𝐈%20|%20𝐋𝐢𝐤𝐞%20|%20𝐂𝐨𝐝𝐢𝐧𝐠%20:);𝐥𝐞𝐭'𝐬%20𝐬𝐭𝐮𝐝𝐲;𝐓𝐨𝐠𝐞𝐭𝐡𝐞𝐫%2😊%20:)%20:)&center=true&width=500&height=50"></a>
</p>

name: Generate snake animation

on:
  schedule: # execute every 12 hours
    - cron: "* */12 * * *"

  workflow_dispatch:

  push:
    branches:
    - main

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
      - name: generate snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: dist/snake.svg?palette=github-dark


      - name: push snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
