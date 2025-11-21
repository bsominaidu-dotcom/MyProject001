<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Rewards & Recognition — Submit & My Submissions (Fluent UI)</title>

<style>
  /* ---------- Fluent-like theme variables ---------- */
  :root{
    --bg:#f3f6fb;
    --surface:#ffffff;
    --muted:#6b7280;
    --accent:#0078d4;         /* Fluent blue */
    --accent-600:#006bb3;
    --success:#107c10;
    --danger:#d13438;
    --emailBlue:#0b5fa5;
    --radius:12px;
    --card-padding:18px;
    --shadow: 0 6px 18px rgba(15,23,42,0.06);
    --glass: linear-gradient(180deg, rgba(255,255,255,0.6), rgba(255,255,255,0.5));
    font-family: "Segoe UI", system-ui, -apple-system, "Helvetica Neue", Arial;
  }

  /* ---------- Base layout ---------- */
  html,body{height:100%; margin:0; background:var(--bg); color:#111; -webkit-font-smoothing:antialiased;}
  .app { max-width:1100px; margin:28px auto; padding:16px; }
  header { display:flex; align-items:center; justify-content:space-between; gap:12px; margin-bottom:18px; }
  h1 { margin:0; color:var(--accent); font-size:20px; letter-spacing:0.2px; }
  .subtitle{ color:var(--muted); font-size:13px; }

  /* ---------- Tabs ---------- */
  .tabs { display:flex; gap:8px; margin-bottom:18px; }
  .tab {
    background:transparent; border:none; padding:10px 16px; border-radius:8px; cursor:pointer; font-weight:700; color:#334155;
    transition:all .18s ease;
  }
  .tab:hover{ background:rgba(0,0,0,0.03); transform:translateY(-1px); }
  .tab.active{ background:var(--surface); box-shadow:var(--shadow); color:var(--accent); border:1px solid rgba(0,0,0,0.04) }

  /* ---------- Card ---------- */
  .card { background:var(--surface); border-radius:var(--radius); padding:var(--card-padding); box-shadow:var(--shadow); margin-bottom:20px; }

  /* ---------- Form grid ---------- */
  .grid { display:grid; grid-template-columns: 1fr 1fr; gap:14px; align-items:start; }
  .full { grid-column: 1 / -1; }
  label { display:block; font-size:13px; color:#0f172a; margin-bottom:6px; font-weight:600; }
  input[type="text"], input[type="date"], select, textarea {
    width:100%; padding:10px 12px; border-radius:8px; border:1px solid #e6eef8; background:white; font-size:14px;
    box-sizing:border-box; color:#0f172a;
  }
  textarea { min-height:100px; resize:vertical; }
  .hint { font-size:12px; color:var(--muted); margin-top:6px; }

  /* ---------- Section separator ---------- */
  .sep { margin:20px 0 8px 0; display:flex; align-items:center; gap:12px; }
  .sep hr { flex:1; border:none; height:1px; background:linear-gradient(90deg,#e6eef8,#f1f5f9); border-radius:2px; }
  .sep .sep-title { font-weight:700; color:#0f172a; font-size:14px; }

  /* ---------- Attachment area (UI only) ---------- */
  .upload {
    border:1px dashed #dbeafe; background:linear-gradient(180deg,#fbfdff,#ffffff); padding:14px; border-radius:10px; text-align:center; color:var(--muted);
  }
  .upload input { display:block; margin:8px auto 0 auto; }

  /* ---------- Buttons ---------- */
  .btn { border: none; padding:10px 14px; border-radius:8px; cursor:pointer; font-weight:700; font-size:14px; }
  .btn.primary { background:var(--accent); color:white; box-shadow: 0 6px 18px rgba(3,105,170,0.12); }
  .btn.secondary { background: #fff; border:1px solid #e6eef8; color:#0f172a; }
  .btn.ghost { background:transparent; color:var(--muted); border:1px solid transparent; }
  .btn.small { padding:6px 8px; font-size:13px; border-radius:6px; }

  /* accent action buttons */
  .btn.approve { background:var(--success); color:white; }
  .btn.reject { background:var(--danger); color:white; }

  /* disabled */
  .btn[disabled], .btn.disabled { opacity:0.5; cursor:not-allowed; }

  /* ---------- Table ---------- */
  .table-wrap { overflow:auto; border-radius:10px; border:1px solid #eef3fb; margin-top:12px; }
  table { width:100%; border-collapse:collapse; min-width:800px; }
  th, td { padding:12px 14px; border-bottom:1px solid #f1f5f9; text-align:left; font-size:14px; color:#0f172a; }
  th { background:#fbfdff; color:#334155; font-weight:700; position:sticky; top:0; }
  tr:hover td { background:linear-gradient(90deg,#fbfdff,#f7fbff); }

  /* status badges */
  .badge { display:inline-block; padding:6px 10px; border-radius:999px; font-weight:700; font-size:12px; }
  .badge.submitted { background:#fff7ed; color:#b45309; }
  .badge.under { background:#ecfbf1; color:#0f7a24; }
  .badge.approved { background:#eef8ff; color:var(--accent); }
  .badge.rejected { background:#fff1f0; color:#b91c1c; }
  .badge.email { background:var(--email-sent); color:var(--emailBlue); border:1px solid #d6e9fb; }

  /* small meta */
  .meta { font-size:13px; color:var(--muted); }

  /* responsive */
  @media (max-width:880px){
    .grid { grid-template-columns: 1fr; }
    table { font-size:13px; }
    .tabs { flex-wrap:wrap; gap:6px; }
  }
</style>
</head>
<body>
  <div class="app">
    <header>
      <div>
        <h1>Rewards & Recognition</h1>
        <div class="subtitle">Submit nominations and track your submissions — Fluent UI style</div>
      </div>
      <div class="meta">Demo • UI-only attachments • In-memory data</div>
    </header>

    <!-- Tabs -->
    <div class="tabs" role="tablist" aria-label="Main Tabs">
      <button class="tab active" role="tab" onclick="openTab('submit')">Submit Nomination</button>
      <button class="tab" role="tab" onclick="openTab('my')">My Submissions</button>
    </div>

    <!-- Submit Nomination (default) -->
    <section id="panel-submit" class="card" aria-labelledby="submit-tab">
      <h2 style="margin-top:0;color:var(--accent)">Submit Nomination</h2>

      <div class="grid" aria-hidden="false">
        <div>
          <label>Employee ID</label>
          <input id="empId" type="text" placeholder="e.g. E12345" />
        </div>
        <div>
          <label>Employee Name</label>
          <input id="empName" type="text" placeholder="Full name" />
        </div>

        <div>
          <label>Location</label>
          <input id="location" type="text" placeholder="City / Office" />
        </div>
        <div>
          <label>Function / Department</label>
          <input id="department" type="text" placeholder="e.g. Finance" />
        </div>

        <div>
          <label>Bonus Program</label>
          <input id="bonusProgram" type="text" placeholder="e.g. Spot Bonus" />
        </div>
        <div>
          <label>Time Period</label>
          <select id="timePeriod">
            <option>Monthly</option><option>Quarterly</option><option>Annually</option>
          </select>
        </div>

        <div>
          <label>Submission Date</label>
          <input id="submissionDate" type="date" />
        </div>
        <div>
          <label>Nominated By</label>
          <input id="nominatedBy" type="text" placeholder="Your name or email" />
        </div>
      </div>

      <div class="sep" role="separator" aria-hidden="true">
        <hr /><div class="sep-title">Reason for Request / Business Justification</div><hr />
      </div>

      <div class="grid">
        <div class="full">
          <label>Relevance</label>
          <textarea id="relevance" placeholder="The overall significance of the accomplishments are in line with goals and objectives of BU"></textarea>
          <div class="hint">The overall significance of the accomplishments are in line with goals and objectives of BU</div>
        </div>

        <div class="full">
          <label>Performance</label>
          <textarea id="performance" placeholder="The overall impact and benefit to Business Function"></textarea>
          <div class="hint">The overall impact and benefit to Business Function</div>
        </div>

        <div class="full">
          <label>Quality</label>
          <textarea id="quality" placeholder="Demonstrated sustainability and delivery of work with top notch quality"></textarea>
          <div class="hint">Demonstrated sustainability and delivery of work with top notch quality</div>
        </div>

        <div class="full">
          <label>Adherence to DN Values</label>
          <textarea id="values" placeholder="Explain how the nominee demonstrates DN Values"></textarea>
        </div>
      </div>

      <div style="margin-top:14px">
        <div class="upload">
          <div style="font-weight:600;color:#0f172a">Attachments</div>
          <div class="meta" style="margin-top:6px">Select files (UI-only). In production these should be uploaded to SharePoint attachments.</div>
          <input id="attachmentInput" type="file" multiple />
          <div id="attachmentPreview" class="meta" style="margin-top:8px"></div>
        </div>
      </div>

      <div style="margin-top:16px; display:flex; gap:10px; justify-content:flex-end;">
        <button class="btn secondary" onclick="clearSubmitForm()">Clear</button>
        <button class="btn primary" onclick="submitNomination()">Submit Nomination</button>
      </div>
    </section>

    <!-- My Submissions -->
    <section id="panel-my" class="card" style="display:none">
      <div style="display:flex; align-items:center; gap:14px; justify-content:space-between;">
        <div>
          <h2 style="margin:0;color:var(--accent)">My Submissions</h2>
          <div class="meta">Filter by Year, Month or Quarter — Email candidate when approved</div>
        </div>

        <div style="display:flex;gap:10px;align-items:center">
          <label class="meta" style="margin:0 6px 0 0">Year</label>
          <select id="myYearFilter" onchange="renderMySubmissions()"></select>

          <label class="meta" style="margin:0 6px 0 0">Period</label>
          <select id="myPeriodFilter" onchange="renderMySubmissions()">
            <option value="All">All</option><option>Monthly</option><option>Quarterly</option><option>Annually</option>
          </select>

          <button class="btn secondary" onclick="exportMyCSV()">Export</button>
        </div>
      </div>

      <div class="table-wrap">
        <table aria-describedby="mySubmissions">
          <thead>
            <tr>
              <th>Employee</th>
              <th>Bonus Program</th>
              <th>Period</th>
              <th>Status</th>
              <th>Submission Date</th>
              <th>Actions</th>
            </tr>
          </thead>
          <tbody id="myTableBody"></tbody>
        </table>
      </div>
    </section>

    <footer style="margin-top:18px" class="meta">Tip: This demo uses client-side data. Replace logic with PnPjs calls for SharePoint integration.</footer>
  </div>

<script>
/* -------------------------
  In-memory demo dataset
  Replace with SharePoint integration (PnPjs) in production
---------------------------*/
const todayISO = new Date().toISOString().slice(0,10);
let submissions = [
  { id:1, empId:'E100', empName:'John Doe', location:'Bengaluru', department:'Finance', bonus:'Spot Bonus', period:'Monthly', submissionDate:'2025-01-20', nominatedBy:'manager@contoso.com', status:'Approved', emailSent:false },
  { id:2, empId:'E101', empName:'Alex Smith', location:'Hyderabad', department:'IT', bonus:'Quarterly Excellence', period:'Quarterly', submissionDate:'2025-02-10', nominatedBy:'peer@contoso.com', status:'Submitted', emailSent:false },
  { id:3, empId:'E102', empName:'Chitra Rao', location:'Mumbai', department:'HR', bonus:'Annual Merit', period:'Annually', submissionDate:'2024-11-15', nominatedBy:'lead@contoso.com', status:'Email Sent to Nominee', emailSent:true }
];

/* -------------------------
  UI helpers & initial setup
---------------------------*/
document.getElementById('submissionDate').value = todayISO;
document.getElementById('attachmentInput').addEventListener('change', e=>{
  const names = [...e.target.files].map(f=>f.name).join(', ');
  document.getElementById('attachmentPreview').textContent = names ? `Selected: ${names}` : '';
});

/* Populate year filter from dataset */
function getYears(){
  const set = new Set(submissions.map(s => {
    const y = new Date(s.submissionDate).getFullYear();
    return isNaN(y) ? null : y;
  }).filter(Boolean));
  return Array.from(set).sort((a,b)=>b-a);
}
function populateYearFilter(){
  const years = getYears();
  const el = document.getElementById('myYearFilter');
  el.innerHTML = '<option value="All">All Submissions</option>' + years.map(y=>`<option value="${y}">${y}</option>`).join('');
}
populateYearFilter();

/* Tabs */
function openTab(tab){
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  const btns = document.querySelectorAll('.tab');
  for(const b of btns){ if(b.textContent.trim().startsWith(tab==='submit' ? 'Submit' : 'My')) { b.classList.add('active'); break; } }
  document.getElementById('panel-submit').style.display = tab==='submit' ? '' : 'none';
  document.getElementById('panel-my').style.display = tab==='my' ? '' : 'none';
  if(tab==='my'){ populateYearFilter(); renderMySubmissions(); }
}

/* Format badge */
function statusBadge(s){
  if(s === 'Approved') return `<span class="badge approved">Approved</span>`;
  if(s === 'Under Review') return `<span class="badge under">Under Review</span>`;
  if(s === 'Rejected') return `<span class="badge rejected">Rejected</span>`;
  if(s === 'Email Sent to Nominee') return `<span class="badge email">Email Sent to Nominee</span>`;
  return `<span class="badge submitted">Submitted</span>`;
}

/* Render My Submissions table with filters */
function renderMySubmissions(){
  const year = document.getElementById('myYearFilter').value;
  const period = document.getElementById('myPeriodFilter').value;
  const tbody = document.getElementById('myTableBody');
  tbody.innerHTML = '';

  submissions.forEach((s, idx)=>{
    // Only show submissions where nominatedBy equals current user? 
    // This demo shows all; if you want only 'my' submissions, compare nominatedBy to logged user.
    // For demo keep all visible. To filter by current user, uncomment next line:
    // if(s.nominatedBy !== 'currentUser@contoso.com') return;

    if(year !== 'All'){
      const y = new Date(s.submissionDate).getFullYear();
      if(String(y) !== String(year)) return;
    }
    if(period !== 'All'){
      if(s.period !== period) return;
    }

    const emailDisabled = s.emailSent === true || s.status === 'Email Sent to Nominee';
    const canEmail = s.status === 'Approved' && !emailDisabled;
    const editBtn = `<button class="btn small" onclick="editSubmission(${s.id})">Edit</button>`;
    const emailBtn = `<button class="btn small ${canEmail ? '' : 'disabled'}" ${canEmail ? `onclick="sendEmail(${s.id})"` : 'disabled'}>${ emailDisabled ? 'Email Sent' : 'Email'}</button>`;

    const actions = s.status === 'Approved' ? `${editBtn} ${emailBtn}` : `${editBtn}`;

    const row = document.createElement('tr');
    row.innerHTML = `
      <td>${escapeHtml(s.empName)} <div class="meta" style="font-weight:600">${escapeHtml(s.empId)}</div><div class="meta">${escapeHtml(s.location)}</div></td>
      <td>${escapeHtml(s.bonus)}</td>
      <td>${escapeHtml(s.period)}</td>
      <td>${statusBadge(s.status)}</td>
      <td>${escapeHtml(s.submissionDate)}</td>
      <td>${actions}</td>
    `;
    tbody.appendChild(row);
  });
}

/* Send Email (updates status and disables email button) */
function sendEmail(id){
  // find item
  const i = submissions.find(x=>x.id===id);
  if(!i) return alert('Item not found');
  // In production: open email preview modal and call Power Automate or Graph to send real email
  // For demo: directly update status
  i.status = 'Email Sent to Nominee';
  i.emailSent = true;
  populateYearFilter();
  renderMySubmissions();
  alert('Demo: Email sent and status updated to "Email Sent to Nominee".');
}

/* Edit (simple prompt demo) */
function editSubmission(id){
  const i = submissions.find(x=>x.id===id);
  if(!i) return alert('Not found');
  // Simple inline prompt demo (replace with modal form if preferred)
  const newName = prompt('Edit Employee Name', i.empName);
  if(newName !== null){ i.empName = newName.trim() || i.empName; renderMySubmissions(); }
}

/* Submit nomination from form */
function submitNomination(){
  const empId = document.getElementById('empId').value.trim();
  const empName = document.getElementById('empName').value.trim();
  const location = document.getElementById('location').value.trim();
  const department = document.getElementById('department').value.trim();
  const bonus = document.getElementById('bonusProgram').value.trim();
  const period = document.getElementById('timePeriod').value;
  const submissionDate = document.getElementById('submissionDate').value || todayISO;
  const nominatedBy = document.getElementById('nominatedBy').value.trim() || 'you@contoso.com';
  // validation
  if(!empName || !bonus){
    alert('Please enter Employee Name and Bonus Program.');
    return;
  }
  const newItem = {
    id: submissions.length ? Math.max(...submissions.map(s=>s.id))+1 : 1,
    empId, empName, location, department, bonus, period,
    submissionDate, nominatedBy, status:'Submitted', emailSent:false
  };
  submissions.push(newItem);
  populateYearFilter();
  renderMySubmissions();
  document.getElementById('attachmentInput').value='';
  document.getElementById('attachmentPreview').textContent='';
  alert('Nomination submitted (demo). In production it will save to SharePoint.');
}

/* Clear form */
function clearSubmitForm(){
  ['empId','empName','location','department','bonusProgram','timePeriod','submissionDate','nominatedBy','relevance','performance','quality','values'].forEach(id=>{
    const el = document.getElementById(id);
    if(el) el.value = '';
  });
  document.getElementById('submissionDate').value = todayISO;
  document.getElementById('attachmentInput').value = '';
  document.getElementById('attachmentPreview').textContent = '';
}

/* Export My Submissions filtered to CSV */
function exportMyCSV(){
  const year = document.getElementById('myYearFilter').value;
  const period = document.getElementById('myPeriodFilter').value;
  const rows = submissions.filter(s=>{
    if(year !== 'All'){ if(String(new Date(s.submissionDate).getFullYear()) !== String(year)) return false; }
    if(period !== 'All'){ if(s.period !== period) return false; }
    return true;
  }).map(s => ({
    EmployeeID: s.empId, EmployeeName: s.empName, Location: s.location, Department: s.department,
    BonusProgram: s.bonus, Period: s.period, Status: s.status, SubmissionDate: s.submissionDate
  }));
  if(!rows.length){ alert('No data to export'); return; }
  const header = Object.keys(rows[0]).join(',') + '\n';
  const csv = rows.map(r => Object.values(r).map(v=>`"${String(v||'').replace(/"/g,'""')}"`).join(',')).join('\n');
  const blob = new Blob([header + csv], { type: 'text/csv;charset=utf-8;' });
  const filename = `Nominations_MySubmissions_${new Date().toISOString().slice(0,10)}.csv`;
  const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = filename; a.style.display='none'; document.body.appendChild(a); a.click(); a.remove();
}

/* Utility */
function escapeHtml(s){ return (s||'').toString().replace(/[&<>"']/g, m => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[m])); }

/* Initialize */
populateYearFilter();
renderMySubmissions();

</script>
</body>
</html>
