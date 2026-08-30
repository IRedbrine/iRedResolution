# Auditoria de segurança — iRedResolution

Revisão feita sobre todo o código-fonte, na perspectiva de dois riscos:
**(A)** o app ser seguro e saudável para quem instala; **(B)** ninguém
conseguir reaproveitar o código como cheat ou malware com a sua marca.

Data: 2026-08-30 · Versão auditada: 1.0 · SHA-256 do build ao final.

---

## Resumo executivo

| | Situação |
|---|---|
| APIs de injeção em outros processos | **Nenhuma** |
| Leitura/escrita de memória alheia | **Nenhuma** |
| Captura de teclado (keylogger) | **Nenhuma** |
| Conexões de rede | 2, ambas para domínios fixos e conhecidos |
| Execução de processos | Só o jogo (input do usuário) e `powercfg` (fixo) |
| Escrita em disco | Só `%AppData%\iRedResolution` e o `cs2_video.txt` do Steam |
| Elevação (admin) | Sob demanda, só para os ajustes de registro HKLM |
| Varredura do Microsoft Defender | **Limpo** |

Conclusão: o app é benigno por construção. Não faz nada que um anticheat
puna, e não expõe o usuário. Os riscos residuais são baixos e documentados
abaixo.

---

## (A) O app é seguro para quem instala?

### A1. Superfície de rede — OK

Só existem duas saídas de rede, ambas com destino **fixo no código** (não
montado a partir de entrada do usuário, então não há como redirecionar):

- `widget.livepix.gg` — apenas um HEAD para checar se a doação está no ar.
- Os links de comunidade (iredhub.com, twitch, discord…) — abertos no
  navegador quando **você** clica.

Nenhum dado do usuário é enviado. Nenhuma telemetria. Nenhum download e
execução de código remoto.

### A2. Execução de processos — OK, com um ponto

- `powercfg` — nome fixo, e o valor de restauração agora é validado como
  numérico antes de repassar (fecha injeção via arquivo de log editado).
- O **jogo** — vem do campo editável. É o próprio usuário mandando abrir
  algo na própria máquina, via `UseShellExecute` (o mesmo que digitar no
  menu Iniciar). Não é escalonamento nem execução remota. Aceitável.
- A reabertura elevada (`--aplicar`) só aceita **ids conhecidos**, filtrados
  contra a lista interna de ajustes. Passar lixo no argumento não executa nada.

### A3. Escrita em disco — OK

Tudo confinado a `%AppData%\iRedResolution` (config, logs, backups) e ao
`cs2_video.txt` dos perfis Steam — este com backup automático antes de
qualquer escrita, e restauração completa disponível.

### A4. Elevação — OK

O app roda **sem admin** (manifesto `asInvoker`). Só pede elevação quando
você aplica ajustes que exigem HKLM, e nesse caso reabre uma instância
dedicada que faz só aquilo e sai. Não mantém privilégio.

### A5. Reversibilidade — OK

Todo ajuste de sistema é registrado e reversível: registro (por chave),
plano de energia (via powercfg) e cs2_video.txt (por backup). Nada é
alterado de forma definitiva.

---

## (B) Alguém consegue transformar isto em cheat?

### O que torna um programa um "cheat" de CS2

Ler/escrever a memória do jogo, injetar DLL, ganchar o processo do jogo,
interceptar DirectX, automatizar tiros/mira. **O iRedResolution não tem
nenhuma dessas capacidades** — e adicioná-las exigiria reescrever o app,
não "destravar" algo.

Confirmado por varredura: `ReadProcessMemory`, `WriteProcessMemory`,
`OpenProcess`, `CreateRemoteThread`, `VirtualAllocEx`, `SetWindowsHookEx`,
`GetAsyncKeyState`, `SendInput` — **todos ausentes**.

### O único gancho existente, e por que é seguro

Para a saturação seguir o foco, o app usa `SetWinEventHook` com a flag
`WINEVENT_OUTOFCONTEXT`. Essa variante **não injeta DLL** em processo
nenhum: o Windows apenas avisa o nosso processo quando a janela em primeiro
plano muda. É a forma benigna, usada por leitores de tela, gravadores e
utilitários de janela. Um anticheat não tem como confundir isso com injeção,
porque nada é escrito no espaço do jogo.

### Compatibilidade com anticheat

Por não tocar no jogo, é compatível com **VAC, FACEIT, ESEA e Vanguard**.
O que ele faz — trocar resolução, editar um .txt de config, ajustar
saturação do monitor — são ações de sistema que o próprio Windows e o painel
da NVIDIA fazem.

### Se alguém pegar o código-fonte

O projeto é distribuível como fonte. Um mau-ator poderia, teoricamente,
partir dele e **escrever** um cheat — mas teria que escrever tudo do zero
(o código de injeção não existe aqui), então o iRedResolution não dá
atalho nenhum. Reaproveitar a marca é coberto na seção de autoria.

---

## Proteção de autoria — o que é honesto esperar

**Verdade técnica:** .NET compila para IL, que qualquer pessoa descompila
com dnSpy ou ILSpy em minutos. Nenhum truque em C# torna o código
"inquebrável". Só um **ofuscador** dificulta de verdade.

O que está embutido (camada de dissuasão, não blindagem):

- Direitos autorais nos metadados do binário, no manifesto e no código.
- Verificação de integridade: o app detecta se os metadados de autoria
  foram trocados e registra em log.
- Carimbo de marca montado em runtime (não aparece como string única no
  binário).
- SHA-256 da build exibido no próprio app, para provar origem.

**Para proteção real antes de distribuir:** rodar o
[ConfuserEx](https://github.com/mkaring/ConfuserEx) (gratuito) sobre o
`iRedResolution.exe`. Ver `docs/GUIA-OFUSCACAO.md`.

---

## Recomendações finais

1. **Antes de publicar:** rodar o ConfuserEx (guia à parte).
2. **Assinatura digital:** um certificado de code signing eliminaria o
   alerta do SmartScreen. É pago e anual — vale se o alcance crescer.
3. **Publicar o SHA-256** de cada release, para os usuários conferirem.
4. **Nunca** aceitar a sugestão de adicionar leitura de memória, macros de
   tiro ou qualquer automação de jogo — é o que separa este utilitário de
   um cheat, e o que mantém todo mundo longe de ban.

---

Copyright © 2026 iRedHUB / Redbrine. Todos os direitos reservados.
