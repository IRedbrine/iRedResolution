# iRedResolution — documento de referência

> Base para o canal do Discord, o site e o material de divulgação.
> Versão 1.2 · Copyright © 2026 iRedHUB / Redbrine.

## Resumo em uma linha

Utilitário gratuito que troca a resolução do monitor **antes** do jogo abrir e restaura ao fechar, para reduzir o alt-tab lento do CS2 mantendo a tela cheia exclusiva.

## O problema

Quem joga numa resolução diferente da área de trabalho, como 1280x960 num monitor 1920x1080, pode ver **preto → cinza → preto** a cada alt-tab. Em tela cheia exclusiva, o jogo define o modo de vídeo; se ele for diferente do modo da área de trabalho, o monitor pode perder o sinal e sincronizar de novo. No PC usado no desenvolvimento, isso foi visto em vídeo, com cerca de 0,17 s de tela preta por troca.

## O que o iRedResolution faz

1. Coloca a área de trabalho na resolução que o jogo vai usar.
2. Abre o jogo.
3. Ao fechar o jogo, devolve a resolução anterior.

No PC usado no desenvolvimento, as piscadas sumiram mantendo o modo exclusivo. **O resultado pode variar.** Driver, monitor e programas abertos também influenciam. Programas que reaplicam saturação a cada troca de foco, por exemplo, podem causar piscadas.

## Recursos

### Resolução e alt-tab

| Recurso | O que faz |
|---|---|
| **JOGAR** | Troca a resolução, abre o jogo e restaura ao fechar |
| **MODO GC** | Aplica a resolução e espera, para launchers como GamersClub e FACEIT |
| **Detecção automática** | Vigia os processos; nesse modo, a resolução só troca depois do jogo abrir |
| **Monitores** | Lista os monitores e reconhece o escolhido mesmo se o Windows renumerá-los |
| **Modos reais** | Mostra as resoluções e os Hz informados pelo monitor |
| **Restauração** | Volta ao fechar o jogo. Se o app ou o PC cair, volta quando o app abrir de novo |
| **Monitores virtuais** | Detecta Sunshine, Parsec, spacedesk e similares, e pergunta antes de desativá-los no jogo |

### OTIMIZAR O PC

Analisa vídeo, sistema, rede, hardware e estabilidade. Nada muda sem você marcar e confirmar, e alguns ajustes pedem administrador.

- **COMPROVADO:** mecanismo documentado, com efeito conhecido.
- **PROVÁVEL:** pode ajudar, mas o ganho não foi medido em toda máquina.
- **EXPERIMENTAL:** resultado varia ou é incerto; vem desmarcado.
- **INFO:** só informa, sem correção automática.

Inclui, entre outros, MPO, HAGS, Game DVR, aceleração do mouse, estado mínimo da CPU e prioridade alta do CS2. A prioridade alta não teve ganho medido e é gravada pelo Windows, sem o app tocar no processo do jogo.

O botão **DESFAZER** reverte todos os ajustes aplicados. O ajuste de MSI é experimental e pode causar tela preta em placa ou driver incompatível; nesse caso, entre no Modo de Segurança e rode `iRedResolution.exe --desfazer`.

### CFG DO CS2

Edita o `cs2_video.txt` dos perfis marcados. Só a conta Steam em uso vem marcada, as resoluções vêm do monitor e o original é guardado antes de gravar. A trava de somente leitura é opcional, e **RESTAURAR ORIGINAL** devolve o arquivo.

### Saturação por jogo

Usa o Digital Vibrance da NVIDIA enquanto o jogo está em foco. Em outras placas, a opção fica desativada. Limitações: com o recurso ligado, a abertura do app volta os monitores ao padrão do driver, e seguir o foco pode causar piscada no alt-tab em alguns PCs.

### MEDIR FPS

Mostra FPS, 1% low, travadas e gargalo usando o PresentMon da Intel. Só libera com o CS2 aberto pelo botão **ABRIR CS2 OFFLINE**, que usa `-insecure` e desliga o VAC naquela sessão, e com o Gamers Club Anti-Cheat fechado.

### Conveniências

Iniciar com o Windows (opcional), bandeja do sistema, presets de jogos e tutorial de escala para NVIDIA, AMD e Intel.

## Apoie o projeto

O iRedResolution é gratuito e sem anúncios. Quem quiser ajudar pode doar via PIX / LivePix, pelo QR code do programa ou pelo botão que abre a página.

Link direto: `widget.livepix.gg/embed/ecc5b854-5173-431c-a590-955cecdd2966`

## Não é hack nem cheat

**Não quer burlar nada:** nem Gamers Club, nem VAC, nem CS2, nem qualquer anti-cheat.

- **NÃO** dá vantagem em jogo.
- **NÃO** injeta código nem lê ou escreve na memória do jogo.
- **NÃO** intercepta a rede ou o tráfego do jogo.
- **NÃO** instala driver ou serviço.
- **NÃO** coleta dados seus.

A compilação falha se o nosso código usar funções de acesso à memória ou ao processo de outro programa. O PresentMon é uma ferramenta externa e pode consultar processos; por isso, só roda em teste offline.

**Nenhum anti-cheat certifica este programa, e cada plataforma tem as próprias regras.** O uso é por sua conta e risco. Detalhes em `AUDITORIA-SEGURANCA.md`.

## Antivírus

O executável não tem assinatura digital paga, então o Windows pode mostrar o SmartScreen. Um antivírus também pode reclamar. Pode ser falso positivo, mas confira antes: baixe só da página oficial e compare o SHA-256 da aba **INTEGRIDADE**. A versão 1.2 passou por uma varredura local do Microsoft Defender sem ameaças, em 06/11/2026; isso não garante o resultado em outros antivírus.

## Requisitos

- Windows de 64 bits. Testado no Windows 11; esta versão ainda não foi testada no Windows 10.
- .NET Framework 4.x, que já vem no Windows 10 e 11.
- Saturação: placa NVIDIA.

## Detalhes técnicos

- **Linguagem:** C# / .NET Framework, WinForms.
- **Tamanho:** cerca de 1,5 MB, arquivo único, com o PresentMon embutido.
- **APIs principais:** `ChangeDisplaySettingsEx`, `EnumDisplaySettings`, `EnumDisplayDevices`, `SetWinEventHook` fora de contexto e NVAPI.

## Comunidade

[Site](https://iredhub.com) · [Twitch](https://twitch.tv/iRedbrine) · [YouTube](https://youtube.com/@Redbrine) · [Discord](https://discord.gg/DQ8TzaFGtd) · [Kick](https://kick.com/iRedbrine) · [TikTok](https://tiktok.com/@iRedbrine) · [Instagram](https://instagram.com/iRedbrine) · [X](https://x.com/Red_Brine) · [Steam](https://steamcommunity.com/id/iRedbrine)

## Licença

Copyright © 2026 iRedHUB / Redbrine. Todos os direitos reservados. O PresentMon é da Intel, sob licença MIT, incluída no programa. Fornecido no estado em que se encontra, sem garantias. O uso é por sua conta e risco.
