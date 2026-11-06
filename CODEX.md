# CODEX.md — Objetivo de implementação integral

## Missão
Entregar uma versão **instalável e testável** do aplicativo webOS deste repositório, preservando o launcher original e acrescentando uma entrada **Arquivos Locais** para uma biblioteca visual de filmes e séries em NAS/DLNA (Smart Share). O usuário quer que o agente execute o desenvolvimento de ponta a ponta, sem parar após protótipos intermediários ou exigir uma sequência de aprovações de etapas. Não declarar conclusão sem evidências de build e instalação documentada.

## Ambiente-alvo
- TV: LG OLED55B7P (B7, 2017), webOS 3.5, firmware 06.10.65.
- NAS doméstico; conteúdos acessíveis por Smart Share/DLNA, a validar na TV real.
- Desenvolvimento/empacotamento em computador, instalação pela rede com Developer Mode e ferramentas webOS compatíveis.
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
- UI responsiva a controle remoto: foco visível, setas, OK, Voltar; performance em hardware de 2017.
- Preferir testes automatizados e verificações de build; adicionar testes relevantes.
- Produzir pacote **.ipk** se as ferramentas de build permitirem; caso contrário documentar precisamente bloqueio e comandos reproduzíveis, sem fingir que pacote existe.
- Documentar instruções de instalação via Developer Mode, dependências do computador/servidor, configuração de NAS/TMDB, limitações conhecidas e testes feitos/não feitos.
- Trabalhar apenas na branch `smartshare-test`, não alterar `main`; commits claros. Não publicar segredos nem modificar repositório de origem.
- O usuário quer **uma execução contínua até uma versão instalável**, não entregas parceladas. Faça decisões técnicas razoáveis sem interromper para dúvidas não essenciais; peça intervenção somente quando indispensável (por exemplo, acesso à TV/NAS ou credenciais). Não alegar teste na TV sem execução real.

## Critérios de conclusão
- App original continua funcionando.
- Acesso à seção Arquivos Locais, cadastro de fontes/pastas, catálogo Filmes/Séries, navegação por controle remoto e fluxo de reprodução implementados.
- Build reproduzível e pacote instalável gerado, ou bloqueio externo claramente explicado.
- README atualizado com instalação/configuração e evidências de testes.
- Resumo final dos commits, arquivos alterados, funcionalidades verificadas, limitações e passos exatos para testar na LG B7.

Este arquivo é um briefing para execução do Codex; **não inicia uma tarefa sozinho**.
