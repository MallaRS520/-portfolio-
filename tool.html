<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>CSV Anomaly Detector — Single File</title>
  <style>
    :root{
      --bg:#f7fafc;
      --card:#ffffff;
      --muted:#6b7280;
      --accent:#2563eb;
      --danger:#ef4444;
      --radius:10px;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      background: linear-gradient(180deg,#eef2ff 0%, #f7fafc 100%);
      color:#111827;
      padding:20px;
      -webkit-font-smoothing:antialiased;
    }
    main{max-width:1100px;margin:0 auto;display:grid;gap:16px}
    header{text-align:center;margin-bottom:6px}
    h1{margin:0;font-size:1.5rem}
    p.lead{margin:6px 0;color:var(--muted)}

    .card{background:var(--card);padding:12px;border-radius:var(--radius);box-shadow:0 6px 18px rgba(16,24,40,0.06)}
    .controls{display:flex;gap:12px;flex-wrap:wrap;align-items:center}
    .file-label{border:2px dashed #e6eefc;padding:8px 12px;border-radius:8px;cursor:pointer;display:inline-block;color:var(--muted)}
    .file-label input{display:none}
    .options{display:flex;gap:10px;align-items:center;margin-left:auto;flex-wrap:wrap}
    label{font-size:0.95rem;color:var(--muted)}
    input[type="number"]{width:90px;padding:4px 6px;margin-left:6px;border-radius:6px;border:1px solid #e5e7eb}
    select{padding:6px;border-radius:6px;border:1px solid #e5e7eb}
    .btn{background:var(--accent);color:white;border:none;padding:8px 12px;border-radius:8px;cursor:pointer}
    .btn.secondary{background:#6b7280}
    .btn:disabled{opacity:0.5;cursor:not-allowed}

    .summary{color:var(--muted)}
    .tables{display:grid;grid-template-columns:1fr 1fr;gap:12px}
    .table-wrap{background:var(--card);padding:12px;border-radius:10px}
    .table-container{max-height:360px;overflow:auto;border-radius:8px;border:1px solid #f3f4f6;padding:8px;background:linear-gradient(180deg, rgba(255,255,255,0.6), transparent)}
    table{border-collapse:collapse;width:100%}
    th,td{padding:6px 8px;border-bottom:1px solid #f3f4f6;font-size:0.9rem}
    th{position:sticky;top:0;background:#fff;font-weight:600}
    tr.anom td{background: rgba(239,68,68,0.06)}
    pre.sample{background:#111827;color:#f8fafc;padding:12px;border-radius:8px;overflow:auto;color: #e6eefc}

    .small{font-size:0.85rem;color:var(--muted)}
    footer{text-align:center;color:var(--muted);margin-top:8px;font-size:0.85rem}

    @media (max-width:900px){
      .tables{grid-template-columns:1fr}
      .options{width:100%;justify-content:space-between}
    }
  </style>
</head>
<body>
  <main>
    <header>
      <h1>CSV Anomaly Detector (single file)</h1>
      <p class="lead">Upload a CSV, detect numeric outliers (Z-score or IQR), view and download anomalous rows — runs entirely in your browser.</p>
    </header>

    <section class="card controls" aria-label="controls">
      <label class="file-label" title="Choose CSV">
        Choose CSV
        <input id="csvFile" type="file" accept=".csv,text/csv" />
      </label>

      <div class="options">
        <label>
          Method:
          <select id="method">
            <option value="zscore">Z-score (|Z| &gt; threshold)</option>
            <option value="iqr">IQR (outside Q1 - k*IQR / Q3 + k*IQR)</option>
          </select>
        </label>

        <label id="zLabel">
          Z threshold:
          <input id="zThreshold" type="number" value="3" step="0.1" min="0.1" />
        </label>

        <label id="iqrLabel" style="display:none">
          IQR k:
          <input id="iqrK" type="number" value="1.5" step="0.1" min="0.1" />
        </label>

        <button id="runBtn" class="btn">Detect Anomalies</button>
        <button id="downloadBtn" class="btn" disabled>Download Anomalies (CSV)</button>
      </div>
    </section>

    <section class="card summary" id="summary">
      <div id="summaryText">No data loaded.</div>
    </section>

    <section class="tables" aria-label="results">
      <div class="table-wrap">
        <h2>Anomalous Rows</h2>
        <div id="anomalyContainer" class="table-container">—</div>
      </div>

      <div class="table-wrap">
        <h2>Normal Rows</h2>
        <div id="normalContainer" class="table-container">—</div>
      </div>
    </section>

    <section class="card">
      <h3>Quick sample CSV</h3>
      <p class="small">Copy-paste into a file or click the button to load into the app (first row must be headers):</p>
      <pre class="sample" id="sampleCSV">id,temp,pressure,notes
1,22.5,101.3,ok
2,23.1,101.2,ok
3,21.9,101.4,ok
4,85.0,99.1,possible-sensor-error
5,22.8,101.3,ok
6,23.0,101.5,ok
7,23.2,101.2,ok
8,19.3,130.0,spike
9,22.7,101.3,ok
10,22.6,101.4,ok</pre>
      <div style="margin-top:8px">
        <button id="loadSample" class="btn secondary">Load sample CSV into app</button>
      </div>
      <p class="small" style="margin-top:8px">Notes: Numeric columns auto-detected. A row is flagged anomalous if <em>any</em> numeric field is an outlier under the chosen method.</p>
    </section>

    <section class="card small">
      <strong>How it works (short):</strong>
      <ul>
        <li><strong>CSV parsing:</strong> built-in parser supports quoted fields and commas inside quotes.</li>
        <li><strong>Numeric detection:</strong> a column is numeric if the majority of its non-empty values parse to finite numbers.</li>
        <li><strong>Z-score method:</strong> compute mean &amp; standard deviation; value is anomalous if |(x - mean) / std| &gt; threshold.</li>
        <li><strong>IQR method:</strong> compute Q1, Q3, IQR = Q3 - Q1; anomalous if x &lt; Q1 - k*IQR or x &gt; Q3 + k*IQR.</li>
      </ul>
    </section>

    <footer>Open <strong>index.html</strong> in your browser — no server required.</footer>
  </main>

  <script>
  // ---------------------------
  // CSV Anomaly Detector (single file)
  // ---------------------------
  // Main features:
  // - Parse CSV in browser (handles quoted fields)
  // - Auto-detect numeric columns
  // - Detect outliers per numeric column using Z-score or IQR
  // - Mark a row anomalous if any numeric field is anomalous
  // - Show normal and anomalous rows in tables
  // - Allow downloading anomalies as CSV
  //
  // Algorithm details are in the UI notes and comments below.

  // Utility: parse CSV text into array of rows (each row is array of strings)
  // Supports quoted fields, escaped quotes, and newlines inside quotes.
  function parseCSV(text) {
    const rows = [];
    let cur = '';
    let row = [];
    let inQuotes = false;
    for (let i = 0; i < text.length; i++) {
      const ch = text[i];
      const next = text[i+1];
      if (ch === '"' ) {
        if (inQuotes && next === '"') { // escaped quote
          cur += '"';
          i++; // skip next quote
        } else {
          inQuotes = !inQuotes;
        }
      } else if (ch === ',' && !inQuotes) {
        row.push(cur);
        cur = '';
      } else if ((ch === '\n' || ch === '\r') && !inQuotes) {
        // handle CRLF and LF
        if (ch === '\r' && next === '\n') { /* skip, will handle both */ }
        // Only push row if not a completely empty final newline
        if (cur !== '' || row.length > 0) {
          row.push(cur);
          rows.push(row);
          row = [];
          cur = '';
        }
      } else {
        cur += ch;
      }
    }
    // push last
    if (cur !== '' || row.length > 0) {
      row.push(cur);
      rows.push(row);
    }
    // Trim optional whitespace from each cell (but preserve internal spaces)
    return rows.map(r => r.map(cell => cell.trim()));
  }

  // Convert rows (array of arrays) into array of objects using header row
  function rowsToObjects(rows) {
    if (!rows || rows.length === 0) return [];
    const header = rows[0];
    const objs = [];
    for (let i = 1; i < rows.length; i++) {
      const row = rows[i];
      // if row length differs, pad with empty strings
      const obj = {};
      for (let j = 0; j < header.length; j++) {
        obj[header[j] || (`col${j}`)] = row[j] === undefined ? '' : row[j];
      }
      objs.push(obj);
    }
    return { header, data: objs };
  }

  // Helper numeric checks
  function toNumber(v) {
    if (v === null || v === undefined) return NaN;
    // Allow commas in numbers like "1,234.5"
    const cleaned = String(v).replace(/,/g, '');
    const n = parseFloat(cleaned);
    return Number.isFinite(n) ? n : NaN;
  }

  // Determine numeric columns: column is numeric if majority of non-empty values are numeric
  function detectNumericColumns(header, data) {
    const numeric = {};
    for (const h of header) {
      let numericCount = 0, nonEmptyCount = 0;
      for (const row of data) {
        const v = row[h];
        if (v !== '' && v !== null && v !== undefined) {
          nonEmptyCount++;
          if (!Number.isNaN(toNumber(v))) numericCount++;
        }
      }
      numeric[h] = nonEmptyCount === 0 ? false : (numericCount / nonEmptyCount) >= 0.6; // >=60% numeric => numeric column
    }
    return numeric;
  }

  // Stats helpers
  function mean(arr) { return arr.reduce((a,b)=>a+b,0)/arr.length; }
  function stddev(arr, usePopulation=false) {
    if (arr.length === 0) return NaN;
    const m = mean(arr);
    const ss = arr.reduce((s,x)=>s + (x - m)*(x - m), 0);
    return Math.sqrt(ss / (usePopulation ? arr.length : Math.max(1, arr.length - 1)));
  }
  function quantile(arrSorted, q) {
    const n = arrSorted.length;
    if (n === 0) return NaN;
    const pos = (n - 1) * q;
    const lower = Math.floor(pos);
    const upper = Math.ceil(pos);
    if (lower === upper) return arrSorted[lower];
    return arrSorted[lower] * (upper - pos) + arrSorted[upper] * (pos - lower);
  }

  // Main anomaly detection factories
  function computeZScoreRules(header, data, numericCols, zThreshold=3) {
    const rules = {}; // {col: {mean, std, threshold}}
    for (const h of header) {
      if (!numericCols[h]) continue;
      const nums = data.map(r => toNumber(r[h])).filter(n => !Number.isNaN(n));
      if (nums.length < 2) continue;
      const m = mean(nums);
      const s = stddev(nums); // sample stddev
      rules[h] = { mean: m, std: s || 1e-9, threshold: zThreshold };
    }
    return rules;
  }
  function computeIQRRules(header, data, numericCols, k=1.5) {
    const rules = {}; // {col: {q1,q3,iqr,k}}
    for (const h of header) {
      if (!numericCols[h]) continue;
      const nums = data.map(r => toNumber(r[h])).filter(n => !Number.isNaN(n)).sort((a,b)=>a-b);
      if (nums.length === 0) continue;
      const q1 = quantile(nums, 0.25);
      const q3 = quantile(nums, 0.75);
      const iqr = q3 - q1;
      rules[h] = { q1, q3, iqr, k };
    }
    return rules;
  }

  // Evaluate a row against the rules: returns {isAnomaly:bool, details:[{col, value, reason}]}
  function evaluateRow(rowObj, zRules, iqrRules, method) {
    const details = [];
    if (method === 'zscore') {
      for (const col in zRules) {
        const v = toNumber(rowObj[col]);
        if (Number.isNaN(v)) continue;
        const { mean, std, threshold } = zRules[col];
        const z = Math.abs((v - mean) / (std || 1e-9));
        if (z > threshold) {
          details.push({ col, value: rowObj[col], reason: `z=${z.toFixed(3)} > ${threshold}` });
        }
      }
    } else {
      for (const col in iqrRules) {
        const v = toNumber(rowObj[col]);
        if (Number.isNaN(v)) continue;
        const { q1, q3, iqr, k } = iqrRules[col];
        if (iqr === 0) continue; // no spread
        if (v < q1 - k * iqr || v > q3 + k * iqr) {
          details.push({ col, value: rowObj[col], reason: `value ${v} outside [${(q1 - k*iqr).toFixed(3)}, ${(q3 + k*iqr).toFixed(3)}]` });
        }
      }
    }
    return { isAnomaly: details.length > 0, details };
  }

  // Render helpers: build table HTML from header + array of objects
  function buildTableHTML(header, rows, highlight=false, maxRows=500) {
    if (!rows || rows.length === 0) return '<div class="small">No rows</div>';
    const h = header.map(h => `<th>${escapeHtml(h)}</th>`).join('');
    const rowsToShow = rows.slice(0, maxRows);
    const body = rowsToShow.map(r => {
      const tds = header.map(c => `<td>${escapeHtml(String(r[c]===undefined?'':r[c]))}</td>`).join('');
      return `<tr ${highlight ? 'class="anom"' : ''}>${tds}</tr>`;
    }).join('');
    const more = rows.length > maxRows ? `<div class="small">Showing ${maxRows} of ${rows.length} rows</div>` : '';
    return `<table><thead><tr>${h}</tr></thead><tbody>${body}</tbody></table>${more}`;
  }

  function escapeHtml(s){ return s.replaceAll('&','&amp;').replaceAll('<','&lt;').replaceAll('>','&gt;'); }

  // Download CSV from array of objects; header array is provided
  function downloadCSV(filename, header, rows) {
    const lines = [];
    // escape fields with quotes if necessary
    const esc = (v) => {
      if (v === null || v === undefined) return '';
      const s = String(v);
      // if contains comma, quote or newline, wrap in quotes and escape existing quotes
      if (s.includes(',') || s.includes('"') || s.includes('\n') || s.includes('\r')) {
        return '"' + s.replaceAll('"', '""') + '"';
      }
      return s;
    };
    lines.push(header.map(esc).join(','));
    for (const r of rows) {
      lines.push(header.map(h => esc(r[h])).join(','));
    }
    const blob = new Blob([lines.join('\r\n')], { type: 'text/csv;charset=utf-8;' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = filename;
    document.body.appendChild(a);
    a.click();
    a.remove();
    URL.revokeObjectURL(url);
  }

  // MAIN UI wiring
  const fileInput = document.getElementById('csvFile');
  const methodSelect = document.getElementById('method');
  const zThresholdInput = document.getElementById('zThreshold');
  const iqrKInput = document.getElementById('iqrK');
  const runBtn = document.getElementById('runBtn');
  const downloadBtn = document.getElementById('downloadBtn');
  const anomalyContainer = document.getElementById('anomalyContainer');
  const normalContainer = document.getElementById('normalContainer');
  const summaryText = document.getElementById('summaryText');
  const zLabel = document.getElementById('zLabel');
  const iqrLabel = document.getElementById('iqrLabel');
  const loadSampleBtn = document.getElementById('loadSample');
  const sampleCSV = document.getElementById('sampleCSV').textContent.trim();

  let currentHeader = null;
  let currentData = null;
  let currentAnomalies = [];
  let currentNormals = [];

  // Toggle option inputs when method changes
  methodSelect.addEventListener('change', () => {
    if (methodSelect.value === 'zscore') {
      zLabel.style.display = '';
      iqrLabel.style.display = 'none';
    } else {
      zLabel.style.display = 'none';
      iqrLabel.style.display = '';
    }
  });

  // Load sample CSV into memory (simulate file input)
  loadSampleBtn.addEventListener('click', () => {
    processCSVText(sampleCSV);
  });

  // When a file is selected, read it
  fileInput.addEventListener('change', (e) => {
    const file = e.target.files && e.target.files[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = () => {
      processCSVText(reader.result);
    };
    reader.onerror = () => {
      alert('Failed to read file');
    };
    reader.readAsText(file);
  });

  // Run detection when button clicked
  runBtn.addEventListener('click', () => {
    if (!currentHeader || !currentData) {
      alert('Please load a CSV first (choose file or use sample).');
      return;
    }
    detectAndRender();
  });

  downloadBtn.addEventListener('click', () => {
    if (!currentAnomalies || currentAnomalies.length === 0) return;
    downloadCSV('anomalies.csv', currentHeader, currentAnomalies);
  });

  // Process CSV text into header + data objects and update UI
  function processCSVText(text) {
    try {
      const rows = parseCSV(text);
      if (!rows || rows.length < 1) {
        summaryText.textContent = 'CSV appears empty or malformed.';
        return;
      }
      const { header, data } = rowsToObjects(rows);
      currentHeader = header;
      currentData = data;
      currentAnomalies = [];
      currentNormals = [];
      anomalyContainer.innerHTML = '<div class="small">Ready — click "Detect Anomalies".</div>';
      normalContainer.innerHTML = '<div class="small">Ready — click "Detect Anomalies".</div>';
      summaryText.innerHTML = `Loaded <strong>${data.length}</strong> rows and <strong>${header.length}</strong> columns. Numeric columns will be auto-detected.`;
      downloadBtn.disabled = true;
    } catch (err) {
      console.error(err);
      alert('Error parsing CSV: ' + err.message);
    }
  }

  // Main detection flow
  function detectAndRender() {
    const header = currentHeader;
    const data = currentData;
    const method = methodSelect.value;
    const zThreshold = parseFloat(zThresholdInput.value) || 3;
    const iqrK = parseFloat(iqrKInput.value) || 1.5;

    // 1) Detect numeric columns
    const numericCols = detectNumericColumns(header, data);
    const numericList = Object.keys(numericCols).filter(h => numericCols[h]);

    // 2) Build rules
    let zRules = {}, iqrRules = {};
    if (method === 'zscore') {
      zRules = computeZScoreRules(header, data, numericCols, zThreshold);
    } else {
      iqrRules = computeIQRRules(header, data, numericCols, iqrK);
    }

    // 3) Evaluate rows
    const anomalies = [];
    const normals = [];
    for (const row of data) {
      const evalResult = evaluateRow(row, zRules, iqrRules, method);
      if (evalResult.isAnomaly) {
        // add details for UI: we attach a __anomDetails property for display
        row.__anomDetails = evalResult.details;
        anomalies.push(row);
      } else {
        normals.push(row);
      }
    }

    currentAnomalies = anomalies;
    currentNormals = normals;

    // 4) Render
    anomalyContainer.innerHTML = buildAnomalyHTML(header, anomalies);
    normalContainer.innerHTML = buildTableHTML(header, normals, false);
    summaryText.innerHTML = `<strong>${anomalies.length}</strong> anomalous rows detected out of <strong>${data.length}</strong> rows. Numeric columns: <strong>${numericList.join(', ') || '—'}</strong>.`;
    downloadBtn.disabled = anomalies.length === 0;
  }

  // Build anomaly table with details column
  function buildAnomalyHTML(header, anomalies) {
    if (!anomalies || anomalies.length === 0) return '<div class="small">No anomalies found.</div>';
    // Add a details column
    const headerWithDetails = header.concat(['__anomaly_details']);
    const rows = anomalies.map(r => {
      const copy = Object.assign({}, r);
      copy['__anomaly_details'] = (r.__anomDetails || []).map(d => `${d.col}: ${d.reason}`).join('; ');
      return copy;
    });
    return buildTableHTML(headerWithDetails, rows, true, 1000);
  }

  // If user drags a file into the page, also support that
  document.addEventListener('dragover', e => e.preventDefault());
  document.addEventListener('drop', e => {
    e.preventDefault();
    const f = e.dataTransfer.files && e.dataTransfer.files[0];
    if (f && (f.type === 'text/csv' || f.name.toLowerCase().endsWith('.csv') || f.type === 'application/octet-stream')) {
      const r = new FileReader();
      r.onload = () => processCSVText(r.result);
      r.readAsText(f);
    }
  });

  // Optional: automatically load sample on first open for convenience
  // processCSVText(sampleCSV); // <-- uncomment if you want automatic load
  </script>
</body>
</html>
