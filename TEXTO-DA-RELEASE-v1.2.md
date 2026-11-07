## iRedResolution 1.2

Troca a resolução da área de trabalho antes do jogo abrir e restaura ao fechar, para reduzir o alt-tab lento do CS2 mantendo a tela cheia exclusiva.

### Correções importantes
- **Alt-tab:** a resolução agora fica na área de trabalho durante o jogo. A v1.1 podia voltar à resolução anterior e trazer a piscada de volta.
- **Monitor:** o app reconhece o monitor escolhido mesmo se o Windows renumerar as telas.
- **Janelas:** crescem até caber o conteúdo; a rolagem só aparece se a tela for pequena demais.
- **Saturação:** não mexe mais no monitor durante o alt-tab. Fica aplicada até o jogo fechar.
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
- **MSI da placa:** agora é experimental e vem desmarcado.

### Não é hack nem cheat
Não injeta código, não lê nem escreve na memória do jogo e não quer burlar nada. Nenhum anti-cheat certifica este programa, e cada plataforma tem as próprias regras. Detalhes em `docs/AUDITORIA-SEGURANCA.md`.

### Segurança do download
O hash abaixo é o mesmo que o app mostra na aba INTEGRIDADE:

SHA-256: PREENCHER_COM_O_HASH_DO_EXE_FINAL

O Windows pode mostrar "O Windows protegeu o computador", porque o arquivo não tem assinatura paga. Baixe só desta página e confira o hash antes de clicar em "Mais informações" e "Executar assim mesmo".

### Requisitos e testes
Windows de 64 bits e .NET Framework 4.x, que já vem no Windows 10 e 11. Saturação requer NVIDIA.

Testado no Windows 11, com placa NVIDIA e três monitores. Ainda não testado: Windows 10, placas AMD e Intel, e notebook com duas placas. Se encontrar problema, conte no Discord.
