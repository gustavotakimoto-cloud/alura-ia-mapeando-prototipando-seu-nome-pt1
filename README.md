<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minha Rotina Semanal 3D</title>
    <style>
        /* Reseta margens e define a fonte */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        /* Fundo com degradê de tons de ROXO animado */
        body {
            background: linear-gradient(135deg, #12001c, #3a0066, #7a00cc, #240046);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
            color: #fff;
            min-height: 100vh;
            overflow-x: hidden;
            perspective: 1000px;
        }

        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        /* --- FORMAS 3D VOADORAS NO FUNDO (ROXAS) --- */
        .shape {
            position: fixed;
            z-index: -1;
            opacity: 0.7;
            animation: fly3D linear infinite;
        }

        .sphere {
            border-radius: 50%;
            background: radial-gradient(circle at 30% 30%, #d494ff, transparent 60%);
            box-shadow: inset -10px -10px 20px rgba(0,0,0,0.5), 10px 10px 30px rgba(0,0,0,0.5);
        }

        .cube {
            background: rgba(153, 51, 255, 0.15);
            backdrop-filter: blur(4px);
            border: 1px solid rgba(204, 153, 255, 0.4);
            box-shadow: inset 0 0 20px rgba(204, 153, 255, 0.2), 15px 15px 30px rgba(0,0,0,0.6);
        }

        .pyramid {
            width: 0; 
            height: 0; 
            border-left: 50px solid transparent;
            border-right: 50px solid transparent;
            border-bottom: 80px solid rgba(170, 0, 255, 0.5);
            filter: drop-shadow(10px 10px 15px rgba(0,0,0,0.5));
        }

        .shape1 { width: 120px; height: 120px; left: 10%; bottom: -150px; animation-duration: 20s; }
        .shape2 { width: 90px; height: 90px; left: 40%; bottom: -100px; animation-duration: 15s; animation-delay: 2s; }
        .shape3 { left: 70%; bottom: -100px; animation-duration: 18s; animation-delay: 5s; }
        .shape4 { width: 150px; height: 150px; left: 85%; bottom: -200px; animation-duration: 25s; animation-delay: 1s; }
        .shape5 { width: 60px; height: 60px; left: 25%; bottom: -80px; animation-duration: 12s; animation-delay: 4s; }

        @keyframes fly3D {
            0% { transform: translateY(0) rotateX(0deg) rotateY(0deg) rotateZ(0deg); }
            100% { transform: translateY(-120vh) rotateX(360deg) rotateY(360deg) rotateZ(180deg); }
        }

        /* --- CABEÇALHO --- */
        header {
            text-align: center;
            padding: 3rem 1rem 1rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.8);
        }

        header h1 {
            font-size: 3rem;
            margin-bottom: 0.5rem;
            color: #e0b3ff;
            letter-spacing: 2px;
        }

        /* --- GRID E CARDS 3D --- */
        .grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
            padding: 2rem 5%;
            max-width: 1200px;
            margin: 0 auto;
        }

        .card {
            background: rgba(40, 0, 80, 0.3);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(180, 100, 255, 0.3);
            border-radius: 20px;
            padding: 2rem;
            text-align: center;
            cursor: pointer;
            box-shadow: 0 15px 35px rgba(0,0,0,0.4), inset 0 0 15px rgba(180,100,255,0.1);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            transform-style: preserve-3d;
        }

        .card:hover {
            transform: translateY(-15px) scale(1.05) rotateX(10deg) rotateY(-5deg);
            box-shadow: 0 25px 45px rgba(0,0,0,0.6), inset 0 0 20px rgba(180,100,255,0.3);
            border-color: rgba(200, 150, 255, 0.7);
        }

        .card-icon {
            font-size: 3rem;
            margin-bottom: 1rem;
            transform: translateZ(30px);
        }

        .card h2 {
            font-size: 1.8rem;
            margin-bottom: 1rem;
            color: #d494ff;
            transform: translateZ(20px);
        }

        .card p {
            font-size: 1rem;
            color: #eeddff;
            transform: translateZ(10px);
            line-height: 1.4;
        }

        /* --- MODAL --- */
        .modal {
            display: none;
            position: fixed;
            z-index: 100;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(6px);
            justify-content: center;
            align-items: center;
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .modal.show {
            opacity: 1;
        }

        .modal-content {
            background: linear-gradient(145deg, rgba(50,0,100,0.95), rgba(20,0,50,0.95));
            border: 2px solid rgba(180, 100, 255, 0.5);
            border-radius: 20px;
            padding: 3rem;
            width: 90%;
            max-width: 500px;
            text-align: left;
            box-shadow: 0 30px 60px rgba(0,0,0,0.9);
            transform: scale(0.7) translateY(50px);
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .modal.show .modal-content {
            transform: scale(1) translateY(0);
        }

        .modal-content h2 {
            margin-bottom: 1.5rem;
            color: #d494ff;
            text-transform: uppercase;
            letter-spacing: 1px;
            text-align: center;
            border-bottom: 1px solid rgba(180, 100, 255, 0.3);
            padding-bottom: 10px;
        }

        .modal-content ul {
            list-style: none;
            padding: 0;
        }

        .modal-content ul li {
            font-size: 1.1rem;
            line-height: 1.6;
            color: #f3e6ff;
            margin-bottom: 10px;
            padding-left: 20px;
            position: relative;
        }

        .modal-content ul li::before {
            content: "➔";
            position: absolute;
            left: 0;
            color: #a855f7;
        }

        /* Botão de Fechar */
        .close-btn {
            position: absolute;
            top: 15px;
            right: 25px;
            color: #fff;
            font-size: 2.5rem;
            font-weight: bold;
            cursor: pointer;
            transition: color 0.3s;
        }

        .close-btn:hover {
            color: #ff66ff;
        }
    </style>
</head>
<body>
    <!-- Objetos 3D voadores roxos no fundo -->
    <div class="shape sphere shape1"></div>
    <div class="shape cube shape2"></div>
    <div class="shape pyramid shape3"></div>
    <div class="shape sphere shape4"></div>
    <div class="shape cube shape5"></div>

    <header>
        <h1>Minha Rotina Semanal</h1>
        <p>Clique nos dias para ver os detalhes</p>
    </header>

    <main class="grid-container">
        <!-- Cards de Segunda a Domingo -->
        <div class="card" onclick="openModal('modal-segunda')">
            <div class="card-icon">📅</div>
            <h2>Segunda-feira</h2>
            <p>Escola, limpeza da casa e PC.</p>
        </div>

        <div class="card" onclick="openModal('modal-terca')">
            <div class="card-icon">🏐</div>
            <h2>Terça-feira</h2>
            <p>Escola, limpeza, treino e PC.</p>
        </div>

        <div class="card" onclick="openModal('modal-quarta')">
            <div class="card-icon">📖</div>
            <h2>Quarta-feira</h2>
            <p>Escola, leitura e PC.</p>
        </div>

        <div class="card" onclick="openModal('modal-quinta')">
            <div class="card-icon">🏐</div>
            <h2>Quinta-feira</h2>
            <p>Escola, treino de vôlei e PC.</p>
        </div>

        <div class="card" onclick="openModal('modal-sexta')">
            <div class="card-icon">🍕</div>
            <h2>Sexta-feira</h2>
            <p>Escola, sair/lazer e PC.</p>
        </div>

        <div class="card" onclick="openModal('modal-sabado')">
            <div class="card-icon">🏠</div>
            <h2>Sábado</h2>
            <p>Ficar em casa e PC.</p>
        </div>

        <div class="card" onclick="openModal('modal-domingo')">
            <div class="card-icon">🎮</div>
            <h2>Domingo</h2>
            <p>Ficar em casa e relaxar no PC.</p>
        </div>
    </main>

    <!-- Modais com os detalhes da rotina -->
    <div id="modal-segunda" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal('modal-segunda')">&times;</span>
            <h2>Rotina de Segunda</h2>
            <ul>
                <li>Acordar e escovar os dentes</li>
                <li>Ir para a escola</li>
                <li>Chegar em casa e limpar tudo</li>
                <li>Jogar no PC</li>
            </ul>
        </div>
    </div>

    <div id="modal-terca" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal('modal-terca')">&times;</span>
            <h2>Rotina de Terça</h2>
            <ul>
                <li>Acordar e escovar os dentes</li>
                <li>Ir para a escola</li>
                <li>Chegar em casa e limpar tudo</li>
                <li>Treino de Vôlei (das 7:30 às 10:00)</li>
                <li>Jogar no PC</li>
            </ul>
        </div>
    </div>

    <div id="modal-quarta" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal('modal-quarta')">&times;</span>
            <h2>Rotina de Quarta</h2>
            <ul>
                <li>Acordar e escovar os dentes</li>
                <li>Ir para a escola</li>
                <li>Ler livros em casa</li>
                <li>Jogar no PC</li>
            </ul>
        </div>
    </div>

    <div id="modal-quinta" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal('modal-quinta')">&times;</span>
            <h2>Rotina de Quinta</h2>
            <ul>
                <li>Acordar e escovar os dentes</li>
                <li>Ir para a escola</li>
                <li>Treino de Vôlei</li>
                <li>Jogar no PC</li>
            </ul>
        </div>
    </div>

    <div id="modal-sexta" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal('modal-sexta')">&times;</span>
            <h2>Rotina de Sexta</h2>
            <ul>
                <li>Acordar e escovar os dentes</li>
                <li>Ir para a escola</li>
                <li>Sair para comer ou lazer</li>
                <li>Jogar no PC</li>
            </ul>
        </div>
    </div>

    <div id="modal-sabado" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal('modal-sabado')">&times;</span>
            <h2>Rotina de Sábado</h2>
            <ul>
                <li>Dia livre!</li>
                <li>Ficar em casa relaxando</li>
                <li>Jogar no PC (o dia todo se quiser!)</li>
            </ul>
        </div>
    </div>

    <div id="modal-domingo" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal('modal-domingo')">&times;</span>
            <h2>Rotina de Domingo</h2>
            <ul>
                <li>Dia de descanso!</li>
                <li>Ficar em casa</li>
                <li>Jogar no PC e se preparar para a semana</li>
            </ul>
        </div>
    </div>

    <!-- JAVASCRIPT -->
    <script>
        // Função para abrir o modal
        function openModal(id) {
            const modal = document.getElementById(id);
            modal.style.display = 'flex';
            setTimeout(() => {
                modal.classList.add('show');
            }, 10);
        }

        // Função para fechar o modal
        function closeModal(id) {
            const modal = document.getElementById(id);
            modal.classList.remove('show');
            setTimeout(() => {
                modal.style.display = 'none';
            }, 300);
        }

        // Fechar modal ao clicar fora da caixa de conteúdo
        window.onclick = function(event) {
            if (event.target.classList.contains('modal')) {
                event.target.classList.remove('show');
                setTimeout(() => {
                    event.target.style.display = 'none';
                }, 300);
            }
        }
    </script>
</body>
</html>
