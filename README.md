<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Nota Necessária para Aprovação Anual</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        .container { max-width: 600px; margin: auto; }
        .input-group { margin-bottom: 20px; }
        .trimestre-header { font-size: 1.2em; font-weight: bold; margin-top: 10px; }
        .result, .verification { margin-top: 20px; }
        .result { font-weight: bold; font-size: 1.1em; color: #2E8B57; }
        label { display: block; margin-top: 10px; }
        input[type="number"] { width: 100px; padding: 5px; margin-top: 5px; }
        button { margin-top: 20px; padding: 10px 20px; font-size: 1em; cursor: pointer; }
        table { width: 100%; margin-top: 20px; border-collapse: collapse; }
        th, td { padding: 10px; border: 1px solid #ddd; text-align: center; }
        .edit-btn, .delete-btn { cursor: pointer; color: blue; text-decoration: underline; }
    </style>
</head>
<body>

<div class="container">
    <h2>Calculadora de Nota Necessária na AV3 do 3º Trimestre</h2>
    <h4>Feito por Rafael Edler Hechtman</h4>

    <label for="materia">Selecione a Matéria:</label>
    <select id="materia">
        <option value="matematica1">Matemática 1</option>
        <option value="matematica2">Matemática 2</option>
        <option value="quimica1">Química 1</option>
        <option value="quimica2">Química 2</option>
        <option value="biologia1">Biologia 1</option>
        <option value="biologia2">Biologia 2</option>
        <option value="fisica1">Física 1</option>
        <option value="fisica2">Física 2</option>
        <option value="portugues">Português</option>
        <option value="historia">História</option>
        <option value="geografia">Geografia</option>
        <option value="literatura">Literatura</option>
        <option value="ingles">Inglês</option>
        <option value="filosofia">Filosofia</option>
    </select>

    <div class="input-group">
        <div class="trimestre-header">1º Trimestre</div>
        <label>Média (ou insira as notas abaixo): <input type="number" id="media1" placeholder="Ex: 6.0" step="0.1" min="0" max="10"></label>
        <label>AV1 (5,0): <input type="number" id="av1_1" placeholder="0-5" step="0.1" min="0" max="5"></label>
        <label>AV2 (5,0): <input type="number" id="av2_1" placeholder="0-5" step="0.1" min="0" max="5"></label>
        <label>AV3 (10,0): <input type="number" id="av3_1" placeholder="0-10" step="0.1" min="0" max="10"></label>
    </div>

    <div class="input-group">
        <div class="trimestre-header">2º Trimestre</div>
        <label>Média (ou insira as notas abaixo): <input type="number" id="media2" placeholder="Ex: 7.0" step="0.1" min="0" max="10"></label>
        <label>AV1 (5,0): <input type="number" id="av1_2" placeholder="0-5" step="0.1" min="0" max="5"></label>
        <label>AV2 (5,0): <input type="number" id="av2_2" placeholder="0-5" step="0.1" min="0" max="5"></label>
        <label>AV3 (10,0): <input type="number" id="av3_2" placeholder="0-10" step="0.1" min="0" max="10"></label>
    </div>

    <div class="input-group">
        <div class="trimestre-header">3º Trimestre (Notas Parciais)</div>
        <label>AV1 (5,0): <input type="number" id="av1_3" placeholder="0-5" step="0.1" min="0" max="5"></label>
        <label>AV2 (5,0): <input type="number" id="av2_3" placeholder="0-5" step="0.1" min="0" max="5"></label>
    </div>

    <div class="input-group">
        <div class="trimestre-header">Média Anual Desejada</div>
        <label>Média Anual Desejada: <input type="number" id="media_desejada_anual" placeholder="Ex: 6.0" step="0.1" min="0" max="10"></label>
    </div>

    <button onclick="calcularNotaNecessaria()">Calcular Nota Necessária na AV3</button>
    <button onclick="salvarResultado()">Salvar Resultado</button>
    
    <div id="resultado" class="result"></div>
    <div id="verificacao" class="verification"></div>

    <table id="resultadosTable" style="display:none;">
        <thead>
            <tr>
                <th>Matéria</th>
                <th>Média 1º Tri</th>
                <th>Média 2º Tri</th>
                <th>Notas 3º Tri (AV1 e AV2)</th>
                <th>Nota Necessária AV3</th>
                <th>Média Anual Desejada</th>
                <th>Ações</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
</div>

<script>
    let notaNecessariaAV3, mediaTerceiroComNotaAV3, mediaDesejadaAnual;

    function calcularMediaTrimestral(av1, av2, av3) {
        return Math.ceil((av1 + av2 + av3) / 2);
    }

    function calcularNotaNecessaria() {
        const media1 = parseFloat(document.getElementById("media1").value) || calcularMediaTrimestral(
            parseFloat(document.getElementById("av1_1").value) || 0,
            parseFloat(document.getElementById("av2_1").value) || 0,
            parseFloat(document.getElementById("av3_1").value) || 0
        );

        const media2 = parseFloat(document.getElementById("media2").value) || calcularMediaTrimestral(
            parseFloat(document.getElementById("av1_2").value) || 0,
            parseFloat(document.getElementById("av2_2").value) || 0,
            parseFloat(document.getElementById("av3_2").value) || 0
        );

        const av1_3 = parseFloat(document.getElementById("av1_3").value) || 0;
        const av2_3 = parseFloat(document.getElementById("av2_3").value) || 0;
        mediaDesejadaAnual = parseFloat(document.getElementById("media_desejada_anual").value) || 6.0;

        const pesoTerceiroTrimestre = 2;
        const mediaNecessariaAnual = mediaDesejadaAnual * 4;
        const somaMedias = media1 + media2;
        const mediaNecessariaTerceiroTrimestre = (mediaNecessariaAnual - somaMedias) / pesoTerceiroTrimestre;
        const totalParcialTerceiro = av1_3 + av2_3;
        notaNecessariaAV3 = (mediaNecessariaTerceiroTrimestre * 2 - totalParcialTerceiro);
        mediaTerceiroComNotaAV3 = calcularMediaTrimestral(av1_3, av2_3, notaNecessariaAV3);

        const resultado = document.getElementById("resultado");

        if (notaNecessariaAV3 > 10) {
            resultado.innerHTML += `Para atingir uma média anual de ${mediaDesejadaAnual}, você precisaria de ${notaNecessariaAV3.toFixed(1)} na AV3, o que é superior a 10. Atingir essa média pode não ser possível.`;
        } else if (notaNecessariaAV3 <= 0) {
            resultado.innerHTML = `Parabéns! Com as notas atuais, você já alcançou a média anual desejada de ${mediaDesejadaAnual}.`;
        } else {
            resultado.innerHTML = `Para atingir uma média anual de ${mediaDesejadaAnual}, você precisa de ${notaNecessariaAV3.toFixed(1)} na AV3 do 3º trimestre. Com essa nota, sua média do 3º trimestre será ${mediaTerceiroComNotaAV3}.`;
        }
    }

    function salvarResultado() {
        const materia = document.getElementById("materia").value;
        const media1 = document.getElementById("media1").value || calcularMediaTrimestral(
            parseFloat(document.getElementById("av1_1").value) || 0,
            parseFloat(document.getElementById("av2_1").value) || 0,
            parseFloat(document.getElementById("av3_1").value) || 0
        );
        const media2 = document.getElementById("media2").value || calcularMediaTrimestral(
            parseFloat(document.getElementById("av1_2").value) || 0,
            parseFloat(document.getElementById("av2_2").value) || 0,
            parseFloat(document.getElementById("av3_2").value) || 0
        );
        const av1_3 = document.getElementById("av1_3").value || 0;
        const av2_3 = document.getElementById("av2_3").value || 0;
        const mediaAnualDesejada = document.getElementById("media_desejada_anual").value || 6.0;

        const tabela = document.getElementById("resultadosTable");
        tabela.style.display = "table";

        const novaLinha = tabela.insertRow(-1);
        novaLinha.innerHTML = `
            <td>${materia}</td>
            <td>${media1}</td>
            <td>${media2}</td>
            <td>${av1_3} e ${av2_3}</td>
            <td>${notaNecessariaAV3.toFixed(1)}</td>
            <td>${mediaAnualDesejada}</td>
            <td><span class="edit-btn" onclick="editarLinha(this)">Editar</span> | <span class="delete-btn" onclick="deletarLinha(this)">Deletar</span></td>
        `;
    }

    function editarLinha(elemento) {
        const linha = elemento.parentNode.parentNode;
        const cells = linha.getElementsByTagName("td");

        document.getElementById("materia").value = cells[0].textContent;
        document.getElementById("media1").value = cells[1].textContent;
        document.getElementById("media2").value = cells[2].textContent;
        document.getElementById("av1_3").value = cells[3].textContent.split(" e ")[0];
        document.getElementById("av2_3").value = cells[3].textContent.split(" e ")[1];
        document.getElementById("media_desejada_anual").value = cells[5].textContent;

        linha.remove();
    }

    function deletarLinha(elemento) {
        const linha = elemento.parentNode.parentNode;
        linha.remove();
    }
</script>

</body>
</html>

