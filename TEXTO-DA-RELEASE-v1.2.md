## iRedResolution 1.2

Resolução por jogo, MODO GC, saturação, OTIMIZAR O PC, CFG DO CS2 e MEDIR FPS num app só. Troca a resolução da área de trabalho antes do jogo abrir e restaura ao fechar, para reduzir o alt-tab lento do CS2 mantendo a tela cheia exclusiva.

### Correções importantes
- **Alt-tab:** a resolução agora fica na área de trabalho durante o jogo. A v1.1 podia voltar à resolução anterior e trazer a piscada de volta.
- **Monitor:** o app reconhece o monitor escolhido mesmo se o Windows renumerar as telas.
- **Janelas:** crescem até caber o conteúdo; a rolagem só aparece se a tela for pequena demais.
- **Saturação:** não mexe mais no monitor durante o alt-tab. Fica aplicada até o jogo fechar. Além da NVIDIA, tenta o controle de Intel e AMD e, sem ele, usa o efeito de cor do Windows.
- **Desfazer:** cada valor volta com o tipo original no registro.
- **Fechar com o jogo aberto:** a resolução não muda por baixo do jogo.
- **Diagnóstico:** cache de shader em outros discos e plano de energia em qualquer idioma.

### Novidades
- **MEDIR FPS:** FPS, 1% low e gargalo, só em teste offline, com `-insecure` e sem o Gamers Club Anti-Cheat.
- **Prioridade alta do CS2:** ajuste opcional do Windows, sem ganho medido. Se o áudio falhar ou surgirem travadas, use o Desfazer.
- **Reiniciar na BIOS:** atalho no OTIMIZAR O PC.
- **Perfis por jogo:** cada jogo lembra a própria resolução.
- **Visual novo:** identidade do iRedHUB, opções recolhidas e Diagnóstico em abas.

### Mudanças de comportamento
- **CFG DO CS2:** marca só a conta Steam em uso, oferece os modos do seu monitor e não trava o arquivo por padrão.
- **MSI da placa e HAGS:** agora são experimentais e vêm desmarcados. O MPO continua sugerido, com texto mais claro sobre quando vale.
- **Saturação:** não apaga mais o ajuste que você já tinha no driver; só desfaz o que uma queda do app deixou aplicado.

### Não é hack nem cheat
Não injeta código, não lê nem escreve na memória do jogo e não quer burlar nada. Nenhum anti-cheat certifica este programa, e cada plataforma tem as próprias regras. Detalhes em `docs/AUDITORIA-SEGURANCA.md`.

### Segurança do download
O hash abaixo é o mesmo que o app mostra na aba INTEGRIDADE:

SHA-256: b2eb69814384f8e0c1e71376908b461c7d38decc7f3ae09839be50c35729f03d

Análise no VirusTotal (07/11/2026): 1 alerta em 70 mecanismos. Só o Elastic alerta, por heurística; os demais não detectaram nada: https://www.virustotal.com/gui/file/b2eb69814384f8e0c1e71376908b461c7d38decc7f3ae09839be50c35729f03d

O Windows pode mostrar "O Windows protegeu o computador", porque o arquivo não tem assinatura paga. Baixe só desta página e confira o hash antes de clicar em "Mais informações" e "Executar assim mesmo".

### Requisitos e testes
Windows de 64 bits e .NET Framework 4.x, que já vem no Windows 10 e 11. Saturação: NVIDIA pelo driver; Intel e AMD quando o driver aceita; nas demais, pelo efeito de cor do Windows, que pode não aparecer em jogo em tela cheia exclusiva.

Testado no Windows 11, com placa NVIDIA e três monitores. Saturação pelo efeito do Windows testada em uma Intel Iris Xe, só na área de trabalho. Ainda não testado: Windows 10, placa AMD e jogo em tela cheia nas placas que não são NVIDIA. Se encontrar problema, conte no Discord.
