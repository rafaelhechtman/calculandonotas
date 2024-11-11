<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Nota Necessária para Aprovação</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        .input-group { margin-bottom: 15px; }
        .result { margin-top: 20px; font-weight: bold; }
    </style>
</head>
<body>

    <h2>Calculadora de Nota Necessária para Aprovação Anual</h2>

    <div id="trimestres-container">
        <div class="trimestre">
            <h3>1º Trimestre</h3>
            <div class="input-group">
                <label>AV1 (5,0): <input type="number" class="av1" min="0" max="5" placeholder="0-5"></label>
                <label>AV2 (5,0): <input type="number" class="av2" min="0" max="5" placeholder="0-5"></label>
                <label>AV3 (10,0): <input type="number" class="av3" min="0" max="10" placeholder="0-10"></label>
            </div>
        </div>

        <div class="trimestre">
            <h3>2º Trimestre</h3>
            <div class="input-group">
                <label>AV1 (5,0): <input type="number" class="av1" min="0" max="5" placeholder="0-5"></label>
                <label>AV2 (5,0): <input type="number" class="av2" min="0" max="5" placeholder="0-5"></label>
                <label>AV3 (10,0): <input type="number" class="av3" min="0" max="10" placeholder="0-10"></label>
            </div>
        </div>

        <div class="trimestre">
            <h3>3º Trimestre</h3>
            <div class="input-group">
                <label>AV1 (5,0): <input type="number" class="av1" min="0" max="5" placeholder="0-5"></label>
                <label>AV2 (5,0): <input type="number" class="av2" min="0" max="5" placeholder="0-5"></label>
                <label>AV3 (10,0): <input type="number" class="av3" min="0" max="10" placeholder="0-10"></label>
            </div>
        </div>
    </div>

    <button onclick="calcularMedia()">Calcular Média Anual</button>

    <div id="resultado" class="result"></div>

    <script>
        function calcularMedia() {
            const trimestres = document.getElementsByClassName("trimestre");
            const resultado = document.getElementById("resultado");

            let somaMedias = 0;
            let medias = [];
            let peso = [1, 1, 2]; // Peso dos trimestres

            for (let i = 0; i < trimestres.length; i++) {
                const av1 = parseFloat(trimestres[i].getElementsByClassName("av1")[0].value) || 0;
                const av2 = parseFloat(trimestres[i].getElementsByClassName("av2")[0].value) || 0;
                const av3 = parseFloat(trimestres[i].getElementsByClassName("av3")[0].value) || 0;

                // Cálculo da média trimestral: (AV1 + AV2 + AV3) / 2
                const mediaTrimestre = Math.ceil((av1 + av2 + av3) / 2);
                medias.push(mediaTrimestre);

                // Soma das médias considerando os pesos
                somaMedias += mediaTrimestre * peso[i];
            }

            // Cálculo da média anual com peso dobrado no 3º trimestre
            const mediaAnual = somaMedias / 4;

            if (mediaAnual >= 6) {
                resultado.innerHTML = `Parabéns! Sua média anual é ${mediaAnual.toFixed(2)}, e você foi aprovado.`;
            } else {
                // Nota necessária no terceiro trimestre para aprovação
                const mediaNecessariaTerceiro = Math.max(6 * 4 - (medias[0] + medias[1] + medias[2]), 0) / 2;
                resultado.innerHTML = `Sua média anual atual é ${mediaAnual.toFixed(2)}. Para ser aprovado, você precisará de ${Math.ceil(mediaNecessariaTerceiro)} na média do 3º trimestre.`;
            }
        }
    </script>

</body>
</html>
