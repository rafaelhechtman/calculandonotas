<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Nota Necessária</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        .input-group { margin-bottom: 15px; }
        .result { margin-top: 20px; font-weight: bold; }
    </style>
</head>
<body>

    <h2>Calculadora de Nota Necessária para Atingir Média</h2>

    <div class="input-group">
        <label>Média Desejada: <input type="number" id="mediaDesejada" min="0" max="100" placeholder="Ex: 60"></label>
    </div>

    <div id="avaliacoes-container">
        <div class="input-group">
            <label>Nota da Avaliação: <input type="number" class="nota" min="0" max="100" placeholder="0-100"></label>
        </div>
    </div>

    <button onclick="adicionarAvaliacao()">Adicionar Outra Avaliação</button>
    <button onclick="calcularNotaNecessaria()">Calcular Nota Necessária</button>

    <div id="resultado" class="result"></div>

    <script>
        function adicionarAvaliacao() {
            const container = document.getElementById("avaliacoes-container");
            const novaAvaliacao = document.createElement("div");
            novaAvaliacao.classList.add("input-group");
            novaAvaliacao.innerHTML = `
                <label>Nota da Avaliação: <input type="number" class="nota" min="0" max="100" placeholder="0-100"></label>
            `;
            container.appendChild(novaAvaliacao);
        }

        function calcularNotaNecessaria() {
            const notas = document.getElementsByClassName("nota");
            const mediaDesejada = parseFloat(document.getElementById("mediaDesejada").value) || 0;
            let somaNotas = 0;
            let numAvaliacoes = 0;

            for (let i = 0; i < notas.length; i++) {
                const nota = parseFloat(notas[i].value);
                if (!isNaN(nota)) {
                    somaNotas += nota;
                    numAvaliacoes++;
                }
            }

            const mediaAtual = somaNotas / numAvaliacoes;
            const notaNecessaria = (mediaDesejada * (numAvaliacoes + 1)) - somaNotas;

            const resultado = document.getElementById("resultado");
            if (notaNecessaria > 100) {
                resultado.innerHTML = `Para atingir uma média de ${mediaDesejada}, você precisaria de ${notaNecessaria.toFixed(2)}, o que é superior a 100. Atingir essa média pode não ser possível.`;
            } else if (notaNecessaria <= 0) {
                resultado.innerHTML = `Parabéns! Com as notas atuais, você já alcançou a média desejada de ${mediaDesejada}.`;
            } else {
                resultado.innerHTML = `Para atingir uma média de ${mediaDesejada}, você precisa de ${notaNecessaria.toFixed(2)} na próxima avaliação.`;
            }
        }
    </script>

</body>
</html>
