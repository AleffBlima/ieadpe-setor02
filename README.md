<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema IEADPE - Setor 02</title>
    <style>
        body { font-family: sans-serif; padding: 20px; background: #f0f2f5; }
        .card { background: white; padding: 20px; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.1); }
        input { width: 100%; padding: 10px; margin: 10px 0; border: 1px solid #ccc; border-radius: 4px; box-sizing: border-box; }
        button { width: 100%; padding: 10px; background: #007bff; color: white; border: none; border-radius: 4px; cursor: pointer; font-size: 16px; }
        button:hover { background: #0056b3; }
    </style>
</head>
<body>

    <div class="card">
        <h2>Cadastro IEADPE - Setor 02</h2>
        <form id="meuForm">
            <input type="text" name="nome" placeholder="Nome Completo" required>
            <input type="text" name="setor" placeholder="Setor (Ex: 02)" required>
            <input type="tel" name="telefone" placeholder="Telefone">
            <button type="submit" id="btnSalvar">Salvar no Banco</button>
        </form>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getFirestore, collection, addDoc } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

        const firebaseConfig = {
            apiKey: "AIzaSyDFxv6iVXzD5bROLAHinDpocUHt6o5VQ6g",
            authDomain: "ieadpe-setor02.firebaseapp.com",
            projectId: "ieadpe-setor02",
            storageBucket: "ieadpe-setor02.firebasestorage.app",
            messagingSenderId: "1092870702547",
            appId: "1:1092870702547:web:7ac72575ea28d2095b1b26"
        };

        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);

        document.getElementById('meuForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            const btn = document.getElementById('btnSalvar');
            btn.innerText = "Enviando...";
            btn.disabled = true;

            const formData = new FormData(e.target);
            const dados = Object.fromEntries(formData.entries());
            dados.dataEnvio = new Date().toLocaleString();

            try {
                await addDoc(collection(db, "registros"), dados);
                alert("Sucesso! Os dados foram salvos no Firebase.");
                e.target.reset();
            } catch (error) {
                alert("Erro ao salvar: " + error.message);
            } finally {
                btn.innerText = "Salvar no Banco";
                btn.disabled = false;
            }
        });
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestão IEADPE - Setor 02</title>
    <style>
        :root { --primary: #1a237e; --secondary: #0d47a1; }
        body { font-family: 'Segoe UI', sans-serif; margin: 0; background: #f4f7f6; }
        header { background: var(--primary); color: white; padding: 15px; text-align: center; font-weight: bold; }
        .menu-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; padding: 15px; }
        .btn-menu { background: white; border: 1px solid #ddd; padding: 20px; border-radius: 10px; text-align: center; font-weight: bold; color: var(--primary); box-shadow: 0 2px 5px rgba(0,0,0,0.1); text-decoration: none;}
        .container { padding: 15px; }
        .form-group { background: white; padding: 15px; border-radius: 8px; margin-bottom: 10px; }
        input, select { width: 100%; padding: 12px; margin: 8px 0; border: 1px solid #ccc; border-radius: 5px; }
        button { width: 100%; padding: 15px; background: var(--secondary); color: white; border: none; border-radius: 5px; font-weight: bold; cursor: pointer; }
    </style>
</head>
<body>

<header>SISTEMA DE GESTÃO - SETOR 02</header>

<div class="menu-grid">
    <div class="btn-menu">📦<br>Estoque</div>
    <div class="btn-menu">📑<br>Notas Fiscais</div>
    <div class="btn-menu">🍷<br>Distribuição Vinho</div>
    <div class="btn-menu">⛪<br>Congregações</div>
</div>

<div class="container">
    <div class="form-group">
        <h3>Entrada de Material (Nota Fiscal)</h3>
        <input type="text" id="item" placeholder="Nome do Produto (Ex: Água Sanitária)">
        <input type="number" id="qtd" placeholder="Quantidade em Nota">
        <select id="categoria">
            <option value="limpeza">Material de Limpeza</option>
            <option value="vinho">Suco de Uva / Vinho</option>
        </select>
        <button onclick="registrarEntrada()">Dar Entrada no Estoque</button>
    </div>
</div>

<script type="module">
    // Aqui entrará a lógica que você já tem do Firebase
    // para somar no estoque e subtrair na distribuição.
    window.registrarEntrada = function() {
        alert("Integrando com o banco para atualizar o estoque...");
    }
</script>

</body>
</html>
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SGE - Setor 02 (IEADPE)</title>
    <style>
        :root { --primary: #003366; --accent: #ffd700; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; margin: 0; background: #f0f2f5; padding-bottom: 50px; }
        .header { background: var(--primary); color: white; padding: 20px; text-align: center; border-bottom: 4px solid var(--accent); }
        .nav-tabs { display: flex; overflow-x: auto; background: #fff; border-bottom: 1px solid #ddd; position: sticky; top: 0; z-index: 100; }
        .tab { padding: 15px 20px; cursor: pointer; white-space: nowrap; font-weight: bold; color: #666; }
        .tab.active { color: var(--primary); border-bottom: 3px solid var(--primary); }
        .container { padding: 15px; }
        .card { background: white; padding: 20px; border-radius: 12px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); margin-bottom: 20px; }
        input, select, textarea { width: 100%; padding: 12px; margin: 8px 0; border: 1px solid #ccc; border-radius: 8px; box-sizing: border-box; font-size: 16px; }
        .btn { width: 100%; padding: 15px; border: none; border-radius: 8px; font-weight: bold; font-size: 16px; cursor: pointer; transition: 0.3s; }
        .btn-primary { background: var(--primary); color: white; }
        .btn-samuel { background: #e91e63; color: white; }
        .info-box { display: flex; justify-content: space-between; background: #e3f2fd; padding: 10px; border-radius: 8px; margin-bottom: 10px; font-weight: bold; color: #0d47a1; }
    </style>
</head>
<body>

<div class="header">
    <h1>SGE - SETOR 02</h1>
    <small>Sistema de Gestão Estratégica</small>
</div>

<div class="nav-tabs">
    <div class="tab active" onclick="showTab('estoque')">📦 ESTOQUE</div>
    <div class="tab" onclick="showTab('distribuicao')">🍷 DISTRIBUIÇÃO</div>
    <div class="tab" onclick="showTab('samuel')">💖 PROJETO SAMUEL</div>
    <div class="tab" onclick="showTab('relatorios')">📊 RELATÓRIOS</div>
</div>

<div class="container" id="content">
    </div>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
    import { getFirestore, collection, addDoc, query, where, getDocs, doc, updateDoc, increment } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

    const firebaseConfig = {
        apiKey: "AIzaSyDFxv6iVXzD5bROLAHinDpocUHt6o5VQ6g",
        authDomain: "ieadpe-setor02.firebaseapp.com",
        projectId: "ieadpe-setor02",
        storageBucket: "ieadpe-setor02.firebasestorage.app",
        messagingSenderId: "1092870702547",
        appId: "1:1092870702547:web:7ac72575ea28d2095b1b26"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    // FUNÇÃO PARA MUDAR DE TELA
    window.showTab = (tab) => {
        const container = document.getElementById('content');
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        // Adicionar logica de UI aqui
        
        if(tab === 'estoque') {
            container.innerHTML = `
                <div class="card">
                    <h3>📥 Entrada (Nota Fiscal)</h3>
                    <input type="text" id="nf_numero" placeholder="Nº da Nota Fiscal">
                    <select id="item_tipo">
                        <option value="Limpeza">Material de Limpeza</option>
                        <option value="Vinho">Vinho / Suco de Uva</option>
                    </select>
                    <input type="text" id="item_nome" placeholder="Nome do Produto">
                    <input type="number" id="item_qtd" placeholder="Quantidade">
                    <button class="btn btn-primary" onclick="window.registrarEntrada()">Confirmar Entrada</button>
                </div>
            `;
        }

        if(tab === 'samuel') {
            container.innerHTML = `
                <div class="card" style="border-left: 5px solid #e91e63;">
                    <h3>💖 Doação - Projeto Samuel</h3>
                    <input type="text" id="doador" placeholder="Nome do Doador (Opcional)">
                    <input type="text" id="item_doado" placeholder="O que foi doado?">
                    <input type="number" id="valor_estimado" placeholder="Valor ou Qtd">
                    <button class="btn btn-samuel" onclick="window.registrarSamuel()">Registrar Doação</button>
                </div>
            `;
        }
    }

    // REGISTRAR NO BANCO
    window.registrarEntrada = async () => {
        const dados = {
            nf: document.getElementById('nf_numero').value,
            tipo: document.getElementById('item_tipo').value,
            item: document.getElementById('item_nome').value,
            qtd: Number(document.getElementById('item_qtd').value),
            data: new Date()
        };
        
        try {
            await addDoc(collection(db, "entradas_estoque"), dados);
            alert("Entrada registrada e estoque atualizado!");
            showTab('estoque');
        } catch (e) { alert("Erro: " + e.message); }
    }

    // Iniciar na primeira aba
    showTab('estoque');

</script>
</body>
</html>
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SGE Setor 02 - Master</title>
    <style>
        :root { --primary: #002855; --secondary: #00509d; --accent: #ffc107; --danger: #d90429; --samuel: #8338ec; }
        body { font-family: 'Segoe UI', sans-serif; margin: 0; background: #f8f9fa; color: #333; }
        .header { background: var(--primary); color: white; padding: 15px; text-align: center; border-bottom: 5px solid var(--accent); }
        .nav-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; padding: 10px; background: #eee; }
        .nav-item { background: white; padding: 10px; text-align: center; border-radius: 8px; font-size: 12px; font-weight: bold; cursor: pointer; border: 1px solid #ddd; }
        .active { background: var(--accent); color: #000; }
        .container { padding: 15px; }
        .card { background: white; padding: 15px; border-radius: 12px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); margin-bottom: 15px; }
        h3 { margin-top: 0; color: var(--primary); border-bottom: 2px solid #eee; padding-bottom: 5px; }
        input, select, textarea { width: 100%; padding: 12px; margin: 8px 0; border: 1px solid #ccc; border-radius: 8px; font-size: 16px; }
        .btn { width: 100%; padding: 15px; border: none; border-radius: 8px; font-weight: bold; color: white; margin-top: 10px; }
        .btn-save { background: #28a745; }
        .btn-order { background: var(--secondary); }
    </style>
</head>
<body>

<div class="header">
    <strong>SISTEMA SETOR 02 - IEADPE</strong><br>Gestão Integrada
</div>

<div class="nav-grid">
    <div class="nav-item" onclick="mudarAba('estoque')">📦 Limpeza/Vinho</div>
    <div class="nav-item" onclick="mudarAba('eletronicos')">⚡ Eletrônicos</div>
    <div class="nav-item" onclick="mudarAba('compras')">🏗️ Mat. Construção</div>
    <div class="nav-item" onclick="mudarAba('samuel')">💜 Proj. Samuel</div>
    <div class="nav-item" onclick="mudarAba('pedidos')">📝 Pedidos/Falta</div>
</div>

<div id="app" class="container"></div>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
    import { getFirestore, collection, addDoc, serverTimestamp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

    const firebaseConfig = {
        apiKey: "AIzaSyDFxv6iVXzD5bROLAHinDpocUHt6o5VQ6g",
        authDomain: "ieadpe-setor02.firebaseapp.com",
        projectId: "ieadpe-setor02",
        storageBucket: "ieadpe-setor02.firebasestorage.app",
        messagingSenderId: "1092870702547",
        appId: "1:1092870702547:web:7ac72575ea28d2095b1b26"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    window.mudarAba = (aba) => {
        const display = document.getElementById('app');
        let html = '';

        if(aba === 'estoque') {
            html = `
                <div class="card">
                    <h3>📦 Entrada de Consumo</h3>
                    <select id="cat_consumo">
                        <option value="Limpeza">Material de Limpeza</option>
                        <option value="Vinho">Vinho / Suco de Uva</option>
                    </select>
                    <input type="text" id="prod_nome" placeholder="Nome do Produto">
                    <input type="number" id="prod_qtd" placeholder="Quantidade">
                    <button class="btn btn-save" onclick="salvar('estoque_consumo')">Registrar Entrada</button>
                </div>`;
        } 
        
        if(aba === 'eletronicos') {
            html = `
                <div class="card">
                    <h3>⚡ Equipamentos Eletrônicos</h3>
                    <select id="eletro_mov">
                        <option value="Entrada">Entrada (Compra/Doação)</option>
                        <option value="Saída">Saída (Distribuição)</option>
                    </select>
                    <input type="text" id="eletro_nome" placeholder="Equipamento (Ex: Microfone)">
                    <input type="text" id="eletro_destino" placeholder="Destino (Congregação/Área)">
                    <button class="btn btn-save" onclick="salvar('eletronicos')">Registrar Movimentação</button>
                </div>`;
        }

        if(aba === 'compras') {
            html = `
                <div class="card">
                    <h3>🏗️ Compras Material de Construção</h3>
                    <select id="armazem">
                        <option value="Asa Branca">Asa Branca</option>
                        <option value="Coral">Coral</option>
                        <option value="Rogério">Rogério</option>
                        <option value="Márcio">Márcio</option>
                        <option value="Outros">Outros</option>
                    </select>
                    <input type="text" id="mat_obra" placeholder="Material Comprado">
                    <input type="number" id="valor_compra" placeholder="Valor R$">
                    <button class="btn btn-save" onclick="salvar('compras_construcao')">Lançar Nota</button>
                </div>`;
        }

        if(aba === 'samuel') {
            html = `
                <div class="card">
                    <h3>💜 Arrecadação Projeto Samuel</h3>
                    <input type="number" id="area_num" placeholder="Área (1-12)">
                    <input type="text" id="cong_nome" placeholder="Congregação">
                    <input type="number" id="valor_samuel" placeholder="Valor Arrecadado">
                    <button class="btn btn-save" style="background:var(--samuel)" onclick="salvar('projeto_samuel')">Confirmar Recebimento</button>
                </div>`;
        }

        if(aba === 'pedidos') {
            html = `
                <div class="card">
                    <h3>📝 Lista de Pedidos (Falta)</h3>
                    <select id="pedido_tipo">
                        <option value="Limpeza">Material de Limpeza</option>
                        <option value="Vinho">Vinho</option>
                        <option value="Eletrônica">Peças de Eletrônica</option>
                    </select>
                    <textarea id="pedido_desc" placeholder="Descreva o que precisa ser comprado..."></textarea>
                    <button class="btn btn-order" onclick="salvar('pedidos_compra')">Adicionar à Lista de Pedidos</button>
                </div>`;
        }

        display.innerHTML = html;
    };

    window.salvar = async (colecao) => {
        let payload = { data: serverTimestamp() };
        
        // Lógica para capturar campos de acordo com a aba
        if(colecao === 'estoque_consumo') {
            payload.categoria = document.getElementById('cat_consumo').value;
            payload.item = document.getElementById('prod_nome').value;
            payload.qtd = document.getElementById('prod_qtd').value;
        } else if(colecao === 'compras_construcao') {
            payload.armazem = document.getElementById('armazem').value;
            payload.item = document.getElementById('mat_obra').value;
            payload.valor = document.getElementById('valor_compra').value;
        } else if(colecao === 'projeto_samuel') {
            payload.area = document.getElementById('area_num').value;
            payload.congregação = document.getElementById('cong_nome').value;
            payload.valor = document.getElementById('valor_samuel').value;
        } else if(colecao === 'eletronicos') {
            payload.movimentacao = document.getElementById('eletro_mov').value;
            payload.item = document.getElementById('eletro_nome').value;
            payload.destino = document.getElementById('eletro_destino').value;
        } else if(colecao === 'pedidos_compra') {
            payload.tipo = document.getElementById('pedido_tipo').value;
            payload.descricao = document.getElementById('pedido_desc').value;
        }

        try {
            await addDoc(collection(db, colecao), payload);
            alert("Registrado com sucesso!");
            mudarAba(colecao === 'pedidos_compra' ? 'pedidos' : 'estoque');
        } catch (e) { alert("Erro: " + e.message); }
    };

    mudarAba('estoque');
</script>
</body>
</html>
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SGE Setor 02 - Administrativo</title>
    <style>
        :root { --primary: #002855; --accent: #ffd700; }
        body { font-family: sans-serif; margin: 0; background: #f4f4f4; }
        .no-print { padding: 15px; background: var(--primary); color: white; text-align: center; }
        .container { padding: 15px; }
        .card { background: white; padding: 20px; border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); margin-bottom: 15px; }
        
        /* Estilo para Impressão de Recibo */
        .print-only { display: none; }
        @media print {
            .no-print, .nav-grid, button { display: none !important; }
            .print-only { display: block; padding: 20px; border: 2px solid #000; }
            .signature-space { margin-top: 50px; display: flex; justify-content: space-between; }
            .sig-line { border-top: 1px solid #000; width: 45%; text-align: center; padding-top: 5px; font-size: 12px; }
        }

        input, select, textarea { width: 100%; padding: 12px; margin: 10px 0; border: 1px solid #ccc; border-radius: 5px; }
        .btn { width: 100%; padding: 15px; background: #28a745; color: white; border: none; border-radius: 5px; font-weight: bold; cursor: pointer; }
    </style>
</head>
<body>

<div class="no-print">
    <h2>IEADPE - SETOR 02</h2>
    <p>Gestão de Material e Distribuição</p>
</div>

<div class="container no-print">
    <div class="card">
        <h3>📦 Registrar Entrega p/ Congregação</h3>
        <input type="text" id="recebedor_nome" placeholder="Nome do Recebedor (Assistente)">
        <select id="cong_lista">
            <option value="">Selecione a Congregação (1 a 75)</option>
            <option value="Congregação 01">Congregação 01</option>
            <option value="Congregação 02">Congregação 02</option>
        </select>
        <textarea id="lista_materiais" placeholder="Ex: 02 Água Sanitária, 01 Sabão em Pó..."></textarea>
        <button class="btn" onclick="gerarRecibo()">Gerar Recibo para Impressão</button>
    </div>
</div>

<div id="recibo" class="print-only">
    <center>
        <img src="https://upload.wikimedia.org/wikipedia/pt/0/03/Logotipo_da_IEADPE.png" width="80"><br>
        <strong>IGREJA EVANGÉLICA ASSEMBLEIA DE DEUS EM PERNAMBUCO</strong><br>
        SETOR 02 - SÃO LOURENÇO DA MATA
    </center>
    <hr>
    <h4>RECIBO DE ENTREGA DE MATERIAL</h4>
    <p><strong>Congregação:</strong> <span id="res_cong"></span></p>
    <p><strong>Materiais entregues:</strong></p>
    <div id="res_materiais" style="min-height: 100px; border: 1px solid #eee; padding: 10px;"></div>
    <p>Data: _/_/2024</p>
    
    <div class="signature-space">
        <div class="sig-line">Entregador (Depósito)</div>
        <div class="sig-line">Recebedor (Congregação)</div>
    </div>
</div>

<script>
    function gerarRecibo() {
        const cong = document.getElementById('cong_lista').value;
        const mat = document.getElementById('lista_materiais').value;
        
        if(!cong || !mat) {
            alert("Preencha a congregação e os materiais!");
            return;
        }

        document.getElementById('res_cong').innerText = cong;
        document.getElementById('res_materiais').innerText = mat;

        // Comando para abrir a janela de impressão do celular/PC
        window.print();
    }
</script>

</body>
</html>
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SGE MASTER - SETOR 02</title>
    <style>
        :root { --navy: #0B1E3D; --gold: #B8860B; --gray: #f4f4f4; }
        body { font-family: 'Segoe UI', sans-serif; margin: 0; background: var(--gray); }
        .no-print { background: var(--navy); color: white; padding: 15px; text-align: center; border-bottom: 4px solid var(--gold); }
        .nav { display: grid; grid-template-columns: repeat(3, 1fr); gap: 5px; padding: 10px; background: #ddd; }
        .nav button { padding: 10px 5px; font-size: 11px; font-weight: bold; border-radius: 4px; border: none; background: white; cursor: pointer; }
        .nav button.active { background: var(--gold); color: white; }
        .container { padding: 15px; max-width: 800px; margin: auto; }
        .card { background: white; padding: 15px; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); margin-bottom: 20px; }
        input, select, textarea { width: 100%; padding: 12px; margin: 8px 0; border: 1px solid #ccc; border-radius: 6px; box-sizing: border-box; }
        .btn-acao { width: 100%; padding: 15px; background: var(--navy); color: white; border: none; border-radius: 6px; font-weight: bold; cursor: pointer; }
        
        /* ESTILO DE IMPRESSÃO / RECIBO */
        #areaImpressao { display: none; }
        @media print {
            .no-print, .nav, .btn-acao, .card h3 { display: none !important; }
            #areaImpressao { display: block; padding: 30px; border: 1px solid #000; }
            .assinaturas { margin-top: 60px; display: flex; justify-content: space-between; }
            .linha { border-top: 1px solid #000; width: 40%; text-align: center; padding-top: 5px; font-size: 12px; }
        }
    </style>
</head>
<body>

<div class="no-print">
    <strong>IEADPE - SETOR 02</strong><br>Gestão Geral e Logística
</div>

<div class="nav no-print">
    <button onclick="aba('limpeza')">LIMPEZA/VINHO</button>
    <button onclick="aba('eletronicos')">ELETRÔNICOS</button>
    <button onclick="aba('construcao')">CONSTRUÇÃO</button>
    <button onclick="aba('samuel')">PROJ. SAMUEL</button>
    <button onclick="aba('pedidos')">FAZER PEDIDO</button>
    <button onclick="window.print()">🖨️ IMPRIMIR</button>
</div>

<div class="container" id="app"></div>
