---
title: Respostas a perguntas de TI & Segurança
---

Em grandes empresas, como a Fortune 500, há times de segurança que auditam as novas tecnologias que estão sendo utilizadas dentro da empresa.

Se os engenheiros de segurança estão interessados no seu projeto, alguns pontos de discussão podem ajudar a responder as questões deles:  

- Como Gatsby compila seu site para arquivos simples, em vez de ter servidores e bancos de dados rodando, ele reduz a superfície de ataque do site para intrusos.

- Gatsby adiciona uma camada de indireção que obscurece o seu CMS -- então, mesmo que o seu CMS _esteja_ vulnerável, os maus autores não terão ideia de onde encontrá-lo. Isto está em contraste com os sistemas onde os maus atores podem facilmente localizar o painel de administração, por exemplo, `/wp-admin` e tentar invadir o sistema.

- Gatsby permite você hospedar o seu site a partir de um CDN global, provavelmente, qualquer CDN que sua empresa estiver usando (ex: Akamai, Cloudflare, Fastly...), o que elimina efetivamente o risco de ataques DDOS.

É de grande utilidade enfatizar ao pessoal de segurança que esses benefícios foram um fator que contribuiu com a seleção do Gatsby para o projeto. Você escolheu o Gatsby, em parte, porque ele é _mais_ seguro.

Leia sobre segurança no Gatsby: [https://www.gatsbyjs.org/blog/2019-04-06-security-for-modern-web-frameworks/](/blog/2019-04-06-security-for-modern-web-frameworks/)

--

**Nota:** você tem ideias adicionais sobre como responder a questõeos de TI e segurança para projetos Gatsby? Estamos abertos a contribuições para os documentos do Gatsby. Saiba [como contribuir](/contributing/docs-contributions/).
