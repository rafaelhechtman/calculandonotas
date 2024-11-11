<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Média por Matéria</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        .input-group { margin-bottom: 15px; }
        .result { margin-top: 20px; font-weight: bold; }
    </style>
</head>
<body>

    <h2>Calculadora de Média por Matéria</h2>

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
            resultado.innerHTML = `<h3>Média por Trimestre</h3>`;
            
            let somaMedias = 0;
            let medias = [];
            let peso = [1, 1, 2]; // Peso dos trimestres

            for (let i = 0; i < trimestres.length; i++) {
                const av1 = parseFloat(trimestres[i].getElementsByClassName("av1")[0].value) || 0;
                const av2 = parseFloat(trimestres[i].getElementsByClassName("av2")[0].value) || 0;
                const av3 = parseFloat(trimestres[i].getElementsByClassName("av3")[0].value) || 0;
                const totalNotas = av1 + av2 + av3;

                // Cálculo da média trimestral: (AV1 + AV2 + AV3) / 2
                const mediaTrimestre = Math.ceil(totalNotas / 2);
                medias.push(mediaTrimestre);

                resultado.innerHTML += `<p>Média do ${i + 1}º Trimestre: ${mediaTrimestre}</p>`;

                // Soma das médias considerando os pesos
                somaMedias += mediaTrimestre * peso[i];
            }

            // Cálculo da média anual com peso dobrado no 3º trimestre
            const mediaAnual = somaMedias / 4;

            if (mediaAnual >= 6) {
                resultado.innerHTML += `<p><strong>Sua média anual é ${mediaAnual.toFixed(2)}, e você foi aprovado.</strong></p>`;
            } else {
                // Nota necessária no terceiro trimestre para aprovação
                const mediaNecessariaTerceiro = Math.max(6 * 4 - (medias[0] + medias[1] + medias[2]), 0) / 2;
                resultado.innerHTML += `<p>Sua média anual atual é ${mediaAnual.toFixed(2)}. Para ser aprovado, você precisará de ${Math.ceil(mediaNecessariaTerceiro)} na média do 3º trimestre.</p>`;
            }
        }
    </script>

</body>
</html>
