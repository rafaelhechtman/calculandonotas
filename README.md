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
        .result { margin-top: 20px; font-weight: bold; font-size: 1.1em; color: #2E8B57; }
        label { display: block; margin-top: 10px; }
        input[type="number"] { width: 100px; padding: 5px; margin-top: 5px; }
        button { margin-top: 20px; padding: 10px 20px; font-size: 1em; cursor: pointer; }
    </style>
</head>
<body>

<div class="container">
    <h2>Calculadora de Nota Necessária na AV3 do 3º Trimestre</h2>

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
        <div class="trimestre-header">Médias Desejadas</div>
        <label>Média Desejada para o 3º Trimestre: <input type="number" id="media_desejada_3" placeholder="Ex: 5.5" step="0.1" min="0" max="10"></label>
        <label>Média Anual Desejada: <input type="number" id="media_desejada_anual" placeholder="Ex: 6.0" step="0.1" min="0" max="10"></label>
    </div>

    <button onclick="calcularNotaNecessaria()">Calcular Nota Necessária na AV3</button>

    <div id="resultado" class="result"></div>
</div>

<script>
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
        const mediaDesejadaTerceiro = parseFloat(document.getElementById("media_desejada_3").value) || null;
        const mediaDesejadaAnual = parseFloat(document.getElementById("media_desejada_anual").value) || 6.0;

        // Peso dos trimestres e média anual necessária
        const pesoTerceiroTrimestre = 2;
        const mediaNecessariaAnual = mediaDesejadaAnual * 4;

        // Soma das médias do 1º e 2º trimestre
        const somaMedias = media1 + media2;

        // Média necessária para o 3º trimestre com base na média anual desejada
        const mediaNecessariaTerceiroTrimestre = mediaDesejadaTerceiro !== null
            ? mediaDesejadaTerceiro
            : (mediaNecessariaAnual - somaMedias) / pesoTerceiroTrimestre;

        // Nota necessária na AV3 do 3º trimestre para alcançar essa média
        const totalParcialTerceiro = av1_3 + av2_3;
        const notaNecessariaAV3 = (mediaNecessariaTerceiroTrimestre * 2 - totalParcialTerceiro);

        // Cálculo da média do 3º trimestre com a nota necessária na AV3
        const mediaTerceiroComNotaAV3 = calcularMediaTrimestral(av1_3, av2_3, notaNecessariaAV3);

        const resultado = document.getElementById("resultado");

        if (notaNecessariaAV3 > 10) {
            resultado.innerHTML = `Para atingir uma média anual de ${mediaDesejadaAnual}, você precisaria de ${notaNecessariaAV3.toFixed(1)} na AV3, o que é superior a 10. Atingir essa média pode não ser possível.`;
        } else if (notaNecessariaAV3 <= 0) {
                    resultado.innerHTML = `Parabéns! Com as notas atuais, você já alcançou a média anual desejada de ${mediaDesejadaAnual}.`;
        } else {
        resultado.innerHTML = `Para atingir uma média anual de ${mediaDesejadaAnual}, você precisa de ${notaNecessariaAV3.toFixed(1)} na AV3 do 3º trimestre. Com essa nota, sua média do 3º trimestre será ${mediaTerceiroComNotaAV3}.`;
        }
    }
</script>

</body>
</html>
