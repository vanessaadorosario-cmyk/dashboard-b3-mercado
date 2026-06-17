<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <title>Macro Checklist - Rastreador do Dólar</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    * {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background: #020617;
      color: #e5e7eb;
    }
    .app {
      max-width: 960px;
      margin: 0 auto;
      padding: 24px 16px 40px;
    }
    .header {
      text-align: center;
      margin-bottom: 20px;
    }
    .header h1 {
      margin: 0 0 6px;
      font-size: 24px;
    }
    .header p {
      margin: 0;
      color: #9ca3af;
      font-size: 14px;
    }
    .cards {
      display: grid;
      grid-template-columns: minmax(0, 1.3fr) minmax(0, 1fr);
      gap: 16px;
    }
    @media (max-width: 900px) {
      .cards {
        grid-template-columns: minmax(0, 1fr);
      }
    }
    .card {
      background: #020617;
      border-radius: 16px;
      border: 1px solid #1f2937;
      padding: 14px 16px 16px;
      margin-bottom: 14px;
      box-shadow: 0 18px 40px rgba(0, 0, 0, 0.6);
    }
    .card h2 {
      margin: 0 0 8px;
      font-size: 17px;
    }
    .card h3 {
      margin: 12px 0 6px;
      font-size: 14px;
    }
    .row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin: 4px 0;
      font-size: 13px;
    }
    .label {
      color: #9ca3af;
      margin-right: 8px;
    }
    .value {
      font-weight: 600;
      text-align: right;
    }
    .tag {
      display: inline-block;
      padding: 2px 8px;
      border-radius: 999px;
      font-size: 11px;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.04em;
    }
    .tag-up {
      background: rgba(34, 197, 94, 0.14);
      color: #22c55e;
    }
    .tag-down {
      background: rgba(239, 68, 68, 0.15);
      color: #f97373;
    }
    .tag-neutral {
      background: rgba(148, 163, 184, 0.16);
      color: #e5e7eb;
    }
    .manual-block {
      margin-top: 10px;
      padding-top: 8px;
      border-top: 1px dashed #1f2937;
      font-size: 12px;
    }
    .manual-block p {
      margin: 0 0 6px;
      color: #9ca3af;
    }
    .manual-block label {
      display: block;
      margin-bottom: 6px;
    }
    .manual-block input {
      width: 100%;
      max-width: 140px;
      padding: 5px 7px;
      border-radius: 6px;
      border: 1px solid #1f2937;
      background: #020617;
      color: #e5e7eb;
      font-size: 13px;
    }
    button {
      padding: 5px 9px;
      border-radius: 6px;
      border: none;
      background: #2563eb;
      color: #e5e7eb;
      font-size: 12px;
      cursor: pointer;
    }
    button:hover {
      background: #1d4ed8;
    }
    .checkbox-group {
      display: flex;
      flex-wrap: wrap;
      gap: 6px 14px;
      margin: 4px 0 6px;
      font-size: 12px;
    }
    .checkbox-group label {
      display: flex;
      align-items: center;
      gap: 4px;
    }
    .hint {
      margin: 4px 0 0;
      font-size: 12px;
      color: #9ca3af;
    }
    .table-ativos {
      margin-top: 6px;
      border-top: 1px dashed #1f2937;
      padding-top: 6px;
      font-size: 12px;
    }
    .table-ativos table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 4px;
    }
    .table-ativos th,
    .table-ativos td {
      padding: 3px 4px;
      border-bottom: 1px solid #111827;
      text-align: left;
      font-size: 11px;
    }
    .table-ativos th {
      color: #9ca3af;
      font-weight: 500;
    }
    .tipo-risco {
      color: #22c55e;
      font-weight: 600;
    }
    .tipo-seguranca {
      color: #f59e0b;
      font-weight: 600;
    }
    .footer {
      margin-top: 18px;
      text-align: center;
      font-size: 11px;
      color: #6b7280;
    }
  </style>
</head>
<body>
  <div class="app">
    <header class="header">
      <h1>Macro Checklist</h1>
      <p>Rastreador do Dólar baseado em ativos de risco, segurança e Minério de Ferro</p>
    </header>

    <div class="cards">
      <!-- COLUNA ESQUERDA: Ativos + Minério -->
      <div>
        <section class="card">
          <h2>Minério de Ferro (Sina I0)</h2>
          <div class="row">
            <span class="label">Último preço (manual):</span>
            <span class="value" id="iron-price">--</span>
          </div>
          <div class="row">
            <span class="label">Variação diária:</span>
            <span class="value" id="iron-change">--</span>
          </div>
          <div class="row">
            <span class="label">Classificação:</span>
            <span class="value"><span id="iron-class" class="tag tag-neutral">--</span></span>
          </div>

          <div class="manual-block">
            <p>Informe a variação do minério em % (ex.: 3.5 para 3,5%).</p>
            <label>
              Variação (%):
              <input type="number" step="0.01" id="iron-manual" placeholder="Ex: 3.5" />
            </label>
            <label>
              Último preço:
              <input type="number" step="0.0001" id="iron-price-manual" placeholder="Opcional" />
            </label>
            <button id="btn-apply-iron">Aplicar minério</button>
          </div>
        </section>

        <section class="card">
          <h2>Variações dos Ativos (Investing)</h2>
          <p class="hint">
            Use os dados da sua carteira do Investing para preencher as variações (% diárias) dos ativos abaixo.
            (Por enquanto é manual. No futuro você pode automatizar com um proxy do CSV da carteira.)
          </p>

          <div class="table-ativos">
            <table>
              <thead>
                <tr>
                  <th>Código</th>
                  <th>Tipo</th>
                  <th>Var% (dia)</th>
                  <th>Status</th>
                </tr>
              </thead>
              <tbody id="ativos-tbody">
                <!-- preenchido via JS -->
              </tbody>
            </table>
          </div>

          <div class="manual-block">
            <p>Atualize as variações informando código do ativo e variação em %.</p>
            <label>
              Código:
              <input type="text" id="ativo-codigo" placeholder="EWZ, DX, USD/MXN..." />
            </label>
            <label>
              Variação (%):
              <input type="number" step="0.01" id="ativo-var" placeholder="Ex: 1.2" />
            </label>
            <button id="btn-apply-ativo">Aplicar variação</button>
          </div>
        </section>
      </div>

      <!-- COLUNA DIREITA: Score + Dólar + Notícias -->
      <div>
        <section class="card">
          <h2>Resumo Risco x Segurança</h2>
          <div class="row">
            <span class="label">Risco em ALTA (pró dólar cair):</span>
            <span class="value" id="risco-alta">--</span>
          </div>
          <div class="row">
            <span class="label">Risco em QUEDA (pró dólar subir):</span>
            <span class="value" id="risco-queda">--</span>
          </div>
          <div class="row">
            <span class="label">Segurança em ALTA (pró dólar subir):</span>
            <span class="value" id="segur-alta">--</span>
          </div>
          <div class="row">
            <span class="label">Segurança em QUEDA (pró dólar cair):</span>
            <span class="value" id="segur-queda">--</span>
          </div>
          <div class="row">
            <span class="label">Ativos neutros:</span>
            <span class="value" id="total-neutro">--</span>
          </div>
        </section>

        <section class="card">
          <h2>Cenário Macro do Dólar</h2>
          <div class="row">
            <span class="label">Score macro:</span>
            <span class="value" id="macro-score">--</span>
          </div>
          <div class="row">
            <span class="label">Tendência do Dólar:</span>
            <span class="value"><span id="usd-trend" class="tag tag-neutral">--</span></span>
          </div>
          <div class="row">
            <span class="label">Recomendação:</span>
            <span class="value" id="usd-action">--</span>
          </div>
        </section>

        <section class="card">
          <h2>Filtro de Notícias</h2>
          <p class="hint">
            Igual à tabela da aba Gráfico: operar depois de Payroll, IPC, PIB, PCE; não operar em feriado americano.
          </p>
          <div class="checkbox-group">
            <label><input type="checkbox" id="chk-payroll" /> Payroll</label>
            <label><input type="checkbox" id="chk-ipc" /> IPC</label>
            <label><input type="checkbox" id="chk-pib" /> PIB EUA</label>
            <label><input type="checkbox" id="chk-pce" /> PCE</label>
            <label><input type="checkbox" id="chk-feriado" /> Feriado EUA</label>
          </div>
          <button id="btn-update-news">Aplicar filtro</button>
          <p class="hint" id="news-hint">Operar normalmente.</p>
        </section>
      </div>
    </div>

    <footer class="footer">
      <p>Este painel é estático (HTML + CSS + JS) e pode ser hospedado diretamente no GitHub Pages.</p>
      <p>Para automatizar variações (Investing e Sina), conecte um proxy/servidor que alimente as variações no lugar da entrada manual.</p>
    </footer>
  </div>

  <script>
    // ========= 1) CONFIGURAÇÃO DOS ATIVOS (baseado na sua planilha) =========

    const LIMITE_PADRAO_ALTA = 0.001;   // 0,1% (na planilha você usa -0,001 / 0,001)
    const LIMITE_PADRAO_QUEDA = -0.001;
    const LIMITE_VX_ALTA = 0.005;
    const LIMITE_VX_QUEDA = -0.005;
    const LIMITE_MINERIO_ALTA = 0.03;   // 3%
    const LIMITE_MINERIO_QUEDA = -0.03;

    // Threshold do score para ALTA / BAIXA do Dólar
    const SCORE_ALTA = 5;
    const SCORE_BAIXA = -5;

    // Lista de ativos extraídos da região "MINÉRIO DE FERRO: 3%+ ... Ativos de segurança ..." da aba Ativos
    // tipo: risco (se sobe, Dólar tende a cair), seguranca (se sobe, Dólar tende a subir)
    let ativos = [
      // ---- BLOCO RISCO (EWZ, XLF, XLP, XLE, XME, EEM, SOXX.O, BSESN, Bolsas China, VALE, PBR etc.) ----
      { codigo: "VALE.K", nome: "Vale SA ADR", tipo: "risco", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "PBR", nome: "Petrobras ADR", tipo: "risco", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "EWZ", nome: "iShares MSCI Brazil ETF", tipo: "risco", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "XLF", nome: "Financial Select Sector SPDR", tipo: "risco", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "XLP", nome: "Consumer Staples Select Sector SPDR", tipo: "risco", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "XLE", nome: "Energy Select Sector SPDR", tipo: "risco", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "XME", nome: "SPDR S&P Metals & Mining ETF", tipo: "risco", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "EEM", nome: "iShares MSCI Emerging Markets ETF", tipo: "risco", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "SOXX.O", nome: "iShares Semiconductor ETF", tipo: "risco", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: ".BSESN", nome: "BSE Sensex 30", tipo: "risco", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "CHINA", nome: "Bolsas China", tipo: "risco", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },

      // ---- BLOCO SEGURANÇA (DX, VX, pares USD/FX, EUR/BRL, posição estrangeiros/volume como neutros) ----
      { codigo: "DX", nome: "Índice Dólar Futuros", tipo: "seguranca", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "VX", nome: "S&P 500 VIX Futuros", tipo: "seguranca", limiteAlta: LIMITE_VX_ALTA, limiteQueda: LIMITE_VX_QUEDA, variacao: 0 },
      { codigo: "USD/MXN", nome: "USD/MXN", tipo: "seguranca", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "USD/NOK", nome: "USD/NOK", tipo: "seguranca", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "USD/NZD", nome: "USD/NZD", tipo: "seguranca", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "USD/AUD", nome: "USD/AUD", tipo: "seguranca", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "USD/KRW", nome: "USD/KRW", tipo: "seguranca", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "USD/CNY", nome: "USD/CNY", tipo: "seguranca", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },
      { codigo: "EUR/BRL", nome: "EUR/BRL", tipo: "seguranca", limiteAlta: LIMITE_PADRAO_ALTA, limiteQueda: LIMITE_PADRAO_QUEDA, variacao: 0 },

      // ---- MINÉRIO (entra como risco) ----
      { codigo: "MINERIO_SINA", nome: "Minério de Ferro (Sina I0)", tipo: "risco", limiteAlta: LIMITE_MINERIO_ALTA, limiteQueda: LIMITE_MINERIO_QUEDA, variacao: 0 }
    ];

    // ========= 2) FUNÇÕES DE CLASSIFICAÇÃO E SCORE =========

    function classificarAtivo(variacao, limiteAlta, limiteQueda) {
      if (variacao >= limiteAlta) return "ALTA";
      if (variacao <= limiteQueda) return "QUEDA";
      return "NEUTRO";
    }

    function calcularScoreEDistribuicao() {
      let riscoAlta = 0, riscoQueda = 0, segurAlta = 0, segurQueda = 0, neutros = 0;
      let score = 0;

      for (const ativo of ativos) {
        const status = classificarAtivo(ativo.variacao, ativo.limiteAlta, ativo.limiteQueda);
        ativo.status = status;

        if (status === "NEUTRO") {
          neutros++;
          continue;
        }

        if (ativo.tipo === "risco") {
          if (status === "ALTA") {
            riscoAlta++;
            score -= 1; // risco subindo -> dólar tende a cair
          } else if (status === "QUEDA") {
            riscoQueda++;
            score += 1; // risco caindo -> dólar tende a subir
          }
        } else if (ativo.tipo === "seguranca") {
          if (status === "ALTA") {
            segurAlta++;
            score += 1; // segurança subindo -> dólar tende a subir
          } else if (status === "QUEDA") {
            segurQueda++;
            score -= 1; // segurança caindo -> dólar tende a cair
          }
        }
      }

      return { riscoAlta, riscoQueda, segurAlta, segurQueda, neutros, score };
    }

    function tendenciaEDecisaoDolar(score) {
      if (score >= SCORE_ALTA) {
        return {
          tendencia: "ALTA",
          acao: "Buscar compras de Dólar em correções (viés forte de alta)."
        };
      } else if (score <= SCORE_BAIXA) {
        return {
          tendencia: "BAIXA",
          acao: "Buscar vendas de Dólar em repiques (viés forte de baixa)."
        };
      } else {
        return {
          tendencia: "NEUTRO",
          acao: "Operar menor / seletivo, sem viés macro claro."
        };
      }
    }

    // ========= 3) UTILITÁRIOS DE UI =========

    function setTag(el, texto, tipo) {
      el.textContent = texto;
      el.classList.remove("tag-up", "tag-down", "tag-neutral");
      if (tipo === "up") el.classList.add("tag-up");
      else if (tipo === "down") el.classList.add("tag-down");
      else el.classList.add("tag-neutral");
    }

    function atualizarResumoNews() {
      const payroll = document.getElementById("chk-payroll").checked;
      const ipc = document.getElementById("chk-ipc").checked;
      const pib = document.getElementById("chk-pib").checked;
      const pce = document.getElementById("chk-pce").checked;
      const feriado = document.getElementById("chk-feriado").checked;
      const hint = document.getElementById("news-hint");

      if (feriado) {
        hint.textContent = "Feriado americano: NÃO OPERAR (liquidez ruim).";
        return;
      }
      if (payroll || ipc || pib || pce) {
        hint.textContent = "Dia de dado importante: operar preferencialmente depois do dado.";
      } else {
        hint.textContent = "Operar normalmente (sem grandes dados no checklist).";
      }
    }

    // Atualiza a tabela de ativos na tela
    function renderTabelaAtivos() {
      const tbody = document.getElementById("ativos-tbody");
      tbody.innerHTML = "";
      for (const ativo of ativos) {
        if (ativo.codigo === "MINERIO_SINA") continue; // minério é mostrado separado
        const tr = document.createElement("tr");

        const tdCod = document.createElement("td");
        tdCod.textContent = ativo.codigo;
        tr.appendChild(tdCod);

        const tdTipo = document.createElement("td");
        tdTipo.textContent = ativo.tipo === "risco" ? "Risco" : "Segurança";
        tdTipo.className = ativo.tipo === "risco" ? "tipo-risco" : "tipo-seguranca";
        tr.appendChild(tdTipo);

        const tdVar = document.createElement("td");
        const pct = ativo.variacao * 100;
        tdVar.textContent = isNaN(pct) ? "--" : pct.toFixed(2) + " %";
        tr.appendChild(tdVar);

        const tdStatus = document.createElement("td");
        tdStatus.textContent = ativo.status || "NEUTRO";
        tr.appendChild(tdStatus);

        tbody.appendChild(tr);
      }
    }

    function atualizarPainel() {
      const { riscoAlta, riscoQueda, segurAlta, segurQueda, neutros, score } =
        calcularScoreEDistribuicao();

      document.getElementById("risco-alta").textContent = riscoAlta;
      document.getElementById("risco-queda").textContent = riscoQueda;
      document.getElementById("segur-alta").textContent = segurAlta;
      document.getElementById("segur-queda").textContent = segurQueda;
      document.getElementById("total-neutro").textContent = neutros;
      document.getElementById("macro-score").textContent = score;

      const { tendencia, acao } = tendenciaEDecisaoDolar(score);
      const usdTrendEl = document.getElementById("usd-trend");
      const usdActionEl = document.getElementById("usd-action");

      if (tendencia === "ALTA") setTag(usdTrendEl, "ALTA", "up");
      else if (tendencia === "BAIXA") setTag(usdTrendEl, "BAIXA", "down");
      else setTag(usdTrendEl, "NEUTRO", "neutral");

      usdActionEl.textContent = acao;

      renderTabelaAtivos();
    }

    function atualizarPainelMinerio(variacaoDecimal, precoUltimo) {
      const priceEl = document.getElementById("iron-price");
      const chgEl = document.getElementById("iron-change");
      const classEl = document.getElementById("iron-class");

      if (precoUltimo != null && !isNaN(precoUltimo)) {
        priceEl.textContent = precoUltimo.toFixed(4);
      } else {
        priceEl.textContent = "--";
      }

      if (variacaoDecimal == null || isNaN(variacaoDecimal)) {
        chgEl.textContent = "--";
        setTag(classEl, "--", "neutral");
        return;
      }

      const pct = variacaoDecimal * 100;
      chgEl.textContent = pct.toFixed(2) + " %";

      // Atualiza ativo de minério
      const minerio = ativos.find(a => a.codigo === "MINERIO_SINA");
      if (minerio) minerio.variacao = variacaoDecimal;

      const status = classificarAtivo(
        variacaoDecimal,
        LIMITE_MINERIO_ALTA,
        LIMITE_MINERIO_QUEDA
      );
      if (status === "ALTA") setTag(classEl, "ALTA", "up");
      else if (status === "QUEDA") setTag(classEl, "QUEDA", "down");
      else setTag(classEl, "NEUTRO", "neutral");

      atualizarPainel();
    }

    // ========= 4) INICIALIZAÇÃO E EVENTOS =========

    document.addEventListener("DOMContentLoaded", () => {
      // Botão filtro de notícias
      document
        .getElementById("btn-update-news")
        .addEventListener("click", atualizarResumoNews);

      // Botão aplicar minério
      document
        .getElementById("btn-apply-iron")
        .addEventListener("click", () => {
          const variacaoStr = document.getElementById("iron-manual").value;
          const precoStr = document.getElementById("iron-price-manual").value;
          const variacaoPct = parseFloat(String(variacaoStr).replace(",", "."));
          const preco = parseFloat(String(precoStr).replace(",", "."));

          if (isNaN(variacaoPct)) {
            alert("Informe uma variação do minério em % válida (ex.: 3.5).");
            return;
          }
          const variacaoDecimal = variacaoPct / 100.0;
          atualizarPainelMinerio(variacaoDecimal, isNaN(preco) ? null : preco);
        });

      // Botão aplicar variação de ativo
      document
        .getElementById("btn-apply-ativo")
        .addEventListener("click", () => {
          const cod = document.getElementById("ativo-codigo").value.trim();
          const varStr = document.getElementById("ativo-var").value;
          if (!cod) {
            alert("Informe o código do ativo (ex.: EWZ, DX, USD/MXN...).");
            return;
          }
          const ativo = ativos.find(a => a.codigo.toUpperCase() === cod.toUpperCase());
          if (!ativo) {
            alert("Ativo não encontrado na lista interna. Ajuste o código ou adicione o ativo no código.");
            return;
          }
          const pct = parseFloat(String(varStr).replace(",", "."));
          if (isNaN(pct)) {
            alert("Informe uma variação em % válida.");
            return;
          }
          ativo.variacao = pct / 100.0;
          atualizarPainel();
        });

      // Inicial
      atualizarResumoNews();
      atualizarPainel();
    });
  </script>
</body>
</html>
