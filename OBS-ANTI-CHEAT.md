# OBS Game Capture e anti-cheat

O GG Stream usa somente os hooks e inject helpers oficiais do OBS fixado no
projeto, preservando seus binários, hashes, assinaturas e a documentação GPL.
Esses binários não são modificados para parecerem oficiais.

Para jogos com anti-cheat, a compatibilidade é avaliada pela documentação atual
do OBS, do jogo e do fornecedor do anti-cheat. O GG Stream nunca faz stealth
injection, manual mapping, reflective injection, ocultação de processo/DLL,
spoofing, bypass, desativação ou alteração do anti-cheat.

Se Game Capture não for legitimamente compatível, o aplicativo não força o hook.
Ele tenta somente WGC da janela segura quando disponível; nunca captura o monitor
inteiro silenciosamente. Se nenhuma rota segura existir, mostra um erro claro.

O GG Stream não altera launch options. Caso um jogo documente uma opção como
`-allow_third_party_software`, o usuário decide e aplica manualmente.
