Béatrix et Djaf 
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<meta name="theme-color" content="#2563eb">
<meta name="description" content="Campus Assistant - Assistant numérique pour étudiants">

<title>Campus Assistant</title>

<style>
/* =========================================================
   CAMPUS ASSISTANT
   VERSION MVP - SINGLE FILE
   HTML + CSS + JAVASCRIPT
   ========================================================= */

:root{
    --primary:#2563eb;
    --primary-dark:#1d4ed8;
    --secondary:#7c3aed;
    --success:#16a34a;
    --danger:#dc2626;
    --warning:#d97706;

    --bg:#f5f7fb;
    --card:#ffffff;
    --text:#111827;
    --muted:#6b7280;
    --border:#e5e7eb;

    --sidebar:#ffffff;
    --input:#f9fafb;

    --shadow:0 10px 30px rgba(15,23,42,.07);
    --radius:18px;
}

body.dark{
    --bg:#0f172a;
    --card:#111827;
    --text:#f9fafb;
    --muted:#9ca3af;
    --border:#263244;
    --sidebar:#111827;
    --input:#1f2937;
    --shadow:0 10px 30px rgba(0,0,0,.25);
}

*{
    box-sizing:border-box;
    margin:0;
    padding:0;
}

html{
    scroll-behavior:smooth;
}

body{
    font-family:
        Inter,
        system-ui,
        -apple-system,
        BlinkMacSystemFont,
        "Segoe UI",
        sans-serif;

    background:var(--bg);
    color:var(--text);
    min-height:100vh;
}

button,
input,
textarea,
select{
    font:inherit;
}

button{
    cursor:pointer;
}

a{
    color:inherit;
    text-decoration:none;
}

/* =========================================================
   LOADING
   ========================================================= */

#loadingScreen{
    position:fixed;
    inset:0;
    z-index:99999;
    background:var(--bg);
    display:flex;
    align-items:center;
    justify-content:center;
    flex-direction:column;
    gap:20px;
}

.loader{
    width:55px;
    height:55px;
    border:5px solid var(--border);
    border-top-color:var(--primary);
    border-radius:50%;
    animation:spin 1s linear infinite;
}

@keyframes spin{
    to{transform:rotate(360deg);}
}

/* =========================================================
   APP LAYOUT
   ========================================================= */

.app{
    display:flex;
    min-height:100vh;
}

.sidebar{
    width:270px;
    background:var(--sidebar);
    border-right:1px solid var(--border);
    position:fixed;
    left:0;
    top:0;
    bottom:0;
    z-index:1000;
    padding:22px 16px;
    display:flex;
    flex-direction:column;
    transition:.3s ease;
}

.logo{
    display:flex;
    align-items:center;
    gap:12px;
    padding:8px 10px 28px;
}

.logo-icon{
    width:46px;
    height:46px;
    border-radius:14px;
    background:linear-gradient(135deg,#2563eb,#7c3aed);
    color:white;
    display:flex;
    align-items:center;
    justify-content:center;
    font-size:24px;
    box-shadow:0 8px 20px rgba(37,99,235,.25);
}

.logo-text{
    font-size:20px;
    font-weight:800;
}

.logo-text span{
    color:var(--primary);
}

.nav{
    display:flex;
    flex-direction:column;
    gap:6px;
}

.nav button{
    border:0;
    background:transparent;
    color:var(--muted);
    padding:13px 14px;
    border-radius:12px;
    display:flex;
    align-items:center;
    gap:13px;
    text-align:left;
    width:100%;
    font-weight:600;
    transition:.2s;
}

.nav button:hover{
    background:var(--input);
    color:var(--text);
}

.nav button.active{
    background:rgba(37,99,235,.11);
    color:var(--primary);
}

.nav-icon{
    width:24px;
    text-align:center;
    font-size:19px;
}

.sidebar-bottom{
    margin-top:auto;
}

.profile-mini{
    border-top:1px solid var(--border);
    padding-top:16px;
    display:flex;
    align-items:center;
    gap:10px;
}

.avatar{
    width:42px;
    height:42px;
    border-radius:50%;
    background:linear-gradient(135deg,#2563eb,#7c3aed);
    color:white;
    display:flex;
    align-items:center;
    justify-content:center;
    font-weight:800;
}

.profile-info{
    overflow:hidden;
}

.profile-name{
    font-weight:700;
    white-space:nowrap;
    overflow:hidden;
    text-overflow:ellipsis;
}

.profile-role{
    color:var(--muted);
    font-size:12px;
}

/* =========================================================
   MAIN
   ========================================================= */

.main{
    margin-left:270px;
    width:calc(100% - 270px);
    min-height:100vh;
}

.topbar{
    height:76px;
    border-bottom:1px solid var(--border);
    background:var(--card);
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding:0 30px;
    position:sticky;
    top:0;
    z-index:500;
}

.mobile-menu{
    display:none;
    border:0;
    background:transparent;
    color:var(--text);
    font-size:25px;
}

.topbar-left{
    display:flex;
    align-items:center;
    gap:15px;
}

.page-title{
    font-size:22px;
    font-weight:800;
}

.search{
    width:260px;
    position:relative;
}

.search input{
    width:100%;
    border:1px solid var(--border);
    background:var(--input);
    color:var(--text);
    padding:11px 14px 11px 40px;
    border-radius:12px;
    outline:none;
}

.search-icon{
    position:absolute;
    left:14px;
    top:50%;
    transform:translateY(-50%);
}

.top-actions{
    display:flex;
    align-items:center;
    gap:10px;
}

.icon-btn{
    width:42px;
    height:42px;
    border:1px solid var(--border);
    border-radius:12px;
    background:var(--card);
    color:var(--text);
    position:relative;
}

.notification-dot{
    position:absolute;
    width:8px;
    height:8px;
    border-radius:50%;
    background:#ef4444;
    right:9px;
    top:8px;
}

.content{
    padding:30px;
    max-width:1500px;
    margin:auto;
}

.view{
    display:none;
}

.view.active{
    display:block;
}

/* =========================================================
   WELCOME
   ========================================================= */

.welcome{
    background:
        linear-gradient(135deg,rgba(37,99,235,.97),rgba(124,58,237,.97));
    color:white;
    border-radius:24px;
    padding:30px;
    display:flex;
    justify-content:space-between;
    align-items:center;
    gap:20px;
    margin-bottom:24px;
    overflow:hidden;
    position:relative;
}

.welcome::after{
    content:"";
    position:absolute;
    width:250px;
    height:250px;
    border-radius:50%;
    background:rgba(255,255,255,.08);
    right:-70px;
    top:-90px;
}

.welcome h1{
    font-size:30px;
    margin-bottom:8px;
}

.welcome p{
    opacity:.88;
}

.date-badge{
    background:rgba(255,255,255,.14);
    border:1px solid rgba(255,255,255,.2);
    padding:12px 16px;
    border-radius:14px;
    white-space:nowrap;
}

/* =========================================================
   CARDS
   ========================================================= */

.stats-grid{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:18px;
    margin-bottom:24px;
}

.stat-card{
    background:var(--card);
    border:1px solid var(--border);
    border-radius:var(--radius);
    padding:20px;
    box-shadow:var(--shadow);
}

.stat-top{
    display:flex;
    justify-content:space-between;
    align-items:center;
}

.stat-icon{
    width:45px;
    height:45px;
    border-radius:13px;
    display:flex;
    align-items:center;
    justify-content:center;
    background:rgba(37,99,235,.1);
    font-size:21px;
}

.stat-value{
    font-size:27px;
    font-weight:800;
    margin-top:14px;
}

.stat-label{
    color:var(--muted);
    margin-top:3px;
    font-size:14px;
}

/* =========================================================
   GRID
   ========================================================= */

.two-col{
    display:grid;
    grid-template-columns:1.5fr 1fr;
    gap:20px;
}

.card{
    background:var(--card);
    border:1px solid var(--border);
    border-radius:var(--radius);
    box-shadow:var(--shadow);
    padding:22px;
}

.card-header{
    display:flex;
    justify-content:space-between;
    align-items:center;
    gap:10px;
    margin-bottom:18px;
}

.card-title{
    font-size:18px;
    font-weight:800;
}

.card-subtitle{
    color:var(--muted);
    font-size:13px;
}

.primary-btn{
    border:0;
    background:var(--primary);
    color:white;
    padding:11px 16px;
    border-radius:11px;
    font-weight:700;
    transition:.2s;
}

.primary-btn:hover{
    background:var(--primary-dark);
    transform:translateY(-1px);
}

.secondary-btn{
    border:1px solid var(--border);
    background:var(--card);
    color:var(--text);
    padding:10px 14px;
    border-radius:11px;
    font-weight:600;
}

.danger-btn{
    border:0;
    background:#fee2e2;
    color:#b91c1c;
    padding:9px 12px;
    border-radius:9px;
}

body.dark .danger-btn{
    background:#3b1515;
    color:#fca5a5;
}

/* =========================================================
   TASKS
   ========================================================= */

.task{
    display:flex;
    align-items:center;
    gap:12px;
    padding:13px 0;
    border-bottom:1px solid var(--border);
}

.task:last-child{
    border-bottom:0;
}

.task-check{
    width:20px;
    height:20px;
    accent-color:var(--primary);
}

.task-main{
    flex:1;
}

.task-title{
    font-weight:650;
}

.task.completed .task-title{
    text-decoration:line-through;
    color:var(--muted);
}

.task-meta{
    font-size:12px;
    color:var(--muted);
    margin-top:3px;
}

.priority{
    padding:5px 8px;
    border-radius:7px;
    font-size:11px;
    font-weight:700;
}

.priority.high{
    background:#fee2e2;
    color:#b91c1c;
}

.priority.medium{
    background:#fef3c7;
    color:#92400e;
}

.priority.low{
    background:#dcfce7;
    color:#166534;
}

/* =========================================================
   SCHEDULE
   ========================================================= */

.schedule-item{
    display:flex;
    gap:14px;
    padding:13px 0;
    border-bottom:1px solid var(--border);
}

.schedule-time{
    width:70px;
    color:var(--primary);
    font-weight:800;
    font-size:13px;
}

.schedule-content{
    flex:1;
}

.schedule-name{
    font-weight:750;
}

.schedule-location{
    color:var(--muted);
    font-size:12px;
    margin-top:4px;
}

/* =========================================================
   PROGRESS
   ========================================================= */

.progress-container{
    margin:16px 0;
}

.progress-label{
    display:flex;
    justify-content:space-between;
    font-size:13px;
    margin-bottom:7px;
}

.progress{
    height:9px;
    border-radius:20px;
    background:var(--border);
    overflow:hidden;
}

.progress-bar{
    height:100%;
    border-radius:20px;
    background:linear-gradient(90deg,#2563eb,#7c3aed);
}

/* =========================================================
   TABLE
   ========================================================= */

.table-wrapper{
    overflow-x:auto;
}

table{
    width:100%;
    border-collapse:collapse;
}

th,
td{
    padding:13px 12px;
    border-bottom:1px solid var(--border);
    text-align:left;
    white-space:nowrap;
}

th{
    color:var(--muted);
    font-size:12px;
    text-transform:uppercase;
}

td{
    font-size:14px;
}

/* =========================================================
   FORMS
   ========================================================= */

.form-grid{
    display:grid;
    grid-template-columns:repeat(2,1fr);
    gap:15px;
}

.form-group{
    display:flex;
    flex-direction:column;
    gap:7px;
}

.form-group.full{
    grid-column:1/-1;
}

.form-group label{
    font-size:13px;
    font-weight:700;
}

.form-group input,
.form-group textarea,
.form-group select{
    width:100%;
    padding:12px;
    border:1px solid var(--border);
    border-radius:10px;
    background:var(--input);
    color:var(--text);
    outline:none;
}

.form-group textarea{
    min-height:120px;
    resize:vertical;
}

/* =========================================================
   NOTES
   ========================================================= */

.notes-grid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:18px;
}

.note-card{
    background:var(--card);
    border:1px solid var(--border);
    border-radius:16px;
    padding:18px;
    min-height:170px;
    box-shadow:var(--shadow);
}

.note-card h3{
    margin-bottom:9px;
}

.note-card p{
    color:var(--muted);
    font-size:14px;
    line-height:1.55;
}

.note-footer{
    margin-top:20px;
    display:flex;
    justify-content:space-between;
    align-items:center;
}

/* =========================================================
   RESOURCES
   ========================================================= */

.resource-grid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:18px;
}

.resource{
    border:1px solid var(--border);
    background:var(--card);
    border-radius:16px;
    padding:20px;
    transition:.2s;
}

.resource:hover{
    transform:translateY(-3px);
    box-shadow:var(--shadow);
}

.resource-icon{
    font-size:35px;
    margin-bottom:12px;
}

.resource h3{
    margin-bottom:6px;
}

.resource p{
    color:var(--muted);
    font-size:13px;
    line-height:1.5;
}

/* =========================================================
   AI ASSISTANT
   ========================================================= */

.ai-layout{
    display:grid;
    grid-template-columns:280px 1fr;
    gap:20px;
}

.ai-sidebar{
    background:var(--card);
    border:1px solid var(--border);
    border-radius:var(--radius);
    padding:20px;
    height:max-content;
}

.ai-avatar{
    width:65px;
    height:65px;
    border-radius:20px;
    background:linear-gradient(135deg,#2563eb,#7c3aed);
    color:white;
    display:flex;
    align-items:center;
    justify-content:center;
    font-size:30px;
    margin-bottom:15px;
}

.ai-sidebar h2{
    margin-bottom:7px;
}

.ai-sidebar p{
    color:var(--muted);
    font-size:13px;
    line-height:1.5;
}

.suggestion{
    width:100%;
    margin-top:10px;
    padding:11px;
    border:1px solid var(--border);
    background:var(--input);
    color:var(--text);
    border-radius:10px;
    text-align:left;
}

.chat{
    height:620px;
    background:var(--card);
    border:1px solid var(--border);
    border-radius:var(--radius);
    display:flex;
    flex-direction:column;
    overflow:hidden;
}

.chat-header{
    padding:18px;
    border-bottom:1px solid var(--border);
    display:flex;
    align-items:center;
    gap:12px;
}

.status-dot{
    width:10px;
    height:10px;
    border-radius:50%;
    background:#22c55e;
}

.messages{
    flex:1;
    overflow-y:auto;
    padding:22px;
    display:flex;
    flex-direction:column;
    gap:14px;
}

.message{
    max-width:78%;
    padding:12px 15px;
    border-radius:15px;
    line-height:1.5;
    font-size:14px;
}

.message.ai{
    align-self:flex-start;
    background:var(--input);
}

.message.user{
    align-self:flex-end;
    color:white;
    background:var(--primary);
}

.message-time{
    font-size:10px;
    opacity:.6;
    margin-top:5px;
}

.chat-input{
    border-top:1px solid var(--border);
    padding:14px;
    display:flex;
    gap:10px;
}

.chat-input input{
    flex:1;
    border:1px solid var(--border);
    background:var(--input);
    color:var(--text);
    padding:12px;
    border-radius:11px;
    outline:none;
}

/* =========================================================
   MODAL
   ========================================================= */

.modal{
    position:fixed;
    inset:0;
    background:rgba(0,0,0,.55);
    z-index:5000;
    display:none;
    align-items:center;
    justify-content:center;
    padding:20px;
}

.modal.show{
    display:flex;
}

.modal-content{
    background:var(--card);
    width:min(600px,100%);
    max-height:90vh;
    overflow:auto;
    border-radius:20px;
    padding:24px;
    box-shadow:0 25px 70px rgba(0,0,0,.3);
}

.modal-header{
    display:flex;
    justify-content:space-between;
    align-items:center;
    margin-bottom:20px;
}

.close-btn{
    border:0;
    background:var(--input);
    color:var(--text);
    width:36px;
    height:36px;
    border-radius:10px;
}

/* =========================================================
   TOAST
   ========================================================= */

.toast-container{
    position:fixed;
    right:20px;
    bottom:20px;
    z-index:10000;
    display:flex;
    flex-direction:column;
    gap:10px;
}

.toast{
    min-width:260px;
    background:var(--card);
    color:var(--text);
    border:1px solid var(--border);
    box-shadow:0 15px 35px rgba(0,0,0,.18);
    border-radius:13px;
    padding:14px 16px;
    animation:toastIn .25s ease;
}

.toast.success{
    border-left:4px solid var(--success);
}

.toast.error{
    border-left:4px solid var(--danger);
}

@keyframes toastIn{
    from{
        transform:translateY(15px);
        opacity:0;
    }
    to{
        transform:translateY(0);
        opacity:1;
    }
}

/* =========================================================
   EMPTY
   ========================================================= */

.empty{
    padding:35px;
    text-align:center;
    color:var(--muted);
}

.empty-icon{
    font-size:40px;
    margin-bottom:10px;
}

/* =========================================================
   MOBILE
   ========================================================= */

@media(max-width:1100px){

    .stats-grid{
        grid-template-columns:repeat(2,1fr);
    }

    .two-col{
        grid-template-columns:1fr;
    }

    .resource-grid{
        grid-template-columns:repeat(2,1fr);
    }

    .notes-grid{
        grid-template-columns:repeat(2,1fr);
    }
}

@media(max-width:800px){

    .sidebar{
        transform:translateX(-100%);
        width:280px;
        box-shadow:20px 0 40px rgba(0,0,0,.12);
    }

    .sidebar.open{
        transform:translateX(0);
    }

    .main{
        margin-left:0;
        width:100%;
    }

    .mobile-menu{
        display:block;
    }

    .topbar{
        padding:0 16px;
    }

    .search{
        display:none;
    }

    .content{
        padding:18px;
    }

    .welcome{
        flex-direction:column;
        align-items:flex-start;
    }

    .stats-grid{
        grid-template-columns:1fr 1fr;
        gap:12px;
    }

    .stat-card{
        padding:16px;
    }

    .stat-value{
        font-size:23px;
    }

    .ai-layout{
        grid-template-columns:1fr;
    }

    .ai-sidebar{
        display:none;
    }

    .resource-grid,
    .notes-grid{
        grid-template-columns:1fr;
    }

    .form-grid{
        grid-template-columns:1fr;
    }

    .chat{
        height:600px;
    }
}

@media(max-width:480px){

    .page-title{
        font-size:18px;
    }

    .top-actions .icon-btn{
        width:38px;
        height:38px;
    }

    .welcome{
        padding:22px;
        border-radius:18px;
    }

    .welcome h1{
        font-size:24px;
    }

    .stats-grid{
        grid-template-columns:1fr;
    }

    .message{
        max-width:88%;
    }
}
</style>
</head>

<body>

<!-- =======================================================
     LOADING
======================================================= -->

<div id="loadingScreen">
    <div class="loader"></div>
    <strong>Chargement de Campus Assistant...</strong>
</div>

<div class="app">

<!-- =======================================================
     SIDEBAR
======================================================= -->

<aside class="sidebar" id="sidebar">

    <div class="logo">
        <div class="logo-icon">🎓</div>
        <div class="logo-text">
            Campus<span>Assistant</span>
        </div>
    </div>

    <nav class="nav">

        <button class="active" data-view="dashboard">
            <span class="nav-icon">🏠</span>
            Tableau de bord
        </button>

        <button data-view="schedule">
            <span class="nav-icon">📅</span>
            Emploi du temps
        </button>

        <butt
