<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Ranking de Vendedores - Recordes e Mês Atual</title>
<style>
body {
  font-family: Arial, sans-serif;
  background: #f5f5f5;
  margin: 0;
  padding: 20px;
}

h1 {
  text-align: center;
  font-size: 48px;
  margin-bottom: 10px;
}

.subtitulo {
  text-align: center;
  font-size: 22px;
  color: #555;
  margin-bottom: 30px;
}

.section-box {
  max-width: 1100px;
  margin: 0 auto 40px auto;
  background: #ffffff;
  padding: 30px 20px;
  border-radius: 20px;
  box-shadow: 0 0 20px rgba(0,0,0,0.1);
}

.section-title {
  text-align: center;
  font-size: 32px;
  margin-bottom: 20px;
  font-weight: bold;
}

/* PÓDIO DE RECORDES */
#podioRecordes {
  background: #f3fff3;
  border: 4px solid #2b7a0b;
}

.podio-container {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  gap: 40px;
}

.card-recorde {
  width: 260px;
  padding: 25px 20px;
  border-radius: 20px;
  box-shadow: 0 0 15px rgba(0,0,0,0.2);
  text-align: center;
}

.card-recorde h3 {
  margin: 10px 0 5px 0;
}

/* RANKING MÊS ATUAL */
#podioMesAtual {
  background: #e8f0ff;
  border: 4px solid #2459c4;
}

.card-podio-mes {
  width: 230px;
  padding: 22px 18px;
  border-radius: 18px;
  box-shadow: 0 0 12px rgba(0,0,0,0.15);
  text-align: center;
}

#listaMesAtual {
  max-width: 1100px;
  margin: 0 auto;
  background: #ffffff;
  padding: 20px;
  border-radius: 20px;
  box-shadow: 0 0 20px rgba(0,0,0,0.1);
}

.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 0;
  font-size: 26px;
  border-bottom: 1px solid #eee;
}

.item:last-child {
  border-bottom: none;
}

.posicao {
  width: 10%;
  font-weight: bold;
}

.nome {
  width: 60%;
  font-weight: bold;
}

.pontos {
  width: 30%;
  text-align: right;
  font-weight: bold;
}
</style>
</head>
<body>
<h1>RESULTADOS COMERCIAIS</h1>
<div class="subtitulo">Pódio de recordes + Ranking do mês atual</div>

<!-- PÓDIO DE RECORDES (RESULTADOS ANTERIORES) -->
<div id="podioRecordes" class="section-box">
  <div class="section-title">🏆 PÓDIO DE RECORDES (TODOS OS TEMPOS)</div>
  <div class="podio-container" id="podioRecordesContainer"></div>
</div>

<!-- PÓDIO DO MÊS ATUAL -->
<div id="podioMesAtual" class="section-box">
  <div class="section-title">📆 PÓDIO DO MÊS ATUAL</div>
  <div class="podio-container" id="podioMesContainer"></div>
</div>

<!-- LISTA COMPLETA DO MÊS ATUAL -->
<div id="listaMesAtual" class="section-box">
  <div class="section-title">📊 Ranking completo do mês</div>
  <div id="listaMesContainer"></div>
</div>

<script>
// =============================
// DADOS DE RECORDES (RESULTADOS ANTERIORES)
// =============================
const recordes = [
  { nome: "Mateus", matriculas: 46 },
  { nome: "João", matriculas: 42 },
];

// =============================
// DADOS DO MÊS ATUAL
// (EDITE APENAS ESSES NÚMEROS QUANDO ATUALIZAR)
// =============================
const mesAtual = [
  { nome: "João", matriculas: 27 },
  { nome: "Leticia", matriculas: 20 },
  { nome: "Marcela", matriculas: 16 },
  { nome: "Eduarda", matriculas: 10 },
  { nome: "Mateus", matriculas: 8 },
  { nome: "Sarah", matriculas: 4 },
  { nome: "Kimberly", matriculas: 3 },
  { nome: "Larissa", matriculas: 3 },
];

// Ordenar recordes (maior para menor)
const rankingRecordes = [...recordes].sort((a,b) => b.matriculas - a.matriculas);

// Ordenar mês atual (maior para menor)
const rankingMes = [...mesAtual].sort((a,b) => b.matriculas - a.matriculas);

// -----------------------------
// GERAR PÓDIO DE RECORDES
// -----------------------------
function gerarPodioRecordes() {
  const container = document.getElementById('podioRecordesContainer');
  container.innerHTML = '';

  const medalhas = [
    { label: '🥇', cor: '#d4af37', bg: '#fff7d6', destaque: true },
    { label: '🥈', cor: '#b5b5b5', bg: '#e0e0e0', destaque: false },
  ];

  rankingRecordes.forEach((v, i) => {
    const m = medalhas[i] || { label: '🏅', cor: '#666', bg: '#f0f0f0', destaque: false };

    container.innerHTML += `
      <div class="card-recorde" style="background:${m.bg}; border:${m.destaque ? '3px solid ' + m.cor : 'none'}; transform:${m.destaque ? 'scale(1.05)' : 'scale(1)'};">
        <div style="font-size:60px; font-weight:bold; color:${m.cor};">${m.label}</div>
        <h3 style="font-size:40px;">${v.nome}</h3>
        <p style="font-size:32px; font-weight:bold;">${v.matriculas} matrículas</p>
        <p style="font-size:18px; margin-top:5px; color:#555;">Recorde pessoal</p>
      </div>
    `;
  });
}

// -----------------------------
// GERAR PÓDIO DO MÊS ATUAL
// -----------------------------
function gerarPodioMes() {
  const container = document.getElementById('podioMesContainer');
  container.innerHTML = '';

  const posicoes = [
    { label: '🥇', cor: '#d4af37', bg: '#fff7d6', escala: 1.1 },
    { label: '🥈', cor: '#b5b5b5', bg: '#e0e0e0', escala: 1.0 },
    { label: '🥉', cor: '#caa075', bg: '#f0d4b2', escala: 0.95 },
  ];

  for (let i = 0; i < 3; i++) {
    const vendedor = rankingMes[i] || { nome: '—', matriculas: '—' };
    const p = posicoes[i];

    container.innerHTML += `
      <div class="card-podio-mes" style="background:${p.bg}; transform:scale(${p.escala});">
        <div style="font-size:52px; font-weight:bold; color:${p.cor};">${p.label}</div>
        <h3 style="font-size:38px; margin-top:10px;">${vendedor.nome}</h3>
        <p style="font-size:30px; font-weight:bold; margin-top:8px;">${vendedor.matriculas} matrículas</p>
      </div>
    `;
  }
}

// -----------------------------
// GERAR LISTA COMPLETA DO MÊS
// -----------------------------
function gerarListaMes() {
  const container = document.getElementById('listaMesContainer');
  container.innerHTML = '';

  rankingMes.forEach((v, i) => {
    container.innerHTML += `
      <div class="item">
        <div class="posicao">${i + 1}º</div>
        <div class="nome">${v.nome}</div>
        <div class="pontos">${v.matriculas} matrículas</div>
      </div>
    `;
  });
}

// Executar tudo
gerarPodioRecordes();
gerarPodioMes();
gerarListaMes();
</script>

</body>
</html>
