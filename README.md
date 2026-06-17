# 🎮 Portal de Jogos Infantil

Este repositório contém um portal de jogos focado no público infantil, desenvolvido inteiramente com **HTML5, CSS3 e JavaScript Vanila**. O projeto é responsivo, possui uma identidade visual alegre e conta com dois jogos clássicos: **Jogo da Velha** e **Jogo da Memória**.

Abaixo está a documentação técnica detalhada de cada seção do código-fonte para fins acadêmicos.

---

## 🛠️ Documentação do Código (Seção por Seção)

<details>
<summary><b>1. Estrutura Inicial e Metadados (HTML Head)</b></summary>

Definições básicas do documento, configurações de responsividade para dispositivos móveis e importação de fontes externas.

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8"> <meta name="viewport" content="width=device-width, initial-scale=1.0"> <title>Meu Portal de Jogos Infantil</title>

    <link rel="preconnect" href="[https://fonts.googleapis.com](https://fonts.googleapis.com)">
    <link rel="preconnect" href="[https://fonts.gstatic.com](https://fonts.gstatic.com)" crossorigin>
    <link href="[https://fonts.googleapis.com/css2?family=Fredoka:wght@300..700&display=swap](https://fonts.googleapis.com/css2?family=Fredoka:wght@300..700&display=swap)" rel="stylesheet">
    <style>
        /* Configuração do plano de fundo e centralização absoluta dos elementos na tela */
        body {
            background-color: #e0f2fe; /* Cor de fallback caso a imagem de fundo falhe ou demore a carregar */
            background-image: url('kids.jpg'); /* Imagem de fundo temática */
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            background-attachment: fixed; /* Efeito de fundo estático durante a rolagem */
            
            font-family: "Fredoka", sans-serif; 
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh; /* Ocupa no mínimo 100% da altura da janela de visualização */
            margin: 0;
            user-select: none; /* Desabilita a seleção de texto para evitar que a criança selecione elementos acidentalmente ao clicar rápido */
        }

        /* Título principal com efeito de contorno/sombra em bloco */
        h1 {
            color: #fff;
            font-size: 3.2rem;
            text-shadow: 4px 4px 0px #f15bb5, -2px -2px 0px #000; 
            margin-bottom: 5px;
            letter-spacing: 2px;
            text-align: center;
        }

        /* Painel flutuante que exibe as instruções e o estado atual do jogo */
        #status {
            color: #333;
            font-size: 1.5rem;
            font-weight: 600;
            margin-bottom: 20px;
            background-color: #ffffff;
            padding: 12px 30px;
            border-radius: 50px; 
            box-shadow: 0px 6px 0px #dddddd; /* Sombra sólida sem desfoque (efeito cartoon) */
            text-align: center;
        }

        /* Container do Menu de Seleção de Jogos */
        .tela-menu {
            display: flex;
            flex-direction: column;
            gap: 20px;
            background-color: rgba(255, 255, 255, 0.9); /* Fundo branco com 90% de opacidade */
            padding: 30px;
            border-radius: 40px;
            box-shadow: 0px 12px 0px #ccc;
            align-items: center;
        }

        /* Estilização base dos botões do Menu */
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

        /* Efeito de clique: desloca o botão ligeiramente para baixo e remove a sombra, simulando pressão física */
        .btn-menu:active { transform: translateY(6px); box-shadow: none; }
        #btn-escolha-velha { background-color: #ff0054; box-shadow: 0px 8px 0px #c9003c; }
        #btn-escolha-memoria { background-color: #00b4d8; box-shadow: 0px 8px 0px #0090ad; }

        /* Classe utilitária fundamental: manipula o fluxo de exibição das telas via JavaScript */
        .escondido { display: none !important; }

        /* Matriz 3x3 do Jogo da Velha controlada por CSS Grid */
        .tabuleiro-velha {
            display: grid;
            grid-template-columns: repeat(3, 105px); /* Três colunas de tamanho fixo */
            grid-template-rows: repeat(3, 105px);    /* Três linhas de tamanho fixo */
            gap: 15px; 
            background-color: #fee440; 
            padding: 20px;
            border-radius: 40px; 
            box-shadow: 0px 12px 0px #f5cb00;
        }

        /* Matriz 4x3 do Jogo da Memória (suporta as 12 cartas do jogo) */
        .tabuleiro-memoria {
            display: grid;
            grid-template-columns: repeat(4, 85px); /* Quatro colunas de tamanho fixo */
            grid-template-rows: repeat(3, 85px);    /* Três linhas de tamanho fixo */
            gap: 12px; 
            background-color: #9b5de5; 
            padding: 20px;
            border-radius: 40px; 
            box-shadow: 0px 12px 0px #7b3fc3;
        }

        /* Estilização genérica das células/botões internos dos tabuleiros */
        .quadrado {
            border: none;
            border-radius: 25px; 
            font-size: 3.5rem;
            cursor: pointer;
            transition: transform 0.1s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* Seletores pseudo-classe nth-child: aplicam cores individuais em padrão arco-íris para cada casa do Jogo da Velha */
        .tabuleiro-velha .quadrado:nth-child(1) { background-color: #ff0054; box-shadow: 0px 6px 0px #c9003c; }
        .tabuleiro-velha .quadrado:nth-child(2) { background-color: #ff5400; box-shadow: 0px 6px 0px #cc4300; }
        .tabuleiro-velha .quadrado:nth-child(3) { background-color: #ffbd00; box-shadow: 0px 6px 0px #cca000; }
        .tabuleiro-velha .quadrado:nth-child(4) { background-color: #70e000; box-shadow: 0px 6px 0px #59b300; }
        .tabuleiro-velha .quadrado:nth-child(5) { background-color: #38b000; box-shadow: 0px 6px 0px #2c8c00; }
        .tabuleiro-velha .quadrado:nth-child(6) { background-color: #00b4d8; box-shadow: 0px 6px 0px #0090ad; }
        .tabuleiro-velha .quadrado:nth-child(7) { background-color: #0077b6; box-shadow: 0px 6px 0px #005f91; }
        .tabuleiro-velha .quadrado:nth-child(8) { background-color: #f15bb5; box-shadow: 0px 6px 0px #c74393; }
        .tabuleiro-velha .quadrado:nth-child(9) { background-color: #00f5d4; box-shadow: 0px 6px 0px #00c2a8; }

        /* Estilo padrão da face oculta da carta da memória */
        .carta {
            background-color: #fee440; 
            box-shadow: 0px 6px 0px #f5cb00;
            font-size: 2.8rem;
        }

        /* Estilo aplicado dinamicamente quando a carta é revelada (virada) */
        .carta.virada {
            background-color: #fff !important;
            box-shadow: 0px 6px 0px #ccc !important;
        }

        .quadrado:active { transform: translateY(6px); box-shadow: none; }

        /* Bloco de alinhamento dos botões inferiores de controle */
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
        // Variável de estado global que armazena qual aplicação está sendo executada ('velha' ou 'memoria')
        let juegoSelecionado = ''; 

        // Função responsável por gerenciar a troca de telas (Roteamento)
        function abrirJogo(jogo) {
            juegoSelecionado = jogo; 
            // Oculta o menu inicial e exibe o cabeçalho de status e os botões de controle
            document.getElementById('menu-inicial').classList.add('escondido');
            document.getElementById('status').classList.remove('escondido');
            document.getElementById('controles-jogo').classList.remove('escondido');

            // Inicializa especificamente a estrutura do jogo selecionado
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

        // Retorna a aplicação para o estado inicial (Menu Principal)
        function voltarMenu() {
            document.getElementById('menu-inicial').classList.remove('escondido');
            document.getElementById('status').classList.add('escondido');
            document.getElementById('controles-jogo').classList.add('escondido');
            document.getElementById('jogo-velha').classList.add('escondido');
            document.getElementById('jogo-memoria').classList.add('escondido');
            document.getElementById('titulo-principal').innerText = "MENU DE JOGOS! 🎮";
            juegoSelecionado = ''; // Reseta o estado global
        }

        // Encaminha a requisição de reinício para a função do respectivo jogo ativo
        function reiniciarJogoAtual() {
            if (juegoSelecionado === 'velha') reiniciarVelha();
            else inicializarMemoria();
        }
        /* -------------------------------------------
            LÓGICA: JOGO DA MEMÓRIA
           ------------------------------------------- */
        // Base de dados contendo os 6 pares de emojis utilizados no jogo
        const emojisMemoria = ['🐶', '🐶', '🦁', '🦁', '🐸', '🐸', '🚀', '🚀', '🦄', '🦄', '🦕', '🦕'];
        let cartasViradas = []; // Armazena temporariamente até 2 referências de elementos de cartas clicadas
        let cartasBloqueadas = false; // Semáforo de controle para impedir cliques múltiplos rápidos enquanto analisa o par atual
        let paresEncontrados = 0; // Acumulador para verificar a condição de vitória absoluta

        // Reconstrói e reinicia o fluxo do tabuleiro da memória
        function inicializarMemoria() {
            paresEncontrados = 0;
            cartasViradas = [];
            cartasBloqueadas = false;
            document.getElementById('status').innerText = "Encontre os pares! 🔍";
            
            // Cria uma cópia do array original e aplica um algoritmo de embaralhamento pseudo-aleatório baseado no método Math.random()
            const emojisEmbaralhados = [...emojisMemoria].sort(() => Math.random() - 0.5);
            const container = document.getElementById('jogo-memoria');
            container.innerHTML = ''; // Limpa elementos HTML residuais de rodadas anteriores
            
            // Loop que itera sobre o array embaralhado injetando os botões diretamente no DOM da página
            emojisEmbaralhados.forEach((emoji, indice) => {
                const botaoCarta = document.createElement('button');
                botaoCarta.classList.add('quadrado', 'carta');
                
                // Utilização do mecanismo Dataset do HTML5 para guardar os dados do emoji ocultos na tag sem expô-los visualmente
                botaoCarta.dataset.emoji = emoji; 
                botaoCarta.dataset.indice = indice;
                botaoCarta.innerText = '❓'; // Texto padrão de exibição oculto
                
                // Atribuição de escopo de função anônima para gerenciar o clique individual da carta criada
                botaoCarta.onclick = function() { virarCarta(this); };
                container.appendChild(botaoCarta); // Insere o nó do botão criado dentro do container pai
            });
        }

        // Regra de negócio de virada e checagem de igualdade
        function virarCarta(cartaClicada) {
            // Cláusula de barreira: bloqueia a execução se o tabuleiro estiver travado ou a carta clicada já estiver aberta
            if (cartasBloqueadas || cartaClicada.classList.contains('virada')) return;

            cartaClicada.classList.add('virada'); // Adiciona classe visual que muda a cor de fundo para branco
            cartaClicada.innerText = cartaClicada.dataset.emoji; // Altera o texto visível exibindo o emoji real contido no Dataset
            cartasViradas.push(cartaClicada); // Adiciona a carta na fila de análise

            // Avalia o par de cartas quando a fila atinge o limite de 2 elementos preenchidos
            if (cartasViradas.length === 2) {
                cartasBloqueadas = true; // Bloqueia novos cliques na tela
                const [carta1, carta2] = cartasViradas; // Desestruturação do array de checagem

                // Cenário de Acerto: os dois conjuntos de dados contêm a mesma string de emoji?
                if (carta1.dataset.emoji === carta2.dataset.emoji) {
                    paresEncontrados++;
                    cartasViradas = []; // Esvazia o array para os próximos cliques
                    cartasBloqueadas = false; // Libera o tabuleiro de volta
                    
                    // Condição de Fim de Jogo: se o total de pares bate com metade do tamanho do array de dados (6 pares)
                    if (paresEncontrados === emojisMemoria.length / 2) {
                        document.getElementById('status').innerText = "Incrível! Você achou tudo! 🎉🥳";
                    }
                } else {
                    // Cenário de Erro: Utiliza uma função de callback assíncrona com temporizador de 1000 milissegundos (1 segundo)
                    // dando tempo para o usuário memorizar as posições erradas antes de desvirar as cartas
                    setTimeout(() => {
                        carta1.classList.remove('virada');
                        carta2.classList.remove('virada');
                        carta1.innerText = '❓'; // Oculta os emojis retornando o caractere padrão
                        carta2.innerText = '❓';
                        cartasViradas = []; // Reseta o cache de verificação
                        cartasBloqueadas = false; // Destrava os botões do tabuleiro para a continuidade do jogo
                    }, 1000);
                }
            }
        }
    </script>
</body>
</html>
