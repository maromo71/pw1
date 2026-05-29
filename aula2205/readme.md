# Documentação Didática de Arquitetura CSS

Este arquivo `README.md` serve como um guia de estudo para alunos de desenvolvimento web. Abaixo, o código CSS original foi mapeado. Cada vez que uma propriedade e um valor aparecem **pela primeira vez**, eles são acompanhados do comentário `/* propriedade: valor */` e de uma explicação detalhada sobre o impacto dessa linha na renderização da página.

---

## Código CSS Comentado e Analisado

```css
/* ==========================================================================
   RESET & CONFIGURAÇÕES GERAIS (Boas Práticas de Design)
   --------------------------------------------------------------------------
   O objetivo desta seção é "zerar" as configurações que os navegadores aplicam
   automaticamente e definir a identidade visual global (cores e fontes).
   ========================================================================== */

* {
    margin: 0; /* margin: 0 */ — Remove o espaçamento externo padrão de todos os elementos.
    padding: 0; /* padding: 0 */ — Remove o espaçamento interno padrão de todos os elementos.
    box-sizing: border-box; /* box-sizing: border-box */ — Altera o cálculo do tamanho do elemento: agora, bordas (border) e espaçamentos internos (padding) ficam inclusos na largura total, evitando que caixas quebrem o layout.
}

:root {
    /* Paleta Dark Mode - Azul Moderno & Profundo */
    /* Variáveis customizadas (Custom Properties): servem para armazenar valores que reutilizaremos no código todo. */
    --bg-dark-absolute: #050811; /* --bg-dark-absolute: #050811 */ — Armazena a cor preta azulada profunda.
    --bg-dark-surface: #0b132b;  /* --bg-dark-surface: #0b132b */ — Armazena o azul escuro usado em blocos/cards.
    --brand-electric: #48cae4;    /* --brand-electric: #48cae4 */ — Armazena o azul neon vibrante para destaques.
    --brand-deep-blue: #1c2541;  /* --brand-deep-blue: #1c2541 */ — Armazena o azul intermediário para estruturas.
    
    /* Tipografia e Texto */
    --text-primary: #f8f9fa;      /* --text-primary: #f8f9fa */ — Armazena o cinza quase branco de alta legibilidade.
    --text-muted: #94a3b8;        /* --text-muted: #94a3b8 */ — Armazena o cinza médio para textos secundários.
    
    /* Efeitos */
    --transition-smooth: all 0.3s cubic-bezier(0.4, 0, 0.2, 1); /* --transition-smooth: all 0.3s cubic-bezier(0.4, 0, 0.2, 1) */ — Armazena uma transição suave que afeta todas as propriedades em 0.3 segundos usando uma aceleração personalizada.
    --border-glow: 1px solid rgba(72, 202, 228, 0.15); /* --border-glow: 1px solid rgba(72, 202, 228, 0.15) */ — Armazena uma borda fina contínua com azul neon semi-transparente (15% de opacidade).
}

html {
    scroll-behavior: smooth; /* scroll-behavior: smooth */ — Faz com que o clique em links âncora role a página de forma suave e deslizante, em vez de um salto brusco.
    font-family: 'Space Grotesk', sans-serif; /* font-family: 'Space Grotesk', sans-serif */ — Define a família tipográfica principal da página com fallback para fontes sem serifa.
    background-color: var(--bg-dark-absolute); /* background-color: var(--bg-dark-absolute) */ — Aplica a cor de fundo guardada na variável global.
    color: var(--text-primary); /* color: var(--text-primary) */ — Define a cor padrão dos textos da aplicação usando a variável de texto claro.
}

body {
    overflow-x: hidden; /* overflow-x: hidden */ — Esconde qualquer conteúdo que tente passar da largura horizontal da tela, impedindo o surgimento da indesejada barra de rolagem lateral.
}

/* Customização básica da barra de rolagem do navegador */
::-webkit-scrollbar {
    width: 8px; /* width: 8px */ — Define a largura física da barra de rolagem vertical.
}
::-webkit-scrollbar-track {
    background: var(--bg-dark-absolute); /* background: var(--bg-dark-absolute) */ — Define a cor da "pista" por onde a barra corre.
}
::-webkit-scrollbar-thumb {
    background: var(--brand-deep-blue); /* background: var(--brand-deep-blue) */ — Define a cor do indicador (o retângulo arrastável).
    border-radius: 4px; /* border-radius: 4px */ — Arredonda os cantos do indicador em 4 pixels.
}
::-webkit-scrollbar-thumb:hover {
    background: var(--brand-electric); /* background: var(--brand-electric) */ — Altera a cor do indicador para azul elétrico quando o usuário passa o mouse por cima.
}

/* ==========================================================================
   HEADER & NAVBAR
   --------------------------------------------------------------------------
   Controla a barra de topo. O aluno aprenderá aqui como fixar elementos 
   e criar layouts horizontais alinhados.
   ========================================================================== */

.main-header {
    position: fixed; /* position: fixed */ — Fixa o elemento em relação à janela de visualização (viewport). Ele não sai do lugar mesmo que a página seja rolada.
    top: 0; /* top: 0 */ — Alinha o elemento grudado no topo absoluto da tela.
    left: 0; /* left: 0 */ — Alinha o elemento grudado na lateral esquerda absoluta.
    width: 100%; /* width: 100% */ — Força o cabeçalho a ocupar toda a largura disponível horizontalmente.
    z-index: 1000; /* z-index: 1000 */ — Camada de empilhamento do elemento no eixo Z. O valor alto garante que ele fique por cima de quase todos os elementos do site.
    background-color: rgba(5, 8, 17, 0.85); /* background-color: rgba(5, 8, 17, 0.85) */ — Aplica um fundo preto azulado com 85% de opacidade, permitindo ver de leve o que passa por trás.
    backdrop-filter: blur(12px); /* backdrop-filter: blur(12px) */ — Aplica um desfoque de 12px ao que está por trás do cabeçalho, simulando um efeito moderno de vidro fosco (Glassmorphism).
    border-bottom: var(--border-glow); /* border-bottom: var(--border-glow) */ — Aplica a borda neon sutil apenas na parte inferior do cabeçalho.
}

.header-container {
    max-width: 1200px; /* max-width: 1200px */ — Define que a largura do conteúdo interno nunca passará de 1200 pixels, independentemente do tamanho do monitor.
    margin: 0 auto; /* margin: 0 auto */ — Centraliza o bloco na horizontal (0 de espaçamento em cima/baixo e calcula automaticamente as laterais de forma idêntica).
    padding: 1.25rem 2rem; /* padding: 1.25rem 2rem */ — Define 1.25rem (20px) de espaçamento interno em cima e embaixo, e 2rem (32px) nas laterais esquerda e direita.
    display: flex; /* display: flex */ — Ativa o modelo flexível de caixas. Transforma os filhos diretos em flex-items alinháveis de forma dinâmica.
    justify-content: space-between; /* justify-content: space-between */ — Distribui os elementos filhos empurrando o primeiro para o extremo esquerdo e o último para o extremo direito, deixando o espaço vazio no meio.
    align-items: center; /* align-items: center */ — Alinha todos os elementos filhos verticalmente exatamente no centro da linha do cabeçalho.
}

.brand-logo {
    font-family: 'Syne', sans-serif; /* font-family: 'Syne', sans-serif */ — Aplica uma tipografia específica (Syne) apenas para a identidade visual da logo.
    font-weight: 800; /* font-weight: 800 */ — Aplica o peso extra-negrito (Extra Bold) para dar destaque e peso visual ao texto da logo.
    font-size: 1.5rem; /* font-size: 1.5rem */ — Define o tamanho da fonte como 1.5 vezes o tamanho base da página (geralmente resulta em 24px).
    letter-spacing: -1px; /* letter-spacing: -1px */ — Reduz o espaço padrão entre as letras em 1px, deixando o texto mais compacto e moderno.
    color: var(--text-primary);
}

.brand-logo span {
    color: var(--brand-electric);
}

.nav-menu {
    display: flex;
    gap: 2rem; /* gap: 2rem */ — Define um espaçamento fixo de 2rem (32px) entre cada link do menu, sem precisar mexer em margens individuais.
}

.nav-link {
    color: var(--text-muted);
    text-decoration: none; /* text-decoration: none */ — Remove o sublinhado padrão que todos os links (`<a>`) possuem no navegador.
    font-weight: 600; /* font-weight: 600 */ — Define a espessura da fonte como semi-negrito (Semi Bold).
    font-size: 0.95rem; /* font-size: 0.95rem */ — Ajusta sutilmente o tamanho do texto para 95% do tamanho base.
    transition: var(--transition-smooth); /* transition: var(--transition-smooth) */ — Habilita animações suaves baseadas na nossa variável quando propriedades como a cor mudarem.
}

.nav-link:hover {
    color: var(--brand-electric);
}

/* ==========================================================================
   ELEMENTOS DE INTERAÇÃO (BOTÕES)
   --------------------------------------------------------------------------
   Aqui o aluno verá estados interativos (`:hover`), uso de sombras neon 
   e transições mecânicas em botões.
   ========================================================================== */

.btn-primary-sm {
    background-color: transparent; /* background-color: transparent */ — Torna o fundo do botão invisível/vazio.
    color: var(--brand-electric);
    border: 1px solid var(--brand-electric); /* border: 1px solid var(--brand-electric) */ — Aplica uma borda de 1px contínua utilizando a cor azul elétrico.
    padding: 0.5rem 1.25rem; /* padding: 0.5rem 1.25rem */ — Define um preenchimento menor interno, ideal para botões pequenos.
    border-radius: 4px;
    text-decoration: none;
    font-weight: 600;
    font-size: 0.875rem; /* font-size: 0.875rem */ — Define o tamanho da fonte um pouco menor para o botão secundário ou compacto (14px).
    transition: var(--transition-smooth);
}

.btn-primary-sm:hover {
    background-color: var(--brand-electric);
    color: var(--bg-dark-absolute);
    box-shadow: 0 0 15px rgba(72, 202, 228, 0.4); /* box-shadow: 0 0 15px rgba(72, 202, 228, 0.4) */ — Adiciona uma sombra difusa ao redor do botão, simulando um efeito luminoso de neon azul elétrico com 40% de opacidade.
}

.btn-primary {
    display: inline-block; /* display: inline-block */ — Permite que o link se comporte como um bloco (aceitando paddings e margens verticais corretamente), mas se alinhe na mesma linha de outros textos.
    background-color: var(--brand-electric);
    color: var(--bg-dark-absolute);
    padding: 0.875rem 2rem; /* padding: 0.875rem 2rem */ — Define o espaçamento interno clássico para botões de destaque maiores.
    border-radius: 4px;
    text-decoration: none;
    font-weight: 700; /* font-weight: 700 */ — Define a espessura da fonte como negrito padrão (Bold).
    transition: var(--transition-smooth);
}

.btn-primary:hover {
    transform: translateY(-2px); /* transform: translateY(-2px) */ — Move o botão mecanicamente 2 pixels para cima no eixo vertical quando o mouse passa por cima, dando a impressão de flutuação.
    box-shadow: 0 0 25px rgba(72, 202, 228, 0.5); /* box-shadow: 0 0 25px rgba(72, 202, 228, 0.5) */ — Projeta um brilho de neon maior e mais intenso (25px de raio de desfoque).
}

.btn-secondary {
    display: inline-block;
    background-color: var(--brand-deep-blue);
    color: var(--text-primary);
    padding: 0.875rem 2rem;
    border-radius: 4px;
    text-decoration: none;
    font-weight: 700;
    border: var(--border-glow); /* border: var(--border-glow) */ — Aplica a variável de borda fina e brilhante a este componente.
    transition: var(--transition-smooth);
}

.btn-secondary:hover {
    background-color: rgba(28, 37, 65, 0.6); /* background-color: rgba(28, 37, 65, 0.6) */ — Altera o fundo do botão secundário para uma versão com 60% de opacidade da cor original.
    color: var(--brand-electric);
    transform: translateY(-2px);
}

/* ==========================================================================
   MAIN STRUCTURE & SECTIONS
   --------------------------------------------------------------------------
   Explica como delimitar seções e trabalhar com pseudo-elementos (`::after`) 
   para decorações puramente visuais via CSS.
   ========================================================================== */

.main-content {
    margin-top: 80px; /* margin-top: 80px */ — Empurra todo o conteúdo do site 80px para baixo. Isso impede que o cabeçalho fixo tampe o início do texto principal.
}

.section-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 6rem 2rem; /* padding: 6rem 2rem */ — Aplica um espaçamento vertical generoso (6rem = 96px) para dar "respiro" visual entre as seções.
}

.section-title {
    font-family: 'Syne', sans-serif;
    font-size: 2.25rem; /* font-size: 2.25rem */ — Define o tamanho padrão dos títulos de seções (36px).
    font-weight: 700;
    margin-bottom: 3rem; /* margin-bottom: 3rem */ — Espaço de 48px adicionado abaixo do título para separá-lo do conteúdo que vem em seguida.
    position: relative; /* position: relative */ — Torna este título uma "âncora" de referência posicional para os elementos filhos ou pseudo-elementos que usarem posicionamento absoluto.
    display: inline-block;
}

/* Linha estilizada abaixo do título da seção */
.section-title::after {
    content: ''; /* content: '' */ — Obrigatório para que um pseudo-elemento funcione. Diz ao navegador para renderizar uma caixa invisível de conteúdo vazio.
    position: absolute; /* position: absolute */ — Posiciona o elemento de forma livre, usando como referência o pai mais próximo que tenha `position: relative` (no caso, `.section-title`).
    bottom: -8px; /* bottom: -8px */ — Posiciona a linha decorativa exatamente 8px abaixo da parte inferior do texto do título.
    left: 0; — Alinha o início da linha exatamente no canto esquerdo do título.
    width: 40px; /* width: 40px */ — Define que a linha decorativa terá 40px de largura física.
    height: 3px; /* height: 3px */ — Define a espessura vertical da linha decorativa em 3px.
    background-color: var(--brand-electric);
}

/* ==========================================================================
   HERO SECTION
   --------------------------------------------------------------------------
   Introduz o CSS Grid Layout e cálculos avançados de dimensões fluídas.
   ========================================================================== */

.hero-section {
    min-height: calc(100vh - 80px); /* min-height: calc(100vh - 80px) */ — Garante que a seção ocupe pelo menos a altura inteira da tela (100vh) subtraindo os 80px do cabeçalho.
    display: flex;
    align-items: center;
    background: radial-gradient(circle at 80% 20%, rgba(28, 37, 65, 0.4) 0%, rgba(5, 8, 11, 0) 50%); /* background: radial-gradient(...) */ — Define um gradiente circular luminoso focado na parte superior direita para simular um efeito de iluminação de fundo.
}

.hero-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 4rem 2rem; /* padding: 4rem 2rem */ — Define espaçamento interno de 4rem (64px) em cima e embaixo.
    display: grid; /* display: grid */ — Ativa o poderoso sistema de layout bidimensional (CSS Grid).
    grid-template-columns: 1.2fr 0.8fr; /* grid-template-columns: 1.2fr 0.8fr */ — Divide o espaço em duas colunas proporcionais: a primeira tem peso 1.2 e a segunda tem peso 0.8 na distribuição.
    gap: 4rem; /* gap: 4rem */ — Adiciona um espaçamento de 64px entre as colunas e linhas do grid.
    align-items: center;
}

.hero-tag {
    color: var(--brand-electric);
    font-weight: 700;
    font-size: 0.875rem; /* font-size: 0.875rem */ — Define a fonte como 14px para textos informativos superiores de tags.
    letter-spacing: 2px; /* letter-spacing: 2px */ — Espaça as letras em 2px para dar um aspecto estético moderno e focado.
    display: block; /* display: block */ — Força o elemento a se comportar como um bloco, jogando qualquer texto que venha depois para a linha de baixo.
    margin-bottom: 1rem; /* margin-bottom: 1rem */ — Cria um espaço de 16px abaixo da tag.
}

.hero-title {
    font-family: 'Syne', sans-serif;
    font-size: 3.5rem; /* font-size: 3.5rem */ — Tamanho imponente para o título principal da página (56px).
    font-weight: 800;
    line-height: 1.1; /* line-height: 1.1 */ — Reduz a altura da linha para 1.1. Isso impede que títulos gigantes com quebras de linha fiquem muito espalhados na vertical.
    margin-bottom: 1.5rem; /* margin-bottom: 1.5rem */ — Espaçamento de 24px abaixo do título principal.
    letter-spacing: -1px;
}

.hero-subtitle {
    color: var(--text-muted);
    font-size: 1.2rem; /* font-size: 1.2rem */ — Define o tamanho do subtítulo como ligeiramente maior que o texto padrão (cerca de 19px).
    line-height: 1.6; /* line-height: 1.6 */ — Aumenta a altura da linha para 1.6, garantindo conforto e legibilidade na leitura de parágrafos.
    margin-bottom: 2.5rem; /* margin-bottom: 2.5rem */ — Espaçamento de 40px antes dos botões de ação.
    max-width: 540px; /* max-width: 540px */ — Limita o comprimento do parágrafo em 540px para que as linhas não fiquem excessivamente longas e cansativas de ler.
}

.hero-actions {
    display: flex;
    gap: 1.5rem; /* gap: 1.5rem */ — Define espaço de 24px entre os botões da hero.
}

/* Container de placeholder visual do lado direito da Hero */
.hero-visual {
    display: flex;
    justify-content: center; /* justify-content: center */ — Alinha o conteúdo interno horizontalmente no centro do container.
    align-items: center;
}

.visual-box-placeholder {
    width: 100%;
    height: 400px; /* height: 400px */ — Fixa a altura do bloco placeholder em 400px.
    background-color: var(--bg-dark-surface); /* background-color: var(--bg-dark-surface) */ — Aplica a cor de superfície escura como fundo da caixa.
    border: var(--border-glow);
    border-radius: 8px; /* border-radius: 8px */ — Arredonda os cantos da caixa visual em 8px.
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    box-shadow: 0 20px 40px rgba(0,0,0,0.5); /* box-shadow: 0 20px 40px rgba(0,0,0,0.5) */ — Projeta uma sombra escura e pesada para baixo (20px de deslocamento vertical e 40px de espalhamento), dando efeito de profundidade 3D na interface.
}

.visual-glitch-text {
    font-size: 0.875rem;
    font-family: monospace; /* font-family: monospace */ — Altera a tipografia para fontes monoespaçadas (estilo código de programação).
    color: var(--brand-electric);
    letter-spacing: 1px; /* letter-spacing: 1px */ — Afasta as letras em 1px para melhorar a estética monoespaçada.
}

/* ==========================================================================
   ABOUT SECTION
   --------------------------------------------------------------------------
   Utilização básica de flex-grow ou distribuição flexível simplificada.
   ========================================================================== */

.about-section {
    background-color: rgba(11, 19, 43, 0.3); /* background-color: rgba(11, 19, 43, 0.3) */ — Aplica uma variação de fundo com 30% de opacidade do azul escuro estrutural.
    border-top: var(--border-glow); /* border-top: var(--border-glow) */ — Cria uma linha brilhante delimitadora no topo da seção.
    border-bottom: var(--border-glow);
}

.about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr; /* grid-template-columns: 1fr 1fr */ — Cria duas colunas idênticas, divididas igualmente em frações de espaço (50% cada).
    gap: 4rem;
    align-items: center;
}

.about-text p {
    color: var(--text-muted);
    font-size: 1.15rem; /* font-size: 1.15rem */ — Tamanho de fonte intermediário confortável para blocos textuais informativos.
    line-height: 1.7; /* line-height: 1.7 */ — Altura de linha confortável para blocos longos de texto.
}

.about-highlights {
    display: flex;
    gap: 2rem;
}

.highlight-card {
    background-color: var(--bg-dark-surface);
    border: var(--border-glow);
    padding: 2rem; /* padding: 2rem */ — Espaçamento interno padrão de 32px nos quatro lados da caixa.
    border-radius: 6px; /* border-radius: 6px */ — Cantos ligeiramente arredondados em 6px.
    flex: 1; /* flex: 1 */ — Faz com que as caixas filhas em um layout flex se expandam igualmente de forma idêntica para preencher o espaço disponível.
    text-align: center; /* text-align: center */ — Centraliza todos os textos que estão dentro deste cartão.
}

.card-number {
    display: block;
    font-family: 'Syne', sans-serif;
    font-size: 2.5rem; /* font-size: 2.5rem */ — Tamanho ampliado (40px) para destacar números estatísticos.
    font-weight: 800;
    color: var(--brand-electric);
    margin-bottom: 0.5rem; /* margin-bottom: 0.5rem */ — Pequeno espaço de 8px abaixo do número.
}

.card-label {
    color: var(--text-muted);
    font-size: 0.9rem; /* font-size: 0.9rem */ — Texto reduzido para rotulagem secundária.
    text-transform: uppercase; /* text-transform: uppercase */ — Transforma todas as letras deste rótulo em maiúsculas de forma automática.
    letter-spacing: 1px;
}

/* ==========================================================================
   STATS & CARDS (Uso de Grid Layout)
   --------------------------------------------------------------------------
   O aluno aprenderá funções de repetição estruturadas (`repeat()`).
   ========================================================================== */

.cards-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr); /* grid-template-columns: repeat(3, 1fr) */ — Atalho para criar 3 colunas de tamanhos perfeitamente idênticos (1fr 1fr 1fr).
    gap: 2rem;
}

.stat-card {
    background-color: var(--bg-dark-surface);
    border: var(--border-glow);
    padding: 2.5rem 2rem; /* padding: 2.5rem 2rem */ — Ajusta 40px em cima e embaixo, e 32px nas laterais para melhor diagramação interna.
    border-radius: 8px;
    transition: var(--transition-smooth);
}

.stat-card:hover {
    transform: translateY(-5px); /* transform: translateY(-5px) */ — Eleva o card em 5px quando o usuário passa o mouse por cima, simulando uma interação reativa física de profundidade.
    border-color: var(--brand-electric); /* border-color: var(--brand-electric) */ — Troca a cor sutil da borda para o azul elétrico aceso de alto contraste.
    box-shadow: 0 10px 30px rgba(72, 202, 228, 0.1); /* box-shadow: 0 10px 30px rgba(72, 202, 228, 0.1) */ — Projeta uma sombra azul neon bem suave (10% de opacidade) com desfoque de 30px abaixo do card.
}

.stat-title {
    font-size: 1rem; /* font-size: 1rem */ — Fixa o tamanho do título em 1rem (16px).
    color: var(--text-muted);
    margin-bottom: 1rem;
}

.stat-value {
    font-family: 'Syne', sans-serif;
    font-size: 3rem; /* font-size: 3rem */ — Número gigante de destaque de 48px para dados importantes.
    font-weight: 700;
    color: var(--text-primary);
    margin-bottom: 0.5rem;
}

.stat-detail {
    font-size: 0.85rem; /* font-size: 0.85rem */ — Define o menor tamanho de texto do projeto (13.6px) para detalhes explicativos.
    color: var(--brand-electric);
    display: block;
}

/* ==========================================================================
   SETUP SECTION
   --------------------------------------------------------------------------
   Trabalha com listas sem formatação nativa e larguras em elementos em linha.
   ========================================================================== */

.setup-section {
    background-color: var(--bg-dark-absolute);
}

.setup-list {
    list-style: none; /* list-style: none */ — Remove os marcadores circulares padrão (as famosas "bolinhas") que as listas `<ul>` ou `<li>` possuem por padrão.
    max-width: 600px; /* max-width: 600px */ — Limita o comprimento horizontal total da lista a 600px.
}

.setup-item {
    padding: 1rem 0; /* padding: 1rem 0 */ — Aplica 1rem (16px) de espaçamento interno em cima e embaixo, e zero nas laterais.
    border-bottom: 1px solid rgba(148, 163, 184, 0.1); /* border-bottom: 1px solid rgba(148, 163, 184, 0.1) */ — Cria uma linha divisória horizontal muito discreta (10% de opacidade) na parte de baixo de cada item.
    color: var(--text-muted);
    font-size: 1.1rem; /* font-size: 1.1rem */ — Define o tamanho da fonte ligeiramente maior (cerca de 17.6px).
}

.setup-item strong {
    color: var(--text-primary);
    display: inline-block;
    width: 150px; /* width: 150px */ — Força a tag `<strong>` (que normalmente não aceita largura por ser inline) a herdar comportamento de bloco e possuir tamanho fixo de 150px. Isso alinha todos os textos seguintes como em uma tabela perfeita.
}

/* ==========================================================================
   FOOTER
   --------------------------------------------------------------------------
   Configuração clássica de encerramento da interface.
   ========================================================================== */

.main-footer {
    background-color: #03050a; /* background-color: #03050a */ — Define um tom quase preto puro (mais escuro que as outras áreas) para fechar a composição do site.
    border-top: var(--border-glow);
    padding: 3rem 2rem; /* padding: 3rem 2rem */ — Ajusta 48px de espaçamento interno superior/inferior para o rodapé.
}

.footer-container {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.footer-copy {
    color: var(--text-muted);
    font-size: 0.9rem;
}

.footer-socials {
    display: flex;
    gap: 1.5rem;
}

.social-link {
    color: var(--text-muted);
    text-decoration: none;
    font-size: 0.9rem;
    font-weight: 600;
    transition: var(--transition-smooth);
}

.social-link:hover {
    color: var(--brand-electric);
}

/* ==========================================================================
   RESPONSIVIDADE BÁSICA (Dica extra de aula)
   --------------------------------------------------------------------------
   O aluno aprenderá o conceito de Mobile-First ou adaptação responsiva.
   ========================================================================== */

@media (max-width: 968px) { /* @media (max-width: 968px) */ — Regra condicional: todas as linhas dentro deste bloco só serão executadas se a tela do dispositivo tiver 968 pixels de largura ou menos (telas de tablets e celulares).
    .hero-container, .about-grid, .cards-grid {
        grid-template-columns: 1fr; /* grid-template-columns: 1fr */ — Altera a divisão de colunas múltiplas das telas grandes para apenas 1 única coluna vertical, empilhando todos os elementos para caber em telas estreitas.
        gap: 2.5rem; /* gap: 2.5rem */ — Reduz levemente o espaçamento de separação para 40px para economizar área útil no dispositivo menor.
    }
    .hero-title {
        font-size: 2.5rem;
    }
    .footer-container {
        flex-direction: column; /* flex-direction: column */ — Muda a distribuição do Flexbox do rodapé de horizontal (linha) para vertical (coluna). Os elementos agora ficam um em cima do outro.
        gap: 1.5rem;
        text-align: center;
    }
}
```

Acima uma descrição de cada uma das classes e elementos do código CSS utilizados. Os comentários são importantes para entender o código e para ajudar a entender o que está sendo feito.