# CV PT/EN Toggle & Content Rewrite Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add a PT/EN language toggle to `index.html` and rewrite all content with stronger, impact-oriented bullets in both languages.

**Architecture:** Single `index.html` file. A `lang-pt` / `lang-en` class on `<body>` controls visibility via CSS. All bilingual text is wrapped in `.pt` / `.en` sibling elements. The toggle button saves preference to `localStorage`.

**Tech Stack:** HTML, CSS, vanilla JavaScript. No build tools. Test by opening the file in a browser.

---

### Task 1: Add CSS for language toggle

**Files:**
- Modify: `index.html` — inside the `<style>` block, after the `@media print` section

**Step 1: Add the two CSS rules**

Inside the `<style>` block, before the closing `</style>`, add:

```css
/* --- LANGUAGE TOGGLE --- */
body.lang-pt .en { display: none !important; }
body.lang-en .pt { display: none !important; }
```

**Step 2: Verify in browser**

Open `index.html` in browser. Nothing should change visually yet — both `.pt` and `.en` elements are showing because neither class is on `<body>` yet.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add CSS for PT/EN language toggle"
```

---

### Task 2: Add toggle button and JavaScript

**Files:**
- Modify: `index.html` — add button after the existing `.print-btn` and add `<script>` before `</body>`

**Step 1: Add the toggle button HTML**

After the existing `<button onclick="window.print()" class="print-btn">` block, add:

```html
<button id="lang-btn" class="print-btn lang-btn" onclick="toggleLang()">
    <i class="fas fa-globe"></i> EN
</button>
```

**Step 2: Add CSS for the lang button position**

Inside `<style>`, after `.print-btn:hover` rule, add:

```css
.lang-btn {
    top: 20px;
    right: 165px;
    background-color: var(--text-light);
}

.lang-btn:hover {
    background-color: var(--primary);
}

@media print {
    .lang-btn { display: none; }
}
```

**Step 3: Add JavaScript before `</body>`**

```html
<script>
    function toggleLang() {
        const body = document.body;
        const btn = document.getElementById('lang-btn');
        if (body.classList.contains('lang-en')) {
            body.classList.remove('lang-en');
            body.classList.add('lang-pt');
            btn.innerHTML = '<i class="fas fa-globe"></i> EN';
            localStorage.setItem('cv-lang', 'pt');
        } else {
            body.classList.remove('lang-pt');
            body.classList.add('lang-en');
            btn.innerHTML = '<i class="fas fa-globe"></i> PT';
            localStorage.setItem('cv-lang', 'en');
        }
    }

    // Load saved preference or default to PT
    (function () {
        const saved = localStorage.getItem('cv-lang') || 'pt';
        document.body.classList.add('lang-' + saved);
        const btn = document.getElementById('lang-btn');
        btn.innerHTML = '<i class="fas fa-globe"></i> ' + (saved === 'pt' ? 'EN' : 'PT');
    })();
</script>
```

**Step 4: Verify in browser**

- Open `index.html`. Page should load in PT.
- Click the globe button. Page should switch to EN (blank for now, since no `.en` elements exist yet).
- Click again. Should switch back to PT.
- Refresh. Should remember the last selected language.

**Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add language toggle button and JS with localStorage persistence"
```

---

### Task 3: Wrap header content in PT/EN pairs

**Files:**
- Modify: `index.html` — the `<header>` block

**Step 1: Replace the `<header>` block**

Replace the entire `<header>...</header>` with:

```html
<header>
    <h1>Lucas Sigrist</h1>
    <div class="role-title">
        <span class="pt">Engenheiro de Automação & Controle | DevSecOps & Cloud Infrastructure</span>
        <span class="en">Automation & Control Engineer | DevSecOps & Cloud Infrastructure</span>
    </div>

    <div class="contact-bar">
        <div class="contact-item">
            <i class="fas fa-map-marker-alt"></i> Americana – SP
        </div>
        <div class="contact-item">
            <i class="fas fa-envelope"></i>
            <a href="mailto:sigrist@live.com">sigrist@live.com</a>
        </div>
        <div class="contact-item">
            <i class="fab fa-whatsapp"></i>
            <a href="https://wa.me/5519996283457" target="_blank" class="whatsapp-btn">
                (19) 99628-3457
            </a>
        </div>
        <div class="contact-item">
            <i class="fab fa-linkedin"></i>
            <a href="https://www.linkedin.com/in/lucassigrist/" target="_blank">LinkedIn Profile</a>
        </div>
    </div>
</header>
```

**Step 2: Verify**

Toggle between PT and EN — role title should change. Everything else stays the same.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: wrap header role title in PT/EN language pairs"
```

---

### Task 4: Rewrite and wrap summary section

**Files:**
- Modify: `index.html` — the `.summary` div inside `<main>`

**Step 1: Replace the `.summary` div**

```html
<div class="summary">
    <p class="pt">Engenheiro de Automação e Controle com atuação em <strong>DevSecOps e Infraestrutura On-Prem e Cloud</strong>. Experiência sólida em orquestração de ambientes híbridos (AWS, Azure, VMware), automação de operações e observabilidade. Histórico de liderança em migrações de segurança, modernização de legado e implementação de pipelines CI/CD — entregando redução de risco operacional e eficiência mensurável.</p>
    <p class="en">Automation & Control Engineer specializing in <strong>DevSecOps and hybrid Cloud/On-Prem infrastructure</strong>. Proven track record in orchestrating multi-cloud environments (AWS, Azure, VMware), automating operations, and building observability solutions. Led security modernization initiatives, legacy migrations, and CI/CD implementations — delivering measurable risk reduction and operational efficiency.</p>
</div>
```

**Step 2: Verify**

Toggle PT/EN — summaries should swap cleanly.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: rewrite and wrap summary in PT/EN"
```

---

### Task 5: Wrap section titles in PT/EN

**Files:**
- Modify: `index.html` — all `<h2 class="section-title">` elements in `<main>`

**Step 1: Replace section title for Experiência**

```html
<h2 class="section-title">
    <i class="fas fa-briefcase"></i>
    <span class="pt">Experiência Profissional</span>
    <span class="en">Work Experience</span>
</h2>
```

**Step 2: Verify toggle on section title**

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: wrap section titles in PT/EN"
```

---

### Task 6: Rewrite and wrap MSDN job bullets

**Files:**
- Modify: `index.html` — the first `.job-item` (MSDN Tecnologia)

**Step 1: Replace the MSDN `.job-item`**

```html
<div class="job-item">
    <div class="job-header">
        <div class="job-role">
            <span class="pt">Analista de Infraestrutura / Cloud & DevOps</span>
            <span class="en">Infrastructure Analyst / Cloud & DevOps</span>
        </div>
        <div class="job-company">MSDN Tecnologia</div>
        <div class="job-date">
            <span class="pt">Fev 2025 – Atual</span>
            <span class="en">Feb 2025 – Present</span>
        </div>
    </div>
    <div class="job-desc">
        <ul>
            <li>
                <span class="pt"><strong>Cloud Engineering:</strong> Arquitetura e sustentação de workloads em AWS e Azure, garantindo escalabilidade e alta disponibilidade para aplicações críticas de clientes corporativos.</span>
                <span class="en"><strong>Cloud Engineering:</strong> Architected and maintained workloads on AWS and Azure, ensuring scalability and high availability for enterprise-critical applications.</span>
            </li>
            <li>
                <span class="pt"><strong>Observabilidade:</strong> Desenvolveu check customizado no Datadog (Python/API + SNMP) para monitoramento de SD-WAN Fortinet, eliminando ponto cego de visibilidade de SLAs e QoS em ambiente multi-site.</span>
                <span class="en"><strong>Observability:</strong> Built a custom Datadog check (Python/API + SNMP) for Fortinet SD-WAN monitoring, eliminating a visibility blind spot for SLA and QoS metrics across a multi-site environment.</span>
            </li>
            <li>
                <span class="pt"><strong>Network Security:</strong> Migrou acesso remoto de SSL VPN para IPsec IKEv2 (XAuth → EAP) e autenticação de LDAP para Radius, implementando microsegmentação baseada em identidade e reduzindo superfície de ataque.</span>
                <span class="en"><strong>Network Security:</strong> Migrated remote access from SSL VPN to IPsec IKEv2 (XAuth → EAP) and authentication from LDAP to Radius, implementing identity-based microsegmentation and reducing attack surface.</span>
            </li>
            <li>
                <span class="pt"><strong>Containerização:</strong> Administração de ambientes Docker, padronizando o ciclo de vida de aplicações e eliminando conflitos de dependências entre serviços.</span>
                <span class="en"><strong>Containerization:</strong> Managed Docker environments, standardizing application lifecycle and eliminating inter-service dependency conflicts.</span>
            </li>
            <li>
                <span class="pt"><strong>Automação:</strong> Desenvolveu scripts Shell e PowerShell para eliminar rotinas manuais repetitivas, liberando capacidade da equipe para tarefas de maior valor.</span>
                <span class="en"><strong>Automation:</strong> Developed Shell and PowerShell scripts to eliminate repetitive manual routines, freeing team capacity for higher-value work.</span>
            </li>
            <li>
                <span class="pt"><strong>Disaster Recovery:</strong> Gestão de backup imutável com Veeam Backup & Replication em ambientes VMware vSphere, garantindo RTO/RPO para workloads críticos.</span>
                <span class="en"><strong>Disaster Recovery:</strong> Managed immutable backup strategy with Veeam Backup & Replication on VMware vSphere, ensuring RTO/RPO compliance for critical workloads.</span>
            </li>
        </ul>
    </div>
</div>
```

**Step 2: Verify in browser**

Toggle PT/EN — bullets should swap. Layout should not break.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: rewrite and wrap MSDN job bullets in PT/EN"
```

---

### Task 7: Rewrite and wrap Spivit job bullets

**Files:**
- Modify: `index.html` — the second `.job-item` (Spivit Global Technologies)

**Step 1: Replace the Spivit `.job-item`**

```html
<div class="job-item">
    <div class="job-header">
        <div class="job-role">
            <span class="pt">Analista de Infraestrutura Pleno / DevOps</span>
            <span class="en">Mid-Level Infrastructure Analyst / DevOps</span>
        </div>
        <div class="job-company">Spivit Global Technologies</div>
        <div class="job-date">Jan 2023 – Fev 2025 / Jan 2023 – Feb 2025</div>
    </div>
    <div class="job-desc">
        <ul>
            <li>
                <span class="pt"><strong>CI/CD:</strong> Estruturou pipelines de integração e entrega contínua do zero, acelerando o ciclo de deploy e reduzindo erros manuais no processo de release.</span>
                <span class="en"><strong>CI/CD:</strong> Built CI/CD pipelines from scratch, accelerating deployment cycles and reducing manual errors in the release process.</span>
            </li>
            <li>
                <span class="pt"><strong>Gestão de Identidade:</strong> Administração centralizada de Active Directory, Microsoft Entra ID e RBAC em ambiente híbrido, cobrindo usuários, grupos e políticas de acesso condicional.</span>
                <span class="en"><strong>Identity Management:</strong> Centralized administration of Active Directory, Microsoft Entra ID, and RBAC in a hybrid environment, covering users, groups, and conditional access policies.</span>
            </li>
            <li>
                <span class="pt"><strong>Infraestrutura de Rede:</strong> Configuração avançada de Switch Core (Cisco/Aruba), VLANs e segmentação de rede em ambiente corporativo distribuído.</span>
                <span class="en"><strong>Network Infrastructure:</strong> Advanced configuration of Core Switches (Cisco/Aruba), VLANs, and network segmentation in a distributed enterprise environment.</span>
            </li>
            <li>
                <span class="pt"><strong>ITSM:</strong> Uso de Datto RMM e Autotask para gestão remota de ativos, automação de processos e fluxos ITIL em ambiente MSP.</span>
                <span class="en"><strong>ITSM:</strong> Leveraged Datto RMM and Autotask for remote asset management, process automation, and ITIL workflows in an MSP environment.</span>
            </li>
        </ul>
    </div>
</div>
```

**Step 2: Note about the date** — the Spivit date is the same in both languages, so no PT/EN split needed there. Keep as plain text.

**Step 3: Verify and commit**

```bash
git add index.html
git commit -m "feat: rewrite and wrap Spivit job bullets in PT/EN"
```

---

### Task 8: Wrap São Lucas job and update

**Files:**
- Modify: `index.html` — the third `.job-item` (São Lucas Saúde)

**Step 1: Replace the São Lucas `.job-item`**

```html
<div class="job-item">
    <div class="job-header">
        <div class="job-role">
            <span class="pt">Analista de Informática Jr. / Infraestrutura</span>
            <span class="en">IT Analyst Jr. / Infrastructure</span>
        </div>
        <div class="job-company">São Lucas Saúde S/A</div>
        <div class="job-date">
            <span class="pt">2016 – 2023 (Projetos Intermitentes)</span>
            <span class="en">2016 – 2023 (Intermittent Projects)</span>
        </div>
    </div>
    <div class="job-desc">
        <ul>
            <li>
                <span class="pt">Sustentação de servidores Windows e Linux, gerenciamento de rotinas de backup e monitoramento de infraestrutura hospitalar.</span>
                <span class="en">Maintained Windows and Linux servers, managed backup routines, and monitored hospital infrastructure.</span>
            </li>
            <li>
                <span class="pt">Resolução de chamados de suporte técnico nível 2 e manutenção preventiva/corretiva de hardware e software.</span>
                <span class="en">Resolved Level 2 support tickets and performed preventive and corrective maintenance on hardware and software.</span>
            </li>
        </ul>
    </div>
</div>
```

**Step 2: Verify and commit**

```bash
git add index.html
git commit -m "feat: wrap São Lucas job in PT/EN"
```

---

### Task 9: Update LinkedIn section to hide in EN

**Files:**
- Modify: `index.html` — the LinkedIn section title and embeds wrapper

**Step 1: Add `pt` class to the LinkedIn section**

Change:
```html
<h2 class="section-title no-print">
```
To:
```html
<h2 class="section-title no-print pt">
```

And change:
```html
<div class="linkedin-embeds no-print"
```
To:
```html
<div class="linkedin-embeds no-print pt"
```

**Step 2: Verify**

Switch to EN — LinkedIn section should disappear. Switch to PT — should reappear.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: hide LinkedIn highlights section in EN version"
```

---

### Task 10: Update sidebar — add LinuxTips cert and wrap soft skills

**Files:**
- Modify: `index.html` — the `<aside class="sidebar">` block

**Step 1: Add LinuxTips to Formação**

Find the `.skill-group` for Formação and add after the existing entries:

```html
<div class="edu-item">
    <span class="edu-degree">
        <span class="pt">DevOps Professional</span>
        <span class="en">DevOps Professional Certification</span>
    </span>
    <span class="edu-school">LinuxTips</span>
    <span class="edu-school">
        <span class="pt">Em andamento, 2025</span>
        <span class="en">In progress, 2025</span>
    </span>
</div>
```

**Step 2: Wrap sidebar section titles in PT/EN**

- "Formação" → `<span class="pt">Formação</span><span class="en">Education</span>`
- "Idiomas" → `<span class="pt">Idiomas</span><span class="en">Languages</span>`
- "Soft Skills" → stays the same (already in English/universal)
- "Tech Stack & Tools", "Security & Network", "Automação & OS" → wrap as needed:
  - `<span class="pt">Automação & OS</span><span class="en">Automation & OS</span>`

**Step 3: Wrap Idiomas content**

```html
<div class="edu-item">
    <span class="edu-degree">
        <span class="pt">Português</span>
        <span class="en">Portuguese</span>
    </span>
    <span class="edu-school">
        <span class="pt">Nativo</span>
        <span class="en">Native</span>
    </span>
</div>
<div class="edu-item">
    <span class="edu-degree">
        <span class="pt">Inglês</span>
        <span class="en">English</span>
    </span>
    <span class="edu-school">
        <span class="pt">Técnico (Leitura Avançada)</span>
        <span class="en">Technical (Advanced Reading)</span>
    </span>
</div>
```

**Step 4: Wrap education degrees**

```html
<div class="edu-item">
    <span class="edu-degree">
        <span class="pt">Engenharia de Automação e Controle</span>
        <span class="en">Automation & Control Engineering</span>
    </span>
    <span class="edu-school">
        <span class="pt">Bacharelado Completo</span>
        <span class="en">Bachelor's Degree</span>
    </span>
    <span class="edu-school">Unisal Americana</span>
</div>
<div class="edu-item">
    <span class="edu-degree">
        <span class="pt">Técnico em Redes & Linux</span>
        <span class="en">Network & Linux Technician</span>
    </span>
    <span class="edu-school">Senac / ETEA</span>
</div>
```

**Step 5: Verify full PT/EN toggle**

Toggle both ways. Check: formação, idiomas, skills sections all swap correctly.

**Step 6: Commit**

```bash
git add index.html
git commit -m "feat: wrap sidebar content in PT/EN, add LinuxTips certification"
```

---

### Task 11: Final review and polish

**Step 1: Open in browser and do full review**

Check list:
- [ ] PT version looks identical to original design
- [ ] EN version is fully in English (no PT text leaking)
- [ ] Toggle button is visible and positioned correctly
- [ ] Refresh page — remembers last language
- [ ] Print PT version — toggle button hidden, content correct
- [ ] Print EN version — toggle button hidden, LinkedIn section hidden
- [ ] Mobile view (resize browser) — layout still works

**Step 2: Fix any issues found**

**Step 3: Final commit**

```bash
git add index.html
git commit -m "feat: complete PT/EN CV with content rewrite and language toggle"
```
