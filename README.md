<div align="center">

<img src="docs/logo.png" width="96" alt="iRedResolution">

# iRedResolution

**Acabe com o alt-tab lento do CS2 — sem trocar para tela cheia em janela.**

Troca a resolução do monitor *antes* do jogo abrir e restaura ao fechar.
Alt-tab instantâneo mantendo a latência do modo exclusivo.

[![Download](https://img.shields.io/badge/Download-iRedResolution.exe-FF2325?style=for-the-badge)](../../releases/latest)
[![Windows](https://img.shields.io/badge/Windows-7%20a%2011-1E1E1E?style=for-the-badge&logo=windows)](#requisitos)
[![Discord](https://img.shields.io/badge/Discord-Comunidade-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/DQ8TzaFGtd)

*390 KB · arquivo único · sem instalação · sem dependências*

<img src="docs/01-principal.png" width="380" alt="Janela principal">

</div>

---

## O problema

Se você joga CS2 numa resolução diferente da área de trabalho — 4:3 esticado,
por exemplo — conhece o sintoma: cada alt-tab vira **preto → cinza → preto** e
trava tudo por segundos. Às vezes a tela nem volta.

Não é bug do jogo. Em tela cheia exclusiva, o CS2 toma posse do display e define
o modo de vídeo. Se esse modo for diferente do modo do desktop, **cada alt-tab
força o Windows a trocar a resolução do sistema inteiro** — e a trocar de volta
ao retornar.

A resposta usual é *"usa borderless"*. Resolve o alt-tab, mas coloca o
compositor do Windows no caminho e **adiciona latência de entrada**. É por isso
que praticamente todo profissional continua no exclusivo.

## A solução

O iRedResolution inverte o problema. Em vez de mudar o jogo, muda o **desktop**:

```
1. desktop  ->  resolução do jogo
2. aguarda o Windows re-enumerar os displays
3. abre o jogo          <- só agora
4. ao fechar            ->  restaura tudo
```

Desktop e jogo na mesma resolução significa **zero troca de modo**. Alt-tab
instantâneo *e* latência mínima do exclusivo. Não é um meio-termo — são as duas
vantagens juntas.

---

## Recursos

| | |
|---|---|
| **Ordem correta** | Troca a resolução antes de lançar, que é o ponto central |
| **MODO GC** | Aplica a resolução e espera — para GamersClub, FACEIT e outros launchers |
| **Detecção automática** | Vigia os processos e age sozinho |
| **Multi-monitor** | Lista todos os displays, marca o principal |
| **Filtro por proporção** | 4:3, 16:9, 16:10, 5:4 |
| **Taxa de atualização** | Só os Hz realmente suportados pela resolução escolhida |
| **Restauração garantida** | O desktop volta mesmo se o app for morto |
| **Monitores virtuais** | Detecta Sunshine/Parsec/spacedesk e desativa durante o jogo |
| **Bandeja do sistema** | Discreto ao lado do relógio |
| **Presets** | CS2, Valorant, Apex, Dota 2, TF2, Rocket League, personalizado |
| **Tutorial embutido** | Escala da GPU passo a passo, por fabricante |
| **Portátil** | Um .exe. Roda de pendrive. Nada no registro. |

## MODO GC — quando o launcher é de outra pessoa

GamersClub e FACEIT têm anticheat e launcher próprios: o botão "Jogar" fica no
site deles. O iRedResolution não pode abrir o jogo — e só reagir quando o
processo aparece não adianta, porque a troca de resolução precisa acontecer
**antes** do jogo subir.

O **MODO GC** inverte o controle:

```
1. clique em MODO GC     ->  resolução aplicada agora
2. o programa espera         (não abre nada, fica na bandeja)
3. clique em Jogar na GC     (normal, como sempre)
4. ao fechar o CS2       ->  resolução restaurada sozinha
```

Manual na abertura, automático no fechamento. Se desistir, o botão vira
CANCELAR; e após 15 minutos sem o jogo abrir, restaura por conta própria.

Para quem prefere que seja **tudo** automático, existe a opção *Detectar o jogo
automaticamente*: o programa vigia os processos listados e age sozinho — mas
nesse caso a resolução só troca depois do jogo já ter aberto.

### Monitores virtuais

Drivers como **Sunshine**, **Parsec**, **SudoMaker** e **spacedesk** criam
displays que o Windows trata como reais. Cada troca de resolução obriga o
sistema a re-enumerar todos eles — a maior causa isolada de alt-tab lento em
quem faz streaming local.

O app identifica esses displays, avisa, e com sua autorização os **desanexa**
enquanto o jogo roda, reanexando ao fechar. Não mexe no driver, não desinstala
nada, não pede administrador.

---

## Requisito: escala pela GPU

> **Leia isto se for usar resolução menor que a nativa do monitor.**

Sem a escala configurada, uma resolução menor aparece pequena no centro da tela
com tarjas pretas em volta. É configuração do driver de vídeo, não do programa.

**NVIDIA** — botão direito na área de trabalho → Painel de Controle NVIDIA →
Monitor → *Ajustar o tamanho e a posição da área de trabalho*

- Escala: **Tela inteira**
- Executar escala em: **GPU**
- Marcar **Substituir o modo de escala definido por jogos e programas**

O app traz o tutorial completo (NVIDIA, AMD e Intel) com botão que abre o painel
do fabricante direto:

<div align="center">
<img src="docs/05-tutorial-escala.png" width="440" alt="Tutorial da escala">
</div>

---

## Como usar

1. Baixe o `iRedResolution.exe` em [Releases](../../releases/latest)
2. Execute — não precisa instalar
3. Escolha monitor, proporção, resolução e Hz
4. Confira o comando do jogo e o nome do processo (já vem pronto para CS2)
5. Clique em **JOGAR** — ou em **MODO GC**, se for jogar pela GamersClub

Fechar no X manda para a bandeja. Para sair de vez: botão direito no ícone → Sair.

---

## Este software NÃO é um cheat

<img src="docs/02-ajuda.png" width="420" align="right" alt="Aviso legal">

- **NÃO** é cheat, hack, trainer ou aimbot
- **NÃO** lê, escreve nem injeta em memória de outros processos
- **NÃO** altera arquivos de jogo
- **NÃO** intercepta rede
- **NÃO** instala serviço ou driver
- **NÃO** pede administrador
- **NÃO** coleta dados

Usa exclusivamente APIs públicas de vídeo do Windows
(`ChangeDisplaySettingsEx`, `EnumDisplaySettings`, `EnumDisplayDevices`) — as
mesmas da tela de Configurações do Windows — e inicia o jogo pelo atalho normal
do sistema.

Compatível com **VAC, FACEIT, ESEA e Vanguard**, por não tocar em nada
relacionado ao jogo.

<br clear="right">

---

## Alerta de antivírus / SmartScreen

O executável **não tem assinatura digital paga** (certificado de code signing é
caro e cobrado por ano). O Windows pode exibir *"O Windows protegeu o
computador"*.

Isso **não indica vírus** — indica apenas que o arquivo é novo e não tem editor
verificado. Clique em **Mais informações → Executar assim mesmo**.

O que foi feito para reduzir falso-positivo:

- Manifesto `asInvoker` — não pede elevação (pedir admin sem necessidade é um
  dos maiores gatilhos de alerta)
- Metadados completos de versão, produto e direitos
- Nenhuma escrita em pastas de sistema ou no registro
- Verificado contra o Microsoft Defender: **limpo**

### Verificando a integridade

O app calcula e exibe o **SHA-256 de si mesmo**, com botão de copiar:

<div align="center">
<img src="docs/02-ajuda.png" width="440" alt="Aba de integridade">
</div>

Compare com o hash publicado na release. Ou confira por conta própria:

```powershell
Get-FileHash .\iRedResolution.exe -Algorithm SHA256
```

---

## Requisitos

- Windows 7 ou superior (testado em Windows 10 e 11)
- .NET Framework 4.0+ — já presente em qualquer Windows moderno

Preferências em `%AppData%\iRedResolution\config.ini`. Nada no registro.

---

## Compilando

Não precisa de Visual Studio — o compilador C# já vem no Windows:

```powershell
$csc = "C:\Windows\Microsoft.NET\Framework64\v4.0.30319\csc.exe"
& $csc -target:winexe -optimize+ -nowarn:0108 `
  -out:iRedResolution.exe -win32icon:src\app.ico -win32manifest:src\app.manifest `
  -resource:src\logo.png,logo.png -resource:src\app.ico,app.ico -resource:src\discord.png,discord.png `
  -reference:System.dll -reference:System.Drawing.dll -reference:System.Windows.Forms.dll -reference:System.Core.dll `
  src\CS2Launcher.cs src\Gui.cs src\Scaling.cs src\About.cs src\AssemblyInfo.cs
```

| Arquivo | Responsabilidade |
|---|---|
| `CS2Launcher.cs` | P/Invoke de display, enumeração de modos, persistência |
| `Gui.cs` | Janela principal, bandeja, MODO GC, detecção de virtuais |
| `Scaling.cs` | Tutorial da escala por fabricante |
| `About.cs` | Ajuda, aviso legal, hash próprio, links |

---

## Comunidade

[Site](https://iredhub.com) ·
[Twitch](https://twitch.tv/iRedbrine) ·
[YouTube](https://youtube.com/@Redbrine) ·
[Discord](https://discord.gg/DQ8TzaFGtd) ·
[Kick](https://kick.com/iRedbrine) ·
[TikTok](https://tiktok.com/@iRedbrine) ·
[Instagram](https://instagram.com/iRedbrine) ·
[X](https://x.com/Red_Brine) ·
[Steam](https://steamcommunity.com/id/iRedbrine)

---

## Licença

Copyright © 2026 iRedHUB / Redbrine. Todos os direitos reservados.

Fornecido no estado em que se encontra, sem garantias de qualquer natureza.
O uso é por sua conta e risco.
