Documentação do Projeto: Portal de Jogos Infantis 🎮
Este projeto acadêmico consiste em uma plataforma web interativa voltada para o público infantil. O objetivo principal é unir o entretenimento ao desenvolvimento cognitivo, oferecendo dois jogos clássicos: o Jogo da Velha (que estimula a estratégia e a convivência) e o Jogo da Memória (que exercita a fixação visual e a concentração).
🛠️ 1. Como o Jogo Foi Feito (Arquitetura e Tecnologias)
Para garantir que o projeto fosse extremamente leve, rápido e acessível a qualquer tipo de dispositivo (computadores, celulares ou tablets), ele foi desenvolvido utilizando exclusivamente tecnologias nativas da web, sem a necessidade de instalar bibliotecas de terceiros ou frameworks pesados.
O código foi estruturado em três pilares fundamentais:
1. HTML5 (Estrutura): Define o "esqueleto" da aplicação. É responsável por criar os botões do menu, as caixas de exibição de texto, as 9 casas do Jogo da Velha e os blocos dinâmicos onde as cartas do Jogo da Memória são inseridas.
2. CSS3 (Design e Visual Lúdico): Dá vida ao projeto. Utiliza uma paleta de cores vibrantes, bordas arredondadas e efeitos de sombra em bloco (estilo cartoon) para atrair a atenção das crianças.
 Destaques técnicos: Uso de CSS Grid para alinhar perfeitamente os tabuleiros e a propriedade ⁠user-select: none⁠, que impede que a criança selecione os textos ou borre a tela caso clique muito rápido várias vezes seguidas.
3. JavaScript (Lógica e Interatividade): É o "cérebro" do sistema. Ele gerencia as regras dos dois jogos, controla de quem é a vez, embaralha as cartas aleatoriamente a cada nova partida e calcula automaticamente as condições de vitória ou empate.
🚀 2. Como Executar o Jogo (Manual de Instalação)
Uma das maiores vantagens dessa arquitetura é a simplicidade de execução. Qualquer pessoa, mesmo sem conhecimento técnico, consegue rodar o jogo de duas formas:
Opção A: Execução Online (Sem instalar nada)
Caso o projeto já esteja hospedado (por exemplo, no GitHub Pages), o público só precisa de um navegador de internet e acesso à rede:
1. Abra o navegador de sua preferência (Google Chrome, Safari, Edge ou Firefox).
2. Digite o endereço web do portal (ex: ⁠https://adspatrick.github.io/JOGOSINFANTISAV3/⁠).
3. O jogo carregará instantaneamente.
Opção B: Execução Local/Offline (Para apresentar na aula)
Se você estiver rodando os arquivos direto do seu computador ou pendrive:
1. Certifique-se de que o arquivo de código está salvo com o nome ⁠index.html⁠ dentro de uma pasta.
2. Vá até a pasta onde o arquivo foi salvo.
3. Dê um duplo clique sobre o arquivo ⁠index.html⁠.
4. Ele abrirá automaticamente no seu navegador padrão e estará pronto para ser jogado, mesmo se o computador estiver totalmente sem internet.

5.Aqui esta o codigo comentado!
6.  <!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8"> 
    <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
    <title>Meu Portal de Jogos Infantil</title>

    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@300..700&display=swap" rel="stylesheet">
    <style>
        /* ==========================================================================
           ESTILOS GERAIS E ESTRUTURA DA PÁGINA (CSS)
           ========================================================================== */
        body {
            background-color: #e0f2fe; 
            background-image: url('kids.jpg'); 
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            background-attachment: fixed; 
            
            font-family: "Fredoka", sans-serif; 
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh; 
            margin: 0;
            /* Evita seleção acidental de texto por crianças clicando rapidamente */
            user-select: none; 
        }

        h1 {
            color: #fff;
            font-size: 3.2rem;
            text-shadow: 4px 4px 0px #f15bb5, -2px -2px 0px #000; 
            margin-bottom: 5px;
            letter-spacing: 2px;
            text-align: center;
        }

        #status {
            color: #333;
            font-size: 1.5rem;
            font-weight: 600;
            margin-bottom: 20px;
            background-color: #ffffff;
            padding: 12px 30px;
            border-radius: 50px; 
            box-shadow: 0px 6px 0px #dddddd; 
            text-align: center;
        }

        .tela-menu {
            display: flex;
            flex-direction: column;
            gap: 20px;
            background-color: rgba(255, 255, 255, 0.9); 
            padding: 30px;
            border-radius: 40px;
            box-shadow: 0px 12px 0px #ccc;
            align-items: center;
        }

        .btn-menu {
            width: 260px;
            padding: 20px;
            font-family: "Fredoka", sans-serif;
            font-size: 1.6rem;
            font-weight: bold;
            color: white;
            border: none;
            border-radius: 30px;
            cursor: pointer;
            transition: transform 0.1s;
        }

        .btn-menu:active { transform: translateY(6px); box-shadow: none; }
        #btn-escolha-velha { background-color: #ff0054; box-shadow: 0px 8px 0px #c9003c; }
        #btn-escolha-memoria { background-color: #00b4d8; box-shadow: 0px 8px 0px #0090ad; }

        /* Classe utilitária para controle de fluxo de telas via JS */
        .escondido { display: none !important; }

        /* Renderização dos tabuleiros utilizando CSS Grid para controle de matriz */
        .tabuleiro-velha {
            display: grid;
            grid-template-columns: repeat(3, 105px); 
            grid-template-rows: repeat(3, 105px);    
            gap: 15px; 
            background-color: #fee440; 
            padding: 20px;
            border-radius: 40px; 
            box-shadow: 0px 12px 0px #f5cb00;
        }

        .tabuleiro-memoria {
            display: grid;
            grid-template-columns: repeat(4, 85px); 
            grid-template-rows: repeat(3, 85px);    
            gap: 12px; 
            background-color: #9b5de5; 
            padding: 20px;
            border-radius: 40px; 
            box-shadow: 0px 12px 0px #7b3fc3;
        }

        .quadrado {
            border: none;
            border-radius: 25px; 
            font-size: 3.5rem;
            cursor: pointer;
            transition: transform 0.1s;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #fff;
        }

        /* Cores individuais simulando padrão arco-íris para o Jogo da Velha */
        .tabuleiro-velha .quadrado:nth-child(1) { background-color: #ff0054; box-shadow: 0px 6px 0px #c9003c; }
        .tabuleiro-velha .quadrado:nth-child(2) { background-color: #ff5400; box-shadow: 0px 6px 0px #cc4300; }
        .tabuleiro-velha .quadrado:nth-child(3) { background-color: #ffbd00; box-shadow: 0px 6px 0px #cca000; }
        .tabuleiro-velha .quadrado:nth-child(4) { background-color: #70e000; box-shadow: 0px 6px 0px #59b300; }
        .tabuleiro-velha .quadrado:nth-child(5) { background-color: #38b000; box-shadow: 0px 6px 0px #2c8c00; }
        .tabuleiro-velha .quadrado:nth-child(6) { background-color: #00b4d8; box-shadow: 0px 6px 0px #0090ad; }
        .tabuleiro-velha .quadrado:nth-child(7) { background-color: #0077b6; box-shadow: 0px 6px 0px #005f91; }
        .tabuleiro-velha .quadrado:nth-child(8) { background-color: #f15bb5; box-shadow: 0px 6px 0px #c74393; }
        .tabuleiro-velha .quadrado:nth-child(9) { background-color: #00f5d4; box-shadow: 0px 6px 0px #00c2a8; }

        .carta {
            background-color: #fee440; 
            box-shadow: 0px 6px 0px #f5cb00;
            font-size: 2.8rem;
            color: initial;
        }

        .carta.virada {
            background-color: #fff !important;
            box-shadow: 0px 6px 0px #ccc !important;
        }

        .quadrado:active { transform: translateY(6px); box-shadow: none; }

        .botoes-container {
            display: flex;
            gap: 15px;
            margin-top: 25px;
        }

        .btn-controle {
            padding: 12px 25px;
            font-size: 1.2rem;
            font-family: "Fredoka", sans-serif;
            font-weight: bold;
            color: #000;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.1s;
        }

        #btn-reiniciar { background-color: #00f5d4; box-shadow: 0px 6px 0px #00bda4; }
        #btn-voltar { background-color: #ffbd00; box-shadow: 0px 6px 0px #cca000; }
        .btn-controle:active { transform: translateY(6px); box-shadow: none; }
    </style>
</head>
<body>

    <h1 id="titulo-principal">MENU DE JOGOS! 🎮</h1>
    
    <div id="status" class="escondido">Vez do jogador: 🌟</div>

    <div id="menu-inicial" class="tela-menu">
        <button id="btn-escolha-velha" class="btn-menu" onclick="abrirJogo('velha')">Jogo da Velha 🎈</button>
        <button id="btn-escolha-memoria" class="btn-menu" onclick="abrirJogo('memoria')">Jogo da Memória 🧸</button>
    </div>

    <div id="jogo-velha" class="tabuleiro-velha escondido">
        <button class="quadrado" onclick="jogarVelha(this, 0)"></button>
        <button class="quadrado" onclick="jogarVelha(this, 1)"></button>
        <button class="quadrado" onclick="jogarVelha(this, 2)"></button>
        <button class="quadrado" onclick="jogarVelha(this, 3)"></button>
        <button class="quadrado" onclick="jogarVelha(this, 4)"></button>
        <button class="quadrado" onclick="jogarVelha(this, 5)"></button>
        <button class="quadrado" onclick="jogarVelha(this, 6)"></button>
        <button class="quadrado" onclick="jogarVelha(this, 7)"></button>
        <button class="quadrado" onclick="jogarVelha(this, 8)"></button>
    </div>

    <div id="jogo-memoria" class="tabuleiro-memoria escondido"></div>

    <div id="controles-jogo" class="botoes-container escondido">
        <button id="btn-reiniciar" class="btn-controle" onclick="reiniciarJogoAtual()">Reiniciar 🔄</button>
        <button id="btn-voltar" class="btn-controle" onclick="voltarMenu()">Mudar de Jogo 🏠</button>
    </div>

    <script>
        /* ==========================================================================
           VARIÁVEIS DE ESTADO E NAVEGAÇÃO GLOBAL
           ========================================================================== */
        
        /** @type {string} Armazena o identificador do jogo atualmente ativo ('velha' ou 'memoria') */
        let juegoSelecionado = ''; 

        /* --- Estado: Jogo da Velha --- */
        /** @type {string} Símbolo do jogador da vez ('🌟' ou '🌈') */
        let turnoAtual = '🌟'; 
        /** @type {string[]} Representação da matriz 3x3 do tabuleiro em array unidimensional */
        let tabuleiroVelhaAtivo = ['', '', '', '', '', '', '', '', ''];
        /** @type {boolean} Define se a partida em curso já chegou ao fim */
        let jogoVelhaFinalizado = false;

        /* --- Estado: Jogo da Memória --- */
        /** @readonly @type {string[]} Banco de dados fixo contendo os 6 pares de emojis do jogo */
        const emojisMemoria = ['🐶', '🐶', '🦁', '🦁', '🐸', '🐸', '🚀', '🚀', '🦄', '🦄', '🦕', '🦕'];
        /** @type {HTMLElement[]} Cache temporário para armazenar até duas cartas selecionadas na rodada */
        let cartasViradas = []; 
        /** @type {boolean} Semáforo de controle para travar cliques extras durante a animação de erro */
        let cartasBloqueadas = false; 
        /** @type {number} Contador de acertos para verificar a condição de vitória absoluta */
        let paresEncontrados = 0; 


        /* ==========================================================================
           FUNÇÕES DE ROTEAMENTO E FLUXO DE TELAS
           ========================================================================== */

        /**
         * Inicializa o ambiente e renderiza a tela do jogo escolhido pelo usuário.
         * @param {string} jogo - O identificador do jogo ('velha' ou 'memoria').
         */
        function abrirJogo(jogo) {
            juegoSelecionado = jogo; 
            
            // Gerencia exibição de containers ocultando o menu e revelando o painel de controle
            document.getElementById('menu-inicial').classList.add('escondido');
            document.getElementById('status').classList.remove('escondido');
            document.getElementById('controles-jogo').classList.remove('escondido');

            if (jogo === 'velha') {
                document.getElementById('titulo-principal').innerText = "JOGO DA VELHA! 🎈";
                document.getElementById('jogo-velha').classList.remove('escondido');
                reiniciarVelha();
            } else {
                document.getElementById('titulo-principal').innerText = "JOGO DA MEMÓRIA! 🧸";
                document.getElementById('jogo-memoria').classList.remove('escondido');
                inicializarMemoria();
            }
        }

        /**
         * Retorna a aplicação para o estado inicial, redefinindo elementos visuais do menu.
         */
        function voltarMenu() {
            document.getElementById('menu-inicial').classList.remove('escondido');
            document.getElementById('status').classList.add('escondido');
            document.getElementById('controles-jogo').classList.add('escondido');
            document.getElementById('jogo-velha').classList.add('escondido');
            document.getElementById('jogo-memoria').classList.add('escondido');
            document.getElementById('titulo-principal').innerText = "MENU DE JOGOS! 🎮";
            juegoSelecionado = ''; 
        }

        /**
         * Direciona a requisição de reinício para o escopo do jogo ativo no momento.
         */
        function reiniciarJogoAtual() {
            if (juegoSelecionado === 'velha') reiniciarVelha();
            else inicializarMemoria();
        }


        /* ==========================================================================
           LÓGICA DO JOGO DA VELHA
           ========================================================================== */

        /**
         * Reseta completamente as variáveis de estado e o conteúdo visual do Jogo da Velha.
         */
        function reiniciarVelha() {
            turnoAtual = '🌟';
            tabuleiroVelhaAtivo = ['', '', '', '', '', '', '', '', ''];
            jogoVelhaFinalizado = false;
            document.getElementById('status').innerText = "Vez do jogador: " + turnoAtual;
            
            const quadrados = document.querySelectorAll('#jogo-velha .quadrado');
            quadrados.forEach(quadrado => {
                quadrado.innerText = '';
            });
        }

        /**
         * Processa a jogada de um usuário ao clicar em uma célula do tabuleiro da velha.
         * @param {HTMLButtonElement} botao - O elemento HTML do botão que foi clicado.
         * @param {number} indice - A posição equivalente no array de estado (0 a 8).
         */
        function jogarVelha(botao, indice) {
            // Cláusula de barreira: impede jogadas em casas ocupadas ou se o jogo acabou
            if (tabuleiroVelhaAtivo[indice] !== '' || jogoVelhaFinalizado) return;

            // Registra a jogada no estado lógico e renderiza na interface
            tabuleiroVelhaAtivo[indice] = turnoAtual;
            botao.innerText = turnoAtual;

            // Verificação de Vitória
            if (verificarVitoriaVelha()) {
                document.getElementById('status').innerText = "Parabéns! O jogador " + turnoAtual + " ganhou! 🎉🏆";
                jogoVelhaFinalizado = true;
                return;
            }

            // Verificação de Empate (Falta de espaços vazios)
            if (!tabuleiroVelhaAtivo.includes('')) {
                document.getElementById('status').innerText = "Deu empate! Que tal jogar de novo? 🤪";
                jogoVelhaFinalizado = true;
                return;
            }

            // Alternância de turno
            turnoAtual = (turnoAtual === '🌟') ? '🌈' : '🌟';
            document.getElementById('status').innerText = "Vez do jogador: " + turnoAtual;
        }

        /**
         * Varre o tabuleiro mapeando vetores estáticos para encontrar combinações de vitória.
         * @returns {boolean} Retorna verdadeiro se alguma combinação linear foi atingida.
         */
        function verificarVitoriaVelha() {
            const combinacoesVitoria = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8], // Horizontais
                [0, 3, 6], [1, 4, 7], [2, 5, 8], // Verticais
                [0, 4, 8], [2, 4, 6]             // Diagonais
            ];

            return combinacoesVitoria.some(combinacao => {
                const [a, b, c] = combinacao;
                return tabuleiroVelhaAtivo[a] !== '' && 
                       tabuleiroVelhaAtivo[a] === tabuleiroVelhaAtivo[b] && 
                       tabuleiroVelhaAtivo[a] === tabuleiroVelhaAtivo[c];
            });
        }


        /* ==========================================================================
           LÓGICA DO JOGO DA MEMÓRIA
           ========================================================================== */

        /**
         * Prepara o tabuleiro da memória limpando o lixo do DOM, embaralhando os pares e renderizando as cartas.
         */
        function inicializarMemoria() {
            paresEncontrados = 0;
            cartasViradas = [];
            cartasBloqueadas = false;
            document.getElementById('status').innerText = "Encontre os pares! 🔍";
            
            // Embaralha o vetor de emojis usando um algoritmo adaptado (Sort com desvio randômico)
            const emojisEmbaralhados = [...emojisMemoria].sort(() => Math.random() - 0.5);
            const container = document.getElementById('jogo-memoria');
            container.innerHTML = ''; 
            
            // Injeção de componentes de cartas de forma dinâmica no DOM
            emojisEmbaralhados.forEach((emoji, indice) => {
                const botaoCarta = document.createElement('button');
                botaoCarta.classList.add('quadrado', 'carta');
                
                // Atribuição de metadados via HTML5 Dataset (Esconde dados lógicos na árvore do DOM)
                botaoCarta.dataset.emoji = emoji; 
                botaoCarta.dataset.indice = indice;
                botaoCarta.innerText = '❓'; 
                
                botaoCarta.onclick = function() { virarCarta(this); };
                container.appendChild(botaoCarta); 
            });
        }

        /**
         * Executa a regra de negócio do clique e revelação das cartas da memória.
         * @param {HTMLButtonElement} cartaClicada - Elemento HTML da carta acionada.
         */
        function virarCarta(cartaClicada) {
            // Impede cliques em cartas já abertas ou durante o bloqueio temporário
            if (cartasBloqueadas || cartaClicada.classList.contains('virada')) return;

            // Altera visual para estado virado revelando o metadado
            cartaClicada.classList.add('virada'); 
            cartaClicada.innerText = cartaClicada.dataset.emoji; 
            cartasViradas.push(cartaClicada); 

            // Avalia se um par de cartas foi formado na rodada atual
            if (cartasViradas.length === 2) {
                cartasBloqueadas = true; 
                const [carta1, carta2] = cartasViradas; 

                // Caso de Sucesso: As cartas possuem o mesmo emoji?
                if (carta1.dataset.emoji === carta2.dataset.emoji) {
                    paresEncontrados++;
                    cartasViradas = []; 
                    cartasBloqueadas = false; 
                    
                    // Valida se a totalidade de pares da base foi encontrada
                    if (paresEncontrados === emojisMemoria.length / 2) {
                        document.getElementById('status').innerText = "Incrível! Você achou tudo! 🎉🥳";
                    }
                } else {
                    // Caso de Erro: Mantém cartas abertas por 1000ms para fixação visual da criança, depois desvira
                    setTimeout(() => {
                        carta1.classList.remove('virada');
                        carta2.classList.remove('virada');
                        carta1.innerText = '❓'; 
                        carta2.innerText = '❓';
                        cartasViradas = []; 
                        cartasBloqueadas = false; 
                    }, 1000);
                }
            }
        }
    </script>
</body>
</html>
