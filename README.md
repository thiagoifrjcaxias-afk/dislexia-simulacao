<!doctype html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Simulação de Leitura Disléxica (Animada)</title>
<style>
  body {
    font-family: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    line-height: 1.6;
    color: #111;
    padding: 2rem;
    background: #fff;
  }
  h1 { font-size: 1.8rem; margin-top: 0; }
  button {
    background: #0077cc;
    color: white;
    border: none;
    padding: 0.6rem 1rem;
    border-radius: 6px;
    cursor: pointer;
  }
  button:hover { background: #005fa3; }
  p {
    font-size: 1.1rem;
    max-width: 700px;
    transition: all 0.3s ease;
  }
</style>
</head>
<body>
  <h1>Simulação de Leitura Disléxica (Animada)</h1>
  <button id="toggle">Ativar simulação</button>

  <p id="texto">
    Se você tivesse dislexia, provavelmente leria dessa maneira os slides que o professor projeta em sala de aula, o material de apoio, os textos e até as provas. A dislexia é um transtorno específico de aprendizagem de origem neurológica, que afeta as habilidades de leitura e escrita. A pessoa com dislexia tem inteligência e criatividade comuns ou até acima da média, mas enfrenta desafios para reconhecer palavras, decodificar sons e compreender o que lê com fluência. Agora que você experimentou um pouquinho dessa sensação... E aí, como foi tentar ler?
  </p>

<script>
  function shuffleWord(word) {
    if (word.length <= 3) return word;
    const middle = word.slice(1, -1).split('');
    for (let i = middle.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [middle[i], middle[j]] = [middle[j], middle[i]];
    }
    return word[0] + middle.join('') + word[word.length - 1];
  }

  let ativo = false;
  const texto = document.getElementById('texto');
  const original = texto.innerText;
  let intervalID = null;

  function embaralharAnimado() {
    texto.innerHTML = original
      .split(' ')
      .map(w => {
        // 40% das palavras serão embaralhadas por vez
        return Math.random() < 0.4 ? shuffleWord(w) : w;
      })
      .join(' ');

    // adiciona leve movimento vertical randômico
    const palavras = texto.querySelectorAll('span');
    palavras.forEach(span => {
      const deslocamento = (Math.random() - 0.5) * 4; // movimento suave
      span.style.display = 'inline-block';
      span.style.transform = `translateY(${deslocamento}px)`;
    });
  }

  document.getElementById('toggle').addEventListener('click', () => {
    ativo = !ativo;
    if (ativo) {
      // transforma cada palavra em um span
      const palavras = original.split(' ').map(w => `<span>${w}</span>`).join(' ');
      texto.innerHTML = palavras;
      intervalID = setInterval(embaralharAnimado, 400);
      document.getElementById('toggle').innerText = 'Desativar simulação';
    } else {
      clearInterval(intervalID);
      texto.innerText = original;
      document.getElementById('toggle').innerText = 'Ativar simulação';
    }
  });
</script>
</body>
</html>
