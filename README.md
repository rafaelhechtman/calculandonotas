<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Notas para Aprovação</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        .input-group { margin-bottom: 15px; }
        .result { margin-top: 20px; }
    </style>
</head>
<body>

    <h2>Calculadora de Notas Necessárias para Aprovação</h2>

    <form action="/calcular" method="post" id="form">
        <div id="disciplinas-container">
            <div class="input-group">
                <label>Disciplina: <input type="text" name="disciplina" placeholder="Ex: Matemática"></label>
                <label>Nota 1º Trimestre: <input type="number" name="nota1" min="0" max="100" placeholder="0-100"></label>
                <label>Nota 2º Trimestre: <input type="number" name="nota2" min="0" max="100" placeholder="0-100"></label>
            </div>
        </div>

        <button type="button" onclick="adicionarDisciplina()">Adicionar Outra Disciplina</button>
        <button type="submit">Calcular Notas Necessárias</button>
    </form>

    <div id="resultado" class="result">
        {% if resultados %}
            <h3>Resultados:</h3>
            {% for disciplina, media in resultados %}
                <p>{{ disciplina }}: Você precisa de {{ media }} no 3º trimestre.</p>
            {% endfor %}
        {% endif %}
    </div>

    <script>
        function adicionarDisciplina() {
            const container = document.getElementById("disciplinas-container");
            const novaDisciplina = document.createElement("div");
            novaDisciplina.classList.add("input-group");
            novaDisciplina.innerHTML = `
                <label>Disciplina: <input type="text" name="disciplina" placeholder="Ex: Matemática"></label>
                <label>Nota 1º Trimestre: <input type="number" name="nota1" min="0" max="100" placeholder="0-100"></label>
                <label>Nota 2º Trimestre: <input type="number" name="nota2" min="0" max="100" placeholder="0-100"></label>
            `;
            container.appendChild(novaDisciplina);
        }
    </script>

</body>
</html>
