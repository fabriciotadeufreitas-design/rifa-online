<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rifa Online</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            color: white;
            margin-bottom: 40px;
            animation: slideDown 0.5s ease-out;
        }

        header h1 {
            font-size: 3em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
            flex-wrap: wrap;
            justify-content: center;
        }

        .tab-button {
            padding: 12px 30px;
            border: none;
            background: rgba(255,255,255,0.2);
            color: white;
            cursor: pointer;
            border-radius: 25px;
            font-size: 1em;
            transition: all 0.3s;
            font-weight: 600;
        }

        .tab-button.active {
            background: white;
            color: #667eea;
        }

        .tab-button:hover {
            background: rgba(255,255,255,0.3);
        }

        .tab-content {
            display: none;
            animation: fadeIn 0.5s ease-in;
        }

        .tab-content.active {
            display: block;
        }

        .card {
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.2);
            margin-bottom: 20px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #333;
            font-weight: 600;
        }

        input, textarea, select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1em;
            transition: border-color 0.3s;
        }

        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: #667eea;
        }

        textarea {
            resize: vertical;
            min-height: 100px;
        }

        button {
            padding: 12px 30px;
            border: none;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-radius: 8px;
            font-size: 1em;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
            font-weight: 600;
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(102, 126, 234, 0.4);
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }

        .raffle-card {
            background: white;
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            border-left: 5px solid #667eea;
            transition: transform 0.3s;
        }

        .raffle-card:hover {
            transform: translateY(-5px);
        }

        .raffle-title {
            font-size: 1.3em;
            font-weight: 700;
            color: #333;
            margin-bottom: 10px;
        }

        .raffle-info {
            color: #666;
            margin-bottom: 8px;
            font-size: 0.9em;
        }

        .raffle-price {
            font-size: 1.5em;
            color: #667eea;
            font-weight: 700;
            margin: 15px 0;
        }

        .progress-bar {
            background: #e0e0e0;
            border-radius: 10px;
            height: 8px;
            margin: 10px 0;
            overflow: hidden;
        }

        .progress-fill {
            background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
            height: 100%;
            transition: width 0.3s;
        }

        .winner-display {
            text-align: center;
            background: linear-gradient(135deg, #ffd700 0%, #ffed4e 100%);
            padding: 40px;
            border-radius: 15px;
            color: #333;
            font-size: 1.5em;
            font-weight: 700;
            margin: 20px 0;
            animation: pulse 0.5s;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        @media (max-width: 768px) {
            header h1 {
                font-size: 2em;
            }
            
            .grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🎉 Rifa Online</h1>
            <p>Gerencie e participe de rifas online</p>
        </header>

        <div class="tabs">
            <button class="tab-button active" onclick="showTab('criar')">Criar Rifa</button>
            <button class="tab-button" onclick="showTab('rifas')">Minhas Rifas</button>
            <button class="tab-button" onclick="showTab('participar')">Participar</button>
            <button class="tab-button" onclick="showTab('resultados')">Resultados</button>
        </div>

        <!-- Aba: Criar Rifa -->
        <div id="criar" class="tab-content active">
            <div class="card">
                <h2>Criar Nova Rifa</h2>
                <form id="formCriarRifa">
                    <div class="form-group">
                        <label>Nome da Rifa</label>
                        <input type="text" id="nomRifa" placeholder="Ex: iPhone 15 Pro" required>
                    </div>

                    <div class="form-group">
                        <label>Descrição</label>
                        <textarea id="descRifa" placeholder="Descreva o prêmio e detalhes da rifa" required></textarea>
                    </div>

                    <div class="form-group">
                        <label>Valor do Bilhete (R$)</label>
                        <input type="number" id="valorBilhete" placeholder="0.00" step="0.01" required>
                    </div>

                    <div class="form-group">
                        <label>Quantidade de Bilhetes</label>
                        <input type="number" id="qtdBilhetes" placeholder="100" min="1" required>
                    </div>

                    <div class="form-group">
                        <label>Data do Sorteio</label>
                        <input type="datetime-local" id="dataSorteio" required>
                    </div>

                    <button type="submit">Criar Rifa</button>
                </form>
                <div id="mensagem"></div>
            </div>
        </div>

        <!-- Aba: Minhas Rifas -->
        <div id="rifas" class="tab-content">
            <div id="minhasRifas" class="grid"></div>
        </div>

        <!-- Aba: Participar -->
        <div id="participar" class="tab-content">
            <div class="card">
                <h2>Rifas Disponíveis</h2>
                <div id="rifasDisponiveis" class="grid"></div>
            </div>
        </div>

        <!-- Aba: Resultados -->
        <div id="resultados" class="tab-content">
            <div id="resultadosSorteios" class="grid"></div>
        </div>
    </div>

    <script>
        const STORAGE_KEY = 'rifas_data';

        class RifaManager {
            constructor() {
                this.rifas = this.loadData();
            }

            loadData() {
                const data = localStorage.getItem(STORAGE_KEY);
                return data ? JSON.parse(data) : [];
            }

            saveData() {
                localStorage.setItem(STORAGE_KEY, JSON.stringify(this.rifas));
            }

            criar(rifa) {
                const novaRifa = {
                    id: Date.now(),
                    ...rifa,
                    bilhetes: [],
                    criador: 'Usuario ' + Math.floor(Math.random() * 1000),
                    dataCriacao: new Date().toISOString(),
                    sorteio: null
                };

                for (let i = 1; i <= rifa.qtdBilhetes; i++) {
                    novaRifa.bilhetes.push({
                        numero: i,
                        comprador: null,
                        email: null
                    });
                }

                this.rifas.push(novaRifa);
                this.saveData();
                return novaRifa;
            }

            obter(id) {
                return this.rifas.find(r => r.id == id);
            }

            obterTodas() {
                return this.rifas;
            }

            comprarBilhete(rifaId, numeroBilhete, nomeComprador, emailComprador) {
                const rifa = this.obter(rifaId);
                if (!rifa) return null;

                const bilhete = rifa.bilhetes.find(b => b.numero == numeroBilhete);
                if (!bilhete || bilhete.comprador) return null;

                bilhete.comprador = nomeComprador;
                bilhete.email = emailComprador;
                this.saveData();
                return bilhete;
            }

            sortear(rifaId) {
                const rifa = this.obter(rifaId);
                if (!rifa) return null;

                const bilhetesVendidos = rifa.bilhetes.filter(b => b.comprador);
                if (bilhetesVendidos.length === 0) return null;

                const bilheteSorteado = bilhetesVendidos[Math.floor(Math.random() * bilhetesVendidos.length)];
                rifa.sorteio = {
                    data: new Date().toISOString(),
                    bilhete: bilheteSorteado.numero,
                    vencedor: bilheteSorteado.comprador,
                    email: bilheteSorteado.email
                };

                this.saveData();
                return rifa.sorteio;
            }

            obterProgresso(rifaId) {
                const rifa = this.obter(rifaId);
                if (!rifa) return 0;
                const vendidos = rifa.bilhetes.filter(b => b.comprador).length;
                return Math.round((vendidos / rifa.qtdBilhetes) * 100);
            }
        }

        const manager = new RifaManager();

        function showTab(tabName) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
            document.querySelectorAll('.tab-button').forEach(el => el.classList.remove('active'));
            
            document.getElementById(tabName).classList.add('active');
            event.target.classList.add('active');

            if (tabName === 'rifas') loadMinhasRifas();
            if (tabName === 'participar') loadRifasDisponiveis();
            if (tabName === 'resultados') loadResultados();
        }

        document.getElementById('formCriarRifa').addEventListener('submit', function(e) {
            e.preventDefault();

            const rifa = {
                nome: document.getElementById('nomRifa').value,
                descricao: document.getElementById('descRifa').value,
                valorBilhete: parseFloat(document.getElementById('valorBilhete').value),
                qtdBilhetes: parseInt(document.getElementById('qtdBilhetes').value),
                dataSorteio: document.getElementById('dataSorteio').value
            };

            try {
                manager.criar(rifa);
                const msg = document.getElementById('mensagem');
                msg.style.background = '#4caf50';
                msg.style.color = 'white';
                msg.style.padding = '15px';
                msg.style.borderRadius = '8px';
                msg.innerHTML = '✓ Rifa criada com sucesso!';
                this.reset();
                setTimeout(() => msg.innerHTML = '', 3000);
            } catch (error) {
                const msg = document.getElementById('mensagem');
                msg.style.background = '#f44336';
                msg.style.color = 'white';
                msg.style.padding = '15px';
                msg.style.borderRadius = '8px';
                msg.innerHTML = '✗ Erro ao criar rifa';
            }
        });

        function loadMinhasRifas() {
            const container = document.getElementById('minhasRifas');
            const rifas = manager.obterTodas();
            
            if (rifas.length === 0) {
                container.innerHTML = '<p style="grid-column: 1/-1; text-align: center; color: white;">Nenhuma rifa criada ainda</p>';
                return;
            }

            container.innerHTML = rifas.map(rifa => `
                <div class="raffle-card">
                    <div class="raffle-title">${rifa.nome}</div>
                    <div class="raffle-info">Criador: ${rifa.criador}</div>
                    <div class="raffle-price">R$ ${rifa.valorBilhete.toFixed(2)}</div>
                    <div class="raffle-info">Bilhetes vendidos: ${rifa.bilhetes.filter(b => b.comprador).length}/${rifa.qtdBilhetes}</div>
                    <div class="progress-bar">
                        <div class="progress-fill" style="width: ${manager.obterProgresso(rifa.id)}%"></div>
                    </div>
                    <button onclick="realizarSorteio(${rifa.id})" style="width: 100%; margin-top: 10px;">Fazer Sorteio</button>
                </div>
            `).join('');
        }

        function loadRifasDisponiveis() {
            const container = document.getElementById('rifasDisponiveis');
            const rifas = manager.obterTodas().filter(r => !r.sorteio);
            
            if (rifas.length === 0) {
                container.innerHTML = '<p style="grid-column: 1/-1; text-align: center; color: white;">Nenhuma rifa disponível</p>';
                return;
            }

            container.innerHTML = rifas.map(rifa => {
                const bilhetesDisponiveis = rifa.bilhetes.filter(b => !b.comprador).length;
                return `
                    <div class="raffle-card">
                        <div class="raffle-title">${rifa.nome}</div>
                        <div class="raffle-info">${rifa.descricao}</div>
                        <div class="raffle-price">R$ ${rifa.valorBilhete.toFixed(2)}</div>
                        <div class="raffle-info">Bilhetes disponíveis: ${bilhetesDisponiveis}/${rifa.qtdBilhetes}</div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: ${manager.obterProgresso(rifa.id)}%"></div>
                        </div>
                        <button onclick="abrirCompra(${rifa.id})" style="width: 100%; margin-top: 10px;">Comprar Bilhete</button>
                    </div>
                `;
            }).join('');
        }

        function abrirCompra(rifaId) {
            const rifa = manager.obter(rifaId);
            const bilhetesDisponiveis = rifa.bilhetes.filter(b => !b.comprador);
            
            let opcoesBilhetes = bilhetesDisponiveis.map(b => 
                `<option value="${b.numero}">Bilhete #${b.numero}</option>`
            ).join('');

            const formulario = `
                <div style="position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); background: white; padding: 30px; border-radius: 12px; box-shadow: 0 20px 60px rgba(0,0,0,0.3); z-index: 1000; max-width: 500px; width: 90%;">
                    <h3>Comprar Bilhete - ${rifa.nome}</h3>
                    <div class="form-group">
                        <label>Selecione o Bilhete</label>
                        <select id="selectBilhete">
                            ${opcoesBilhetes}
                        </select>
                    </div>
                    <div class="form-group">
                        <label>Nome</label>
                        <input type="text" id="inputNome" placeholder="Seu nome" required>
                    </div>
                    <div class="form-group">
                        <label>Email</label>
                        <input type="email" id="inputEmail" placeholder="seu@email.com" required>
                    </div>
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
                        <button onclick="confirmarCompra(${rifaId})">Comprar</button>
                        <button onclick="fecharModal()" style="background: #999;">Cancelar</button>
                    </div>
                </div>
                <div id="modal-backdrop" style="position: fixed; top: 0; left: 0; right: 0; bottom: 0; background: rgba(0,0,0,0.5); z-index: 999;" onclick="fecharModal()"></div>
            `;

            document.body.insertAdjacentHTML('beforeend', formulario);
        }

        function confirmarCompra(rifaId) {
            const bilhete = document.getElementById('selectBilhete').value;
            const nome = document.getElementById('inputNome').value;
            const email = document.getElementById('inputEmail').value;

            if (!nome || !email) {
                alert('Preencha todos os campos');
                return;
            }

            manager.comprarBilhete(rifaId, bilhete, nome, email);
            fecharModal();
            loadRifasDisponiveis();
            alert('✓ Bilhete comprado com sucesso!');
        }

        function fecharModal() {
            const backdrop = document.getElementById('modal-backdrop');
            if (backdrop) {
                backdrop.remove();
                backdrop.parentElement?.remove();
            }
        }

        function realizarSorteio(rifaId) {
            const rifa = manager.obter(rifaId);
            if (rifa.bilhetes.filter(b => b.comprador).length === 0) {
                alert('Nenhum bilhete foi vendido ainda!');
                return;
            }

            if (confirm('Tem certeza que deseja realizar o sorteio?\nIsso não pode ser desfeito!')) {
                const resultado = manager.sortear(rifaId);
                alert(`🎉 VENCEDOR!\n\nBilhete: #${resultado.bilhete}\nVencedor: ${resultado.vencedor}\nEmail: ${resultado.email}`);
                loadMinhasRifas();
                loadRifasDisponiveis();
            }
        }

        function loadResultados() {
            const container = document.getElementById('resultadosSorteios');
            const rifas = manager.obterTodas().filter(r => r.sorteio);
            
            if (rifas.length === 0) {
                container.innerHTML = '<p style="grid-column: 1/-1; text-align: center; color: white;">Nenhum sorteio realizado ainda</p>';
                return;
            }

            container.innerHTML = rifas.map(rifa => `
                <div class="raffle-card">
                    <div class="raffle-title">${rifa.nome}</div>
                    <div class="winner-display">
                        🏆 ${rifa.sorteio.vencedor}
                    </div>
                    <div class="raffle-info"><strong>Bilhete Sorteado:</strong> #${rifa.sorteio.bilhete}</div>
                    <div class="raffle-info"><strong>Email:</strong> ${rifa.sorteio.email}</div>
                    <div class="raffle-info"><strong>Data:</strong> ${new Date(rifa.sorteio.data).toLocaleString('pt-BR')}</div>
                </div>
            `).join('');
        }
    </script>
</body>
</html>
