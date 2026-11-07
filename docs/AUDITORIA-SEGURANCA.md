# Revisão de segurança — iRedResolution 1.2

**Data:** 2026-11-06. **Build público:** SHA-256 `E96CDFA94A92E948FA35B06983986ED3F2AD967739BED9DFE32B4B4A886EDA17`.

Esta é uma revisão interna do autor, feita no código-fonte e no executável. **Não é uma auditoria independente nem uma certificação de anti-cheat.**

## Resumo

| Item | Situação |
|---|---|
| Injeção de código e leitura ou escrita de memória, no nosso código | Nenhuma |
| `OpenProcess` e hooks de teclado ou mouse, no nosso código | Nenhum |
| Simulação de teclado ou mouse | Nenhuma |
| Rede no app | Só a verificação da página de doação e os links que você abrir |
| Telemetria e coleta de dados | Nenhuma |
| Ferramenta externa embutida | PresentMon, da Intel, só em teste offline |
| Microsoft Defender | Varredura local sem ameaças, assinaturas 1.463.160.0 |

## Regra do projeto

O iRedResolution não é hack nem cheat e não quer burlar nada: nem Gamers Club, nem VAC, nem CS2, nem qualquer anti-cheat.

A compilação falha se o nosso código usar `OpenProcess`, `ReadProcessMemory`, `WriteProcessMemory`, `VirtualAllocEx`, `CreateRemoteThread`, `QueueUserAPC`, `DebugActiveProcess` ou `SetThreadContext`, ou se acessar módulos, afinidade ou classe de prioridade de um processo. A trava vale para o nosso código, não para programas externos.

## O que o programa usa

### Rede

- `widget.livepix.gg`: verificação feita ao abrir a tela de doação.
- Links da comunidade e da doação: abrem no navegador quando você clica.

O build público não inclui o radar do iRedGuard, usado só em um build privado do autor.

### Programas executados

| Programa | Quando |
|---|---|
| O jogo ou comando configurado | Ao clicar em JOGAR ou ABRIR CS2 OFFLINE |
| `powercfg` | Ao ler o plano de energia ou aplicar e desfazer o ajuste da CPU |
| PresentMon | No MEDIR FPS, em teste offline |
| `net.exe` | No medidor, para consultar o grupo de desempenho ou, com UAC, incluir seu usuário |
| `shutdown.exe` | Só em REINICIAR NA BIOS |
| Painel do fabricante | Só ao clicar no tutorial de escala |
| O próprio app, elevado | Só ao aplicar ou desfazer ajustes |

### O que grava

| Onde | Quando |
|---|---|
| `%AppData%\iRedResolution` | Preferências, logs, histórico de medição, backups do CFG e registro do desfazer |
| `%LocalAppData%\iRedResolution\tools` | PresentMon, conferido por SHA-256 |
| Pasta temporária | Arquivo de medição do PresentMon |
| Registro HKCU `Run` | Só com *Iniciar com o Windows* |
| Registro HKCU e HKLM, e plano de energia | Só nos ajustes aplicados por você |
| `cs2_video.txt` | Só ao aplicar pelo CFG, com backup do original |

### Administrador

O app abre sem administrador (`asInvoker`). A elevação é pedida para aplicar ou desfazer ajustes, para incluir o usuário no grupo do medidor, para medir sem essa permissão e para reiniciar na BIOS.

## O que não dá para garantir

- **Anti-cheat:** nenhum certifica este programa, e cada plataforma tem as próprias regras. As mudanças são feitas fora do jogo, mas isso não garante como cada sistema vai reagir.
- **PresentMon:** contém referências a `OpenProcess` e `QueryFullProcessImageName`, e por isso só libera em teste offline, com `-insecure` e sem o Gamers Club Anti-Cheat aberto.
- **Prioridade alta do CS2:** usa `Image File Execution Options`, sem tocar no processo, mas não teve ganho medido nem teste específico com anti-cheats.
- **Saturação:** usa `SetWinEventHook` fora de contexto, sem injetar DLL, e a NVAPI. Pode causar piscada no alt-tab em alguns PCs.
- **MSI:** em placa ou driver incompatível, pode causar tela preta ao iniciar. A recuperação é pelo Modo de Segurança, com `iRedResolution.exe --desfazer`.
- **Conta padrão do Windows:** se o UAC usar outra conta, ajustes de usuário podem ir para o perfil dela.
- **Antivírus:** a varredura limpa no Defender não garante o resultado em outros produtos.
- **Código:** programas .NET podem ser descompilados, e o executável não é ofuscado.

## Limites desta revisão

O programa foi verificado no Windows 11, com placa NVIDIA, em três monitores. O restante está indicado como não testado nas notas da versão.

Copyright © 2026 iRedHUB / Redbrine. Todos os direitos reservados.
