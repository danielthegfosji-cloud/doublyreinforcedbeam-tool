# RC Design Suite - Agent Guidelines

## Project Overview

This is a pure HTML/CSS/JavaScript web application implementing ACI 318-11 reinforced concrete design calculations. No build system or test framework exists.

## Build, Lint, and Test Commands

### Running the Application
Simply open any HTML file in a modern web browser:
```bash
# Open in default browser (Windows)
start index.html

# Or use any local server
python -m http.server 8000
# Then visit http://localhost:8000
```

### No Build System
This project uses no bundler, transpiler, or build tools. All JavaScript and CSS are inline within HTML files or in a single `styles.css`.

### No Test Framework
No automated tests exist. Manual verification should be performed by opening pages in a browser.

---

## Code Style Guidelines

### HTML Structure
- Use semantic HTML5 elements (`<header>`, `<main>`, `<nav>`, `<section>`)
- Always include `<!DOCTYPE html>` and `lang="en"`
- Meta viewport tag for responsive design
- External resources loaded via CDN in `<head>`:
  - Font Awesome icons
  - Google Fonts (Inter)
  - MathJax for LaTeX rendering
  - Chart.js, Plotly.js, Three.js for visualizations

### CSS Conventions
```css
/* Use CSS custom properties (variables) for theming */
:root {
    --primary: #2c3e50;
    --accent: #3498db;
    --error: #e74c3c;
}

/* BEM-like naming for components */
.nav-item, .nav-header, .card, .card-icon, .card-title

/* Layout patterns */
.sidebar { width: 380px; position: fixed; }
.main-content, .content-area { margin-left: 380px; }

/* Form elements */
.form-group, .form-row, .form-col, label, input, select
```

### JavaScript Conventions

**Constants and Data:**
```javascript
const Es = 200000; // MPa - Steel modulus
const rebarData = [
    { name: "8 mm", diam: 8.0, area: 50 },
    { name: "10 mm", diam: 11.3, area: 100 },
    // ...
];
```

**Function Naming:** camelCase
```javascript
function calculateDesign() { }
function getBeta1(fc) { }
function drawSection(b, h, cover, stirrup, n_tension) { }
function switchTab(mode) { }
```

**Input Retrieval Pattern:**
```javascript
const fc = parseFloat(document.getElementById('d_fc').value);
const fy = parseFloat(document.getElementById('d_fy').value);
```

**Validation Pattern:**
```javascript
if (isNaN(fc) || fc < 12 || isNaN(fy) || fy < 200) {
    document.getElementById('result-output').innerHTML = 
        "<p style='color: var(--error);'>Error message here.</p>";
    return;
}
```

**DOM Manipulation:**
```javascript
document.getElementById('results').innerHTML = resultHTML;
document.getElementById('results').style.display = 'block';
```

**Canvas Drawing:**
```javascript
function drawSection(...) {
    const canvas = document.getElementById('beamCanvas');
    const ctx = canvas.getContext('2d');
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    // Use ctx.fillRect, ctx.arc, ctx.strokeRect, etc.
}
```

**Event Handling:**
```javascript
button.onclick = functionName;
// Or inline
<button onclick="calculateDesign()">Calculate</button>
```

---

## Engineering Conventions

### Unit System
- Use SI units consistently: MPa for stress, mm for dimensions, kN for force
- Convert units at input boundaries:
```javascript
const Mu = Mu_kNm * 1e6; // Convert kN-m to N-mm
const Vu = Vu_kN * 1e3;  // Convert kN to N
```

### ACI 318M-11 Constants
- Concrete strain limit: `eps_u = 0.003`
- Steel modulus: `Es = 200000 MPa`
- Beta1 factor: `0.85` for f'c ≤ 28 MPa, reduces by 0.05 per 7 MPa above 28, min 0.65
- Phi factors: `0.9` tension-controlled, `0.65` compression-controlled, transition zone per code
- Capacity reduction: `phi = 0.65 + (et - 0.002) * 250/3` in transition

### Calculation Patterns
- Always implement iterative solvers for c (neutral axis depth) with convergence tolerance
- Include code check alerts (warnings for transition zone, errors for code violations)
- Show both nominal and design (phi-reduced) values in results

---

## File Organization

| File | Purpose |
|------|---------|
| `index.html` | Main dashboard with navigation sidebar |
| `styles.css` | Shared styles with CSS variables |
| `*.html` | Individual calculator modules |
| `Split_Topics/` | Reference documentation |

### Creating New Calculator Pages
1. Copy structure from existing page (e.g., `rectangular-beams.html`)
2. Include required CDN scripts
3. Link `styles.css`
4. Use sidebar navigation pattern
5. Implement calculation functions with proper validation
6. Add Canvas visualizations for section diagrams
7. Use MathJax for LaTeX formulas in labels and results

---

## Common Patterns

### Tab Switching
```javascript
function switchTab(tab) {
    const designForm = document.getElementById('design-form');
    const analysisForm = document.getElementById('analysis-form');
    
    if (tab === 'design') {
        designForm.style.display = 'block';
        analysisForm.style.display = 'none';
    } else {
        designForm.style.display = 'none';
        analysisForm.style.display = 'block';
    }
    MathJax.typesetPromise();
}
```

### Rendering Results
```javascript
let resultHTML = `<h4>Design Results</h4>`;
resultHTML += `<div class="result-item"><span>Label:</span> <strong>${value}</strong></div>`;
document.getElementById('result-output').innerHTML = resultHTML;
MathJax.typesetPromise();
```

### Alert Messages
```javascript
const alertArea = document.getElementById('alert-area');
alertArea.innerHTML = `<div class="alert-box alert-danger"><i class="fa-solid fa-circle-xmark"></i> Error message</div>`;
```
