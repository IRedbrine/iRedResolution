# iRedResolution — documento de referência

> Documento-fonte para o canal `#ired-resolution` no Discord, publicação no
> site e material de divulgação.
> Versão 1.0 · Copyright © 2026 iRedHUB / Redbrine.

---

## Resumo em uma linha

Utilitário gratuito que troca a resolução do monitor **antes** do jogo abrir e
restaura ao fechar, eliminando o alt-tab lento do CS2 sem abrir mão da latência
do modo tela cheia exclusivo — e ainda traz diagnóstico do PC, gerenciador da
config do CS2 e saturação por jogo.

---

## O problema que ele resolve

Quem joga CS2 numa resolução diferente da área de trabalho — o caso clássico é
4:3 esticado, tipo 1280×960 num monitor 1920×1080 — conhece o sintoma: cada
alt-tab vira uma sequência de **preto → cinza → preto** que trava tudo por
vários segundos. Às vezes a tela nem volta.

A causa não é bug do CS2. Em tela cheia exclusiva o jogo toma posse do display
e define o modo de vídeo. Se esse modo for diferente do modo da área de
trabalho, **cada alt-tab força o Windows a trocar a resolução do sistema
inteiro** — e a trocar de volta ao retornar. Isso foi confirmado com vídeo: o
monitor perde sinal e re-sincroniza por cerca de 0,17s a cada troca de foco.

### A solução convencional, e por que ela não serve

A resposta usual da comunidade é "usa tela cheia em janela (borderless)". Isso
resolve o alt-tab, mas introduz o compositor do Windows no caminho, o que
adiciona latência de entrada — perceptível para quem joga a sério, e o motivo
de praticamente todo profissional continuar no exclusivo.

### O que o iRedResolution faz

Inverte a ordem do problema. Em vez de mudar o jogo, ele muda o **desktop**:

1. Coloca a área de trabalho na mesma resolução que o jogo vai usar
2. Espera o Windows re-enumerar os displays
3. **Só então** abre o jogo
4. Monitora o processo e, ao fechar, devolve tudo ao estado anterior

Com desktop e jogo na mesma resolução, não existe troca de modo — o alt-tab fica
instantâneo **e** você mantém o exclusivo com a latência mínima. Testado no
mundo real: **zero piscadas, zero travadas**.

---

## Tudo que o programa faz

### Resolução e alt-tab

| Recurso | O que faz |
|---|---|
| **JOGAR** | Troca a resolução do desktop, abre o jogo e restaura ao fechar |
| **MODO GC** | Aplica a resolução e espera — para GamersClub, FACEIT e outros launchers que abrem o jogo por fora |
| **Detecção automática** | Vigia os processos e age sozinho, sem clicar em nada |
| **Seleção de monitor** | Lista todos os displays, marca o principal |
| **Filtro por proporção** | 4:3, 16:9, 16:10, 5:4 — só as resoluções que interessam |
| **Taxa de atualização** | Lista os Hz realmente suportados pela resolução escolhida |
| **Restauração garantida** | O desktop volta mesmo se o app travar ou for morto |
| **Monitores virtuais** | Detecta Sunshine/Parsec/spacedesk e desativa durante o jogo |

### Otimização do PC (botão OTIMIZAR O PC)

Analisa vídeo, sistema, rede, hardware e estabilidade, lista o que dá para
melhorar e deixa **você escolher** o que aplicar — nada é alterado sem marcar.
Cada item tem um **selo de confiança**:

- **COMPROVADO** — problema documentado, correção conhecida (ex: MPO desligando o alt-tab piscando).
- **PROVÁVEL** — relatos consistentes, sem prova formal (ex: HAGS, tela cheia exclusiva).
- **EXPERIMENTAL** — citado em fóruns, sem evidência sólida — vem desmarcado.
- **INFO** — só reporta, sem correção automática (ex: RAM fora de spec, reinícios do sistema).

Cobre MPO, HAGS, Game DVR, aceleração do mouse, MSI mode da GPU, estado mínimo
da CPU, e detecta acúmulo de drivers de áudio/antivírus (a causa de travadinha
por DPC). **Tudo é reversível** pelo botão DESFAZER — inclusive o plano de
energia.

### Config de vídeo do CS2 (botão CFG DO CS2)

Encontra o Steam e **todos os perfis** com CS2 instalado, e grava o
`cs2_video.txt` em todos de uma vez — útil para quem tem mais de uma conta.
Serve para as opções que **o menu do jogo não mostra**, como
`fullscreen_min_on_focus_loss`. Faz backup do original antes, trava o arquivo
como somente-leitura (o CS2 reescreve ao sair) e tem **RESTAURAR ORIGINAL** que
devolve tudo, inclusive o cadeado.

### Saturação por jogo

Aumenta a saturação (Digital Vibrance da NVIDIA) **só enquanto o jogo está em
foco** — ao dar alt-tab, a área de trabalho volta ao normal na hora. Cada jogo
guarda o seu nível (CS2 e Valorant não dividem o mesmo), e por padrão mexe só no
monitor do jogo, com opção de aplicar em todos. Aposenta o VibranceGUI.

### Conveniências

- **Iniciar com o Windows** (na bandeja), sem precisar criar atalho na mão.
- **Bandeja do sistema** — roda discreto ao lado do relógio.
- **Presets de jogos** — CS2, Valorant, Apex, Dota 2, TF2, Rocket League e personalizado.
- **Tutorial de escala** — passo a passo por fabricante (NVIDIA, AMD, Intel), com botão que abre o painel.
- **Portátil** — um único .exe, sem instalação, sem dependências.

---

## Apoie o projeto (botão APOIAR O PROJETO)

O iRedResolution é **gratuito e sem anúncios**. Quem quiser ajudar a manter o
projeto vivo pode doar via **PIX / LivePix**:

- Um **QR code** embutido no programa (funciona offline e para mostrar em live).
- Um botão que abre a página de doação no navegador.

Link direto: `widget.livepix.gg/embed/ecc5b854-5173-431c-a590-955cecdd2966`

Não pode doar? Divulgar para a galera do CS2, deixar estrela no GitHub, seguir
os canais e reportar bugs no Discord ajuda tanto quanto.

---

## Este software NÃO é um cheat

Vale deixar explícito, porque é um utilitário para jogos:

- **NÃO** é cheat, hack, trainer, aimbot ou vantagem competitiva.
- **NÃO** lê, escreve nem injeta nada na memória de outros processos.
- **NÃO** altera arquivos de jogo (só o `cs2_video.txt`, que é config, com backup).
- **NÃO** intercepta rede, não coleta dados, não tem telemetria.
- **NÃO** pede administrador para rodar (só sob demanda, para ajustes de registro).

Usa exclusivamente APIs públicas e documentadas do Windows
(`ChangeDisplaySettingsEx`, `EnumDisplaySettings`, `SetWinEventHook` sem injeção)
e a NVAPI oficial da NVIDIA para a saturação.

Passou por **auditoria de segurança** (ver `AUDITORIA-SEGURANCA.md`): nenhuma
API de injeção, URLs todas fixas, verificado limpo contra o Microsoft Defender.
Por não tocar no jogo, é compatível com **VAC, FACEIT, ESEA e Vanguard**.

---

## Sobre alertas de antivírus

O executável **não tem assinatura digital paga** (certificado de code signing é
caro e cobrado por ano). Por isso o Windows pode exibir *"O Windows protegeu o
computador"* (SmartScreen). Isso **não indica vírus** — só que o arquivo é novo
e não tem editor verificado. Para executar: **Mais informações → Executar assim
mesmo**.

O app calcula e exibe o **SHA-256 de si mesmo** na aba INTEGRIDADE, para
qualquer um conferir que o arquivo não foi modificado.

---

## Requisitos

- Windows 7 ou superior (testado em Windows 10 e 11).
- .NET Framework 4.0+ — já presente em qualquer Windows moderno.
- Saturação: placa **NVIDIA** (o recurso aparece desabilitado em outras).
- Nenhuma instalação: arquivo único, portátil, roda de pendrive.

Preferências ficam em `%AppData%\iRedResolution`. Nada é gravado fora dali além
dos ajustes que você escolhe aplicar (todos reversíveis).

---

## Como usar (o básico)

1. Abra o `iRedResolution.exe`.
2. Escolha o monitor, a proporção, a resolução e os Hz.
3. Confira o comando do jogo e o nome do processo (já vem pronto para CS2).
4. Clique em **JOGAR** — ou em **MODO GC** se for jogar pela GamersClub.

Fechar no X manda para a bandeja; para sair de vez, botão direito no ícone → Sair.

---

## Detalhes técnicos

- **Linguagem:** C# / .NET Framework 4.x, WinForms, controles desenhados à mão.
- **Tamanho:** ~477 KB, arquivo único, sem dependências externas.
- **APIs:** `ChangeDisplaySettingsEx`, `EnumDisplaySettings`, `EnumDisplayDevices`,
  `SetWinEventHook` (sem injeção), NVAPI (Digital Vibrance), `powercfg`.
- **Reversibilidade:** registro (por chave), plano de energia (powercfg),
  `cs2_video.txt` (backup) — tudo desfazível.

---

## Comunidade

| | |
|---|---|
| Site | [iredhub.com](https://iredhub.com) |
| Twitch | [twitch.tv/iRedbrine](https://twitch.tv/iRedbrine) |
| YouTube | [youtube.com/@Redbrine](https://youtube.com/@Redbrine) |
| Discord | [discord.gg/DQ8TzaFGtd](https://discord.gg/DQ8TzaFGtd) |
| Kick | [kick.com/iRedbrine](https://kick.com/iRedbrine) |
| TikTok | [tiktok.com/@iRedbrine](https://tiktok.com/@iRedbrine) |
| Instagram | [instagram.com/iRedbrine](https://instagram.com/iRedbrine) |
| X | [x.com/Red_Brine](https://x.com/Red_Brine) |
| Steam | [steamcommunity.com/id/iRedbrine](https://steamcommunity.com/id/iRedbrine) |

---

## Licença

Copyright © 2026 iRedHUB / Redbrine. Todos os direitos reservados.
Software proprietário — ver `LICENCA.txt`. Fornecido no estado em que se
encontra, sem garantias. O uso é por sua conta e risco.
