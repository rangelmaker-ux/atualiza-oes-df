# Promob Start Atualizações — instalação manual autorizada

O instalador aplica bibliotecas completas de cores/MDF, módulos, tampo/molduras e puxadores, preservando TODOS os arquivos existentes de System/budget. Não substitui executáveis ou DLLs do Start.

1. Salve o projeto e feche o Start.
2. Execute o instalador completo, autorize a elevação do Windows e selecione a pasta do Start.
3. Informe o código acordado para autorizar a aplicação. Arquivos idênticos são mantidos; arquivos diferentes recebem backup antes da substituição.
4. O atalho Promob Start Atualizações será criado na área de trabalho compartilhada.
5. Abra o atalho e confira o endereço preconfigurado https://github.com/rangelmaker-ux/atualiza-oes-df. Essa configuração também exige o código. O endereço já vem configurado; a tarefa consulta esse repositório sem instalar automaticamente.
6. Buscar / baixar permite consultar manualmente. A tarefa do Windows consulta a cada quatro horas; apenas baixa pacotes assinados e registra o resultado.
7. Durante a visita técnica, informe o código e clique em Instalar pacote baixado. A aplicação é local e exige Start fechado, versão compatível, espaço e integridade corretos.

O código não é salvo em texto: o executável contém uma verificação PBKDF2. Não é proteção contra administradores do Windows modificando o software diretamente. Não há bloqueio de firewall incluído: este programa não abre portas nem modifica a conectividade do Start; bloquear todo o Start requer configuração e teste próprios dos executáveis envolvidos.

## Publicação

Os pacotes serão publicados em GitHub Releases no repositório separado https://github.com/rangelmaker-ux/atualiza-oes-df. Cada release contém package.zip, release.json e release.sig. O atualizador consulta releases/latest/download/release.json. A versão deve usar sequência crescente. O pacote precisa ser produzido por PublishPackage.py e assinado localmente com Sign.exe.

A chave privada signing.dpapi NÃO deve ser publicada. Ela está protegida por DPAPI para o usuário Windows desta máquina. A chave pública já está incorporada no atualizador. O instalador Windows não possui certificado Authenticode: o Windows pode exibir o aviso de editor desconhecido. A assinatura dos pacotes de atualização é própria e não substitui um certificado Authenticode.

Após cada correção: valide localmente, liste os arquivos necessários, gere pacote incremental, publique os três arquivos na release e aguarde a visita para instalar. Não inclua mudanças de orçamento/XML: o atualizador as rejeita mesmo quando assinadas. Mudanças de bibliotecas podem alterar as peças/consumos de projetos futuros; preservar o exportador não garante valores idênticos se o projeto ou as definições de componentes mudarem.

## Falhas e recuperação

O instalador verifica o runtime validado do Start, os registros nativos e os vínculos de posicionamento. Em falha durante aplicação, tenta reverter os arquivos escritos. Backups ficam em AtualizacoesBackup dentro do Start; logs de consulta em ProgramData/PSA3/<identificador>/atualizador.log. O instalador oferece Restaurar backup com autorização; backups antigos que alteram orçamento/XML devem ser rejeitados nesta versão para preservar o estado atual.

Não executar o instalador anterior Completo 2026-10-05: ele ainda inclui alterações de orçamento/XML. Usar a versão Manual.

## Verificação desta versão

Instalação completa em pasta de teste nova e reinstalação: 27.110 arquivos de bibliotecas; 15.496 registros nativos e 198 vínculos de puxadores. Os 284 arquivos de orçamento/XML já existentes ficaram byte a byte iguais. Testes de assinatura, código errado, versão repetida e reversão passaram. O registro do atalho e do agendamento foram testados com elevação. A tarefa executou como SYSTEM, consultou o GitHub e terminou com resultado 0, sem instalar. Também passou o teste real de download, assinatura e aplicação autorizada de um pacote incremental pelo GitHub.
