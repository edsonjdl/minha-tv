# Revisão de código — Minha TV

Data: 13/11/2026. Revisão estática inicial; sem testes executados ou alterações na TV.

## Identificação e escopo

O repositório `edsonjdl/minha-tv` contém uma versão do projeto **Free My TV**, com cliente webOS/Tizen e Android. Ainda **não está confirmado** que seja o mesmo projeto pessoal Edplex/player LG discutido com o proprietário. Não presumir equivalência nem implantação.

## Comentários por arquivo

- **P1 — `web/index.html`:** scripts `config.js`, `coins.js`, `i18n.js`, `strings.js`, `tv.js`, `zones.js`, `data.js`, `home.js` carregam em sequência. Testar a aplicação empacotada em LG webOS 3 (Chrome 38) e modelos mais novos, incluindo rede/TMDB indisponíveis e erro de script; verificar se existe fallback visível e navegação por controle remoto.
- **P2 — `webos/build.py`, `tv_apps()`:** o empacotamento local pode incorporar lista e ícones de aplicativos da TV. Incluir teste automatizado garantindo que `--generic`/release exclui inventário local, ícones e segredos, e que pacote local não seja distribuído como release.
- **P2 — `CLAUDE.md` e `README.md`:** procedimentos documentam instalação via Developer Mode, validade limitada e reversão. Exigir identificação da TV e backup das configurações necessárias antes de qualquer instalação; nenhuma alteração em aparelhos sem autorização específica.

## Próxima etapa

Confirmar se `minha-tv` é o aplicativo solicitado ou se Edplex tem código em outro local; depois examinar módulos JS, APIs, persistência, testes, build, privacidade e compatibilidade de webOS. **Não declarar code review integral concluído.** Não foi possível publicar comentários inline em PR porque nenhum PR aberto foi encontrado; este arquivo contém as referências diretas aos trechos revisados.
