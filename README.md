# Catálogo de mods do Block Miner

Este repositório é o **catálogo online** que aparece no jogo em **Mods → Catálogo**.
O jogo lê o [`index.json`](index.json) e baixa só o mod que o jogador escolher (nunca todos).
Antes de instalar, o jogo confere o **sha256** e o tamanho de cada arquivo: se não baterem, o mod é recusado.

## Mods disponíveis

| Mod | Versão | O que faz |
|---|---|---|
| Blocos de Cores | 1.0.0 | Azulejos esmaltados em 8 cores, com lajes e escadas |
| Engenho | 0.3.0 | Máquinas movidas a rotação: eixos, engrenagens, motores, mó, rolos trituradores, prensa, batedeira + tacho, ventoinha, funis e esteiras com itens; novo: fluidos (canos, bomba, tanques, ralo, bico dosador; garapa, chocolate, café, leite), queimador superaquecido, funil de bronze com filtro e braço robótico |
| Lanternas | 1.1.0 | Lanterna de papel e luminária de vidro fosco (luz 15) |

## Como publicar um mod novo ou uma versão nova

No repositório do jogo, com a pasta do mod pronta (`mod.json`, `data/`, `assets/`):

```
python tools\modkit\bmmodkit.py validate <pasta-do-mod>
python tools\modkit\bmmodkit.py pack <pasta-do-mod> -o "<este repositório>\mods"
cd "<este repositório>"
python "<repo do jogo>\tools\modkit\bmmodkit.py" index mods\*.bmmod --base-url "https://raw.githubusercontent.com/Gabriel9536/mygamemods/main/mods" --name "Catálogo oficial do Block Miner" -o index.json
git add . && git commit -m "mod: <nome> <versão>" && git push
```

Regras:
- Um arquivo `.bmmod` publicado **nunca é alterado**: uma versão nova gera um arquivo novo (`<id>-<versão>.bmmod`).
- O `index.json` é sempre gerado pelo `bmmodkit.py` (ele calcula o sha256 e o tamanho).
- Mods só de dados e arte (sem programas `.dll`/`.exe`; o jogo recusa).
