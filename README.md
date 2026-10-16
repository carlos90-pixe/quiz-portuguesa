
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quiz de Português</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #eef1ff;
      text-align: center;
      padding: 30px 15px;
    }

    .jogo {
      max-width: 600px;
      margin: auto;
      background: white;
      padding: 25px;
      border-radius: 20px;
      box-shadow: 0 5px 20px #0002;
    }

    h1 { color: #5865f2; }

    button {
      display: block;
      width: 100%;
      padding: 14px;
      margin: 10px 0;
      border: 0;
      border-radius: 10px;
      background: #5865f2;
      color: white;
      font-size: 16px;
      cursor: pointer;
    }

    button:hover { background: #414bd0; }

    #feedback {
      font-weight: bold;
      margin: 18px 0;
    }
  </style>
</head>
<body>
  <div class="jogo">
    <h1>📚 Quiz de Português</h1>
    <p id="progresso">Pergunta 1 de 10</p>
    <h2 id="pergunta"></h2>
    <div id="alternativas"></div>
    <p id="feedback"></p>
    <p id="pontos">Pontos: 0</p>
    <button id="proximo" hidden>Próxima pergunta</button>
  </div>

  <script>
    const perguntas = [
      {
        pergunta: "Qual palavra está escrita corretamente?",
        alternativas: ["Caxorro", "Cachorro", "Cachoro"],
        correta: 1
      },
      {
        pergunta: "Qual é o plural de pão?",
        alternativas: ["Pãos", "Pães", "Pãoses"],
        correta: 1
      },
      {
        pergunta: "Qual destas palavras é um verbo?",
        alternativas: ["Janela", "Bonito", "Brincar"],
        correta: 2
      },
      {
        pergunta: "Qual é o antônimo de feliz?",
        alternativas: ["Contente", "Triste", "Alegre"],
        correta: 1
      },
      {
        pergunta: "Qual palavra é um substantivo?",
        alternativas: ["Cidade", "Correr", "Bonito"],
        correta: 0
      },
      {
        pergunta: "Qual é o feminino de ator?",
        alternativas: ["Autora", "Atriz", "Atora"],
        correta: 1
      },
      {
        pergunta: "Qual palavra é um adjetivo?",
        alternativas: ["Mesa", "Correr", "Bonito"],
        correta: 2
      },
      {
        pergunta: "Qual é um sinônimo de feliz?",
        alternativas: ["Contente", "Nervoso", "Cansado"],
        correta: 0
      },
      {
        pergunta: "Qual sinal usamos no final de uma pergunta?",
        alternativas: [".", ",", "?"],
        correta: 2
      },
      {
        pergunta: "Qual palavra está acentuada corretamente?",
        alternativas: ["Lapís", "Lapis", "Lápis"],
        correta: 2
      }
    ];

    let indice = 0;
    let pontos = 0;
    let respondeu = false;

    const pergunta = document.getElementById("pergunta");
    const alternativas = document.getElementById("alternativas");
    const feedback = document.getElementById("feedback");
    const progresso = document.getElementById("progresso");
    const pontuacao = document.getElementById("pontos");
    const proximo = document.getElementById("proximo");

    function mostrarPergunta() {
      respondeu = false;
      feedback.textContent = "";
      proximo.hidden = true;

      if (indice >= perguntas.length) {
        pergunta.textContent = "🏆 Jogo concluído!";
        alternativas.innerHTML = "";
        progresso.textContent = "Fim do jogo";
        feedback.textContent =
          `Você fez ${pontos} de 100 pontos!`;
        proximo.textContent = "Jogar novamente";
        proximo.hidden = false;
        return;
      }

      const atual = perguntas[indice];
      progresso.textContent =
        `Pergunta ${indice + 1} de ${perguntas.length}`;
      pergunta.textContent = atual.pergunta;
      alternativas.innerHTML = "";

      atual.alternativas.forEach((texto, i) => {
        const botao = document.createElement("button");
        botao.textContent = texto;
        botao.onclick = () => responder(i);
        alternativas.appendChild(botao);
      });

      pontuacao.textContent = `Pontos: ${pontos}`;
    }

    function responder(escolha) {
      if (respondeu) return;
      respondeu = true;

      const correta = perguntas[indice].correta;

      if (escolha === correta) {
        pontos += 10;
        feedback.textContent = "✅ Resposta correta! +10 pontos";
      } else {
        feedback.textContent =
          "❌ Resposta incorreta. Correta: " +
          perguntas[indice].alternativas[correta];
      }

      pontuacao.textContent = `Pontos: ${pontos}`;
      proximo.textContent =
        indice === perguntas.length - 1
          ? "Ver resultado"
          : "Próxima pergunta";
      proximo.hidden = false;
    }

    proximo.onclick = () => {
      if (indice >= perguntas.length) {
        indice = 0;
        pontos = 0;
        proximo.textContent = "Próxima pergunta";
      } else {
        indice++;
      }

      mostrarPergunta();
    };

    mostrarPergunta();
  </script>
</body>
</html>

