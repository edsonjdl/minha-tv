# CODEX.md — Objetivo de implementação integral

## Missão
Entregar uma versão **instalável e testável** do aplicativo webOS deste repositório, preservando o launcher original e acrescentando uma entrada **Arquivos Locais** para uma biblioteca visual de filmes e séries em NAS/DLNA (Smart Share). O usuário quer que o agente execute o desenvolvimento de ponta a ponta, sem parar após protótipos intermediários ou exigir uma sequência de aprovações de etapas. Não declarar conclusão sem evidências de build e instalação documentada.

## Ambiente-alvo
- TVs-alvo: LG OLED55B7P (B7, 2017), webOS 3.5, firmware 06.10.65; e LG OLED77C4PUA (C4, 2024), webOS 24. O mesmo aplicativo deve atender às duas TVs.
- NAS doméstico; conteúdos acessíveis por Smart Share/DLNA, a validar na TV real.
- Desenvolvimento/empacotamento em computador, instalação pela rede com Developer Mode e ferramentas webOS compatíveis.
- Priorizar compatibilidade com webOS 3.5 sem prejudicar webOS 24; isolar diferenças de API, player e permissões por detecção de capacidades, não por suposição. Preferir um único pacote .ipk quando tecnicamente viável; se inviável, documentar a razão e gerar builds específicos.
- O app original é um launcher com atalhos de serviços e integração TMDB. Não substituir webOS.

## Experiência exigida
1. Manter launcher, atalhos e demais recursos existentes intactos.
2. Adicionar entrada **Arquivos Locais** ao lado dos serviços existentes, abrindo uma seção dedicada.
3. Na seção local, permitir cadastrar/remover fontes ou pastas de biblioteca, identificando cada uma como **Filmes** ou **Séries**; persistir configurações de maneira apropriada e segura.
4. Exibir catálogo navegável por controle remoto, com capas, sinopses e organização estilo serviço de streaming, enriquecido via TMDB quando disponível; fallback offline e correção manual de correspondências.
5. Abrir detalhes e reproduzir o arquivo selecionado no player suportado pela B7, com controles e tratamento de erros.
6. Suportar navegação eficiente sem percorrer manualmente toda a árvore de pastas em cada abertura.
7. Evitar expor IPs, credenciais, tokens e caminhos privados em commits. Chaves TMDB e configurações sensíveis devem ser parametrizadas.
8. Considerar a limitação observada de 8 faixas de legendas MKV na TV como investigação secundária: não prometer superar restrição do player. Se viável, oferecer seleção por servidor/remux sem recodificação, como evolução, sem bloquear entrega inicial.

## Orientações técnicas
- **Inspecionar primeiro o código e a licença**; aproveitar arquitetura, build e ferramentas existentes. Não supor que o projeto original já acessa DLNA ou arquivos locais.
- Determinar se o webOS 3.5 permite descoberta e navegação DLNA diretamente por APIs disponíveis ao app. Se não, implementar pequeno serviço complementar no Windows/rede local para indexação e URLs de mídia, com documentação de instalação e inicialização. Não presumir que APIs modernas funcionam no webOS 3.5.
- Considerar CORS, HTTP/HTTPS, descoberta UPnP/SSDP, formatos de mídia e restrições do player; testar emulador/ambiente compatível quando possível. A reprodução direta deve evitar transcodificação desnecessária.
- UI responsiva a controle remoto: foco visível, setas, OK, Voltar; performance em hardware de 2017. Verificar navegação, reprodução, permissões e layout também na C4/webOS 24.
- Preferir testes automatizados e verificações de build; adicionar testes relevantes.
- Produzir pacote **.ipk** se as ferramentas de build permitirem; caso contrário documentar precisamente bloqueio e comandos reproduzíveis, sem fingir que pacote existe.
- Documentar instruções de instalação via Developer Mode para B7 e C4, dependências do computador/servidor, configuração de NAS/TMDB, limitações conhecidas e testes feitos/não feitos em cada modelo.
- Trabalhar apenas na branch `smartshare-test`, não alterar `main`; commits claros. Não publicar segredos nem modificar repositório de origem.
- O usuário quer **uma execução contínua até uma versão instalável**, não entregas parceladas. Faça decisões técnicas razoáveis sem interromper para dúvidas não essenciais; peça intervenção somente quando indispensável (por exemplo, acesso à TV/NAS ou credenciais). Não alegar teste na TV sem execução real.

## Critérios de conclusão
- App original continua funcionando.
- Acesso à seção Arquivos Locais, cadastro de fontes/pastas, catálogo Filmes/Séries, navegação por controle remoto e fluxo de reprodução implementados.
- Build reproduzível e pacote instalável gerado para ambas as TVs (preferencialmente o mesmo .ipk), ou bloqueio externo claramente explicado.
- README atualizado com instalação/configuração e evidências de testes.
- Resumo final dos commits, arquivos alterados, funcionalidades verificadas, limitações e passos exatos para testar na LG B7.

Este arquivo é um briefing para execução do Codex; **não inicia uma tarefa sozinho**.

## Identidade visual aprovada — Edplex (06/11/2026)
- **Decisão do usuário:** renomear a entrada e a seção **Arquivos Locais** para **Edplex** (grafia da marca no cartão: **EDPLEX**). Preservar a funcionalidade de biblioteca local.
- **Logo aprovado:** cartão retangular horizontal com cantos arredondados; fundo **azul-marinho escuro uniforme, sem degradê**; símbolo superior de película cinematográfica azul-ciano com triângulo vermelho de reprodução; lettering grande **ED** branco + **PLEX** vermelho; traço vermelho curvo abaixo do nome. Não substituir por ícone genérico de pasta.
- **Arquivo de referência:** a arte foi aprovada nesta conversa do ChatGPT, mas **o PNG ainda não foi enviado ao repositório**. Ao receber o PNG, armazená-lo no projeto, preferencialmente em `assets/edplex-logo.png` (ou diretório de recursos existente) e utilizá-lo no cartão do launcher. Não afirmar que o arquivo já existe no GitHub; pedir a imagem caso ela não esteja disponível no ambiente do Codex. Não recriar uma imagem diferente sem necessidade.
- Ajustar tamanho/proporção, foco pelo controle remoto e legibilidade para ficar coerente com os cartões de Netflix/Disney+/Prime Video. Manter a compatibilidade B7 e C4. Preservar o original e trabalhar somente em `smartshare-test`.
