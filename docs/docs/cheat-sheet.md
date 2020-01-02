---
title: Tabela de Referência (Cheat Sheet)
---

A equipe do Gatsby criou um recurso que você pode achar útil ao criar um site do Gatsby: uma lista com todos os principais comandos e dicas de desenvolvimento! Sinta-se à vontade para baixar e imprimir uma cópia (e cole-a na sua estação de trabalho!). Para informações online relacionadas, visite [Início Rápido](/docs/quick-start/) e [Comandos (Gatsby CLI)](/docs/gatsby-cli/).

Baixe o PDF: <a href="/gatsby-cheat-sheet.pdf" baixar>gatsby-cheat-sheet.pdf</a>

<figure aria-labelledby="cheat_sheet-text">
    <h2>Page 1</h2>
    <a href="/cheat-sheet_page_1.png" title="Clique para abrir a imagem em uma nova janela" target="_blank" style="display:block;">
        <img src="/cheat-sheet_page_1.png" alt="Cheat Sheet - page 1" style="display:block; margin:0;" />
    </a>
    <h2>Page 2</h2>
    <a href="/cheat-sheet_page_2.png" title="Clique para abrir a imagem em uma nova janela" target="_blank" style="display:block;">
        <img src="/cheat-sheet_page_2.png" alt="Cheat Sheet - page 2" style="display:block; margin:0;" />
    </a>
</figure>

<div id="cheat_sheet-text" style=" position: absolute; height: 1px; width: 1px;overflow: hidden; clip: rect(1px, 1px, 1px, 1px);">
    <h2>Folha de dicas do Gatsby</h2>
    <p>v1.0 para Gatsby 2.x
        <a href="https://gatsby.dev/cheatsheet">Última versão <span aria-hidden="true">↗</span></a>
    </p>
    <h2>Principais Documentos</h2>
    <table>
        <tbody>
            <tr>
                <td>
                    <p>Documentos Gatsby</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/docs">gatsby.dev/docs</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Gatsby no GitHub</p>
                </td>
                <td>
                    <p><a href="https://github.com/gatsbyjs/gatsby">github.com/gatsbyjs/gatsby</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Tutorial Gatsby</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/tutorial">gatsby.dev/tutorial</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Ínicio Rápido<br />(para desenvolvedores intermediários e avançados)</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/quick-start">gatsby.dev/quick-start</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Starters Gatsby</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/starters">gatsby.dev/starters</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Guia de Referência Rápido</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/recipes">gatsby.dev/recipes</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Adicionando Imagens</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/image">gatsby.dev/image</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>APIs Node Gatsby</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/api">gatsby.dev/api</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Consultas com GraphQL</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/graphql">gatsby.dev/graphql</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Deploy e Hospedagem</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/deploy">gatsby.dev/publicação</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Using Gatsby Link</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/link">gatsby.dev/link</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Consulta Estática</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/static-query">gatsby.dev/static-query</a></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p>Como Contribuir</p>
                </td>
                <td>
                    <p><a href="https://gatsby.dev/contribute">gatsby.dev/contribute</a></p>
                </td>
            </tr>
        </tbody>
    </table>
    <p><a href="https://www.gatsbyjs.org/">gatsbyjs.org</a></p>
    <p><a href="https://twitter.com/gatsbyjs">twitter.com/gatsbyjs</a></p>
    <h2>Comandos Gatsby CLI</h2>
    <p>Primeiro, instale o executável global:
        <br />
        <code>npm install -g gatsby-cli</code></p>
    <p>Run <code>gatsby --help</code> para uma lista de comandos e opções.</p>
    <h3><code>gatsby novo <span style="font-weight:normal">nome-do-meu-site</span></code></h3>
    <p>Crie um novo site local do Gatsby usando o iniciador padrão (consulte “Comandos de iniciação rápida” nesta folha de dicas sobre como usar outros starters).</p>
    <h3><code>gatsby develop</code></h3>
    <p>Inicie o servidor de desenvolvimento Gatsby.</p>
    <table>
        <tbody>
            <tr>
                <td>
                    <p><code>-H, --host</code></p>
                </td>
                <td>
                    <p>Set host. Defaults to <code>localhost</code></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>-p, --port</code></p>
                </td>
                <td>
                    <p>Set port. Defaults to <code>8000</code></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>-o, --open</code></p>
                </td>
                <td>
                    <p>Abra o site no seu navegador (padrão)</p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>-S, --https</code></p>
                </td>
                <td>
                    <p>Use HTTPS</p>
                </td>
            </tr>
        </tbody>
    </table>
    <h3><code>gatsby build</code></h3>
    <p>Compile seu aplicativo e prepare-o para publicação.<br /></p>
    <table>
        <tbody>
            <tr>
                <td>
                    <p><code>--prefix-paths</code></p>
                </td>
                <td>
                    <p>Construir um site com caminhos de link predefinidos<br />(set <code>pathPrefix</code> in your config)</p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>--no-uglify</code></p>
                </td>
                <td>
                    <p>Construir sites sem pacotes 'uglifying JS'<br />(para depuração)</p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>--open-tracing-config-file</code></p>
                </td>
                <td>
                    <p>Arquivo de configuração do Tracer (compatível com OpenTracing). Veja <a href="https://gatsby.dev/tracing">gatsby.dev/tracing</a></p>
                </td>
            </tr>
        </tbody>
    </table>
    <h3><code>gatsby serve</code></h3>
    <p>Fornece a configuração de produção para teste.</p>
    <table>
        <tbody>
            <tr>
                <td>
                    <p><code>-H, --host</code></p>
                </td>
                <td>
                    <p>Definir host. O padrão é <code>localhost</code></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>-p, --port</code></p>
                </td>
                <td>
                    <p>Definir porta. O padrão é <code>9000</code></p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>-o, --open</code></p>
                </td>
                <td>
                    <p>Abra o site no seu navegador (padrão)</p>
                </td>
            </tr>
            <tr>
                <td>
                    <p><code>--prefix-paths</code></p>
                </td>
                <td>
                    <p>Fornece sites com caminho de links predefinidos (se contruir com <code>pathPrefix</code> em seu <code>gatsby-config.js</code>)</p>
                </td>
            </tr>
        </tbody>
    </table>
    <h3><code>informações do gatsby</code></h3>
    <p>Obtenha informações úteis sobre o ambiente, será necessário quando for relatar um bug em <a href="https://github.com/gatsbyjs/gatsby/issues">github.com/gatsbyjs/gatsby/issues</a>.</p>
    <table>
        <tbody>
            <tr>
                <td>
                    <p><code>-C, --clipboard</code></p>
                </td>
                <td>
                    <p>Copia automaticamente as informações do ambiente para a área de transferência</p>
                </td>
            </tr>
        </tbody>
    </table>
    <h3>gatsby limpo</h3>
    <p>Destrua o <code>.cache</code> do Gatsby e diretórios públicos <code>(public)</code>.</p>
    <h2>Camisetas, chapéus, moletom, e mais!</h2>
    <p>Inscreva-se na newsletter do Gatsby e <strong>ganhe 30% de desconto</strong> em sua compra na loja Gatsby!(<a href="https://gatsby.dev/store">gatsby.dev/store</a>)</p>
    <p>Inscreva-se<a href="https://gatsby.dev/discount">gatsby.dev/discount</a></p>
    <h2>Comandos de início rápido</h2>
    <p>Crie um novo site usando o starter "Blog":<br />
    <code>gatsby new my-blog-starter https://github.com/gatsbyjs/gatsby-starter-blog</code></p>
    <p>Navegue até o diretório do seu novo site e inicie-o:<br />
    <code>cd my-blog-starter/<br />
    desenvolvimento gatsby</code></p>
    <p>Seu site agora está sendo executado em <code>http://localhost:8000</code>!</p>
    <p>Você também verá um segundo link: <code>http://localhost:8000/___graphql</code>. Esta é uma ferramenta que você pode usar para experimentar a consulta de seus dados. Saiba mais sobre isso em <a href="https://gatsby.dev/tutorial">gatsby.dev/tutorial</a></p>
    <p>Para mais starters Gatsby, visite <a href="https://gatsby.dev/starters">gatsby.dev/starters</a>.</p>
    <h2>Definições úteis de arquivo</h2>
    <p>Cada um desses arquivos deve estar na raiz da pasta do projeto Gatsby. Veja <a href="https://gatsby.dev/projects">gatsby.dev/projects</a></p>
    <p><code>gatsby-config.js</code> — configurar opções para um site feito com Gatsby, com metadados para o título do projeto, descrição, plugins, etc.</p>
    <p><code>gatsby-node.js</code> — implementar APIs Node.js do Gatsby para personalizar e estender as configurações padrão que afetam o processo de criação</p>
    <p><code>gatsby-browser.js</code> — personalizar e estender as configurações padrão que afetam o navegador, usando as APIs do navegador do Gatsby</p>
    <p><code>gatsby-ssr.js</code> — use as APIs de renderização do lado do servidor do Gatsby para personalizar as configurações padrão que afetam a renderização</p>
</div>
