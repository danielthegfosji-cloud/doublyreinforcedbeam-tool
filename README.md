# SimpleCrete Suite

### [🚀 Live Demo](https://danielthegfosji-cloud.github.io/reinforcedConcrete/)

A comprehensive, web-based engineering suite for the analysis and design of reinforced concrete and masonry structures. This tool implements the **ACI 318-11** and **ACI 530/TMS 402** standards, providing engineers and students with an interactive platform to verify structural components.

## 🌟 Key Features

The suite is divided into specialized modules covering the full spectrum of reinforced concrete design:

### 1. Analysis & Basics
*   **Material Properties:** Calculate $E_c$, $f_r$, and $\beta_1$ based on concrete density and strength. Includes standard metric rebar data.
*   **Load Calculations:** Automated factored load combinations ($1.2D + 1.6L$) and generation of Shear/Moment diagrams for various support conditions.
*   **Flexural Analysis:** Interactive exploration of the three stages of beam behavior: Uncracked, Cracked-Elastic (Transformed Section), and Ultimate Strength.

### 2. Beam Design
*   **Rectangular Beams:** Design and analysis for singly and doubly reinforced sections with automated strain limit and ductility checks.
*   **T-Beams:** Analysis of effective flange widths and transition between rectangular and T-beam behavior.
*   **Shear & Torsion:** Detailed stirrup spacing design and combined stress checks for members subject to torque.
*   **Serviceability:** Calculation of Gergely-Lutz crack widths and long-term deflections using the effective moment of inertia ($I_e$).
*   **Bond & Development:** Calculation of tension/compression development lengths, lap splices, and standard hook requirements.

### 3. Column Analysis
*   **Short Columns:** Axial capacity verification and slenderness limit checks.
*   **Interaction Diagrams:** Generation of $P_n-M_n$ curves for biaxial bending and section capacity verification.
*   **Slender Columns:** Moment magnification method for braced and unbraced frames.

### 4. Slabs & Foundations
*   **Slab Systems:** Design of One-Way and Two-Way slabs using the Direct Design Method (DDM) and Equivalent Frame Method (EFM).
*   **Foundations:** Specialized calculators for Wall Footings, Isolated Footings (centered or eccentric), Combined Footings, and Pile Caps.
*   **Mat Foundations:** Analysis of soil pressure distribution and reinforcement mesh requirements for multi-column mats.

### 5. Walls & Special Topics
*   **Retaining Walls:** Stability analysis (Overturning, Sliding, Bearing) and structural design of the stem, toe, and heel.
*   **Shear Walls:** In-plane shear and flexural design for lateral force-resisting systems.
*   **Prestressed Concrete:** Stress verification at transfer and service stages, along with ultimate strength estimation for bonded tendons.
*   **Reinforced Masonry:** Design of non-load-bearing walls for out-of-plane lateral loads.

## 🛠️ Technical Stack

*   **Frontend:** HTML5, CSS3 (Modern Sidebar UI), Vanilla JavaScript (ES6+).
*   **Mathematics:** [MathJax](https://www.mathjax.org/) for high-quality LaTeX rendering of engineering formulas.
*   **Visualizations:**
    *   **Canvas API:** Dynamic 2D cross-sections and stress/strain diagrams.
    *   **Chart.js:** Interactive interaction diagrams and deflection profiles.
    *   **Plotly.js:** 3D surface plots for moment capacity analysis.
    *   **Three.js:** 3D reinforcement models for complex slab systems.

## 📚 Standards & References

*   **ACI 318-11:** Building Code Requirements for Structural Concrete.
*   **ACI 530-11 / TMS 402:** Building Code Requirements for Masonry Structures.
*   **McCormac & Brown:** *Design of Reinforced Concrete*, 9th Edition.

## 🚀 Getting Started

1.  Clone the repository.
2.  Open `index.html` in any modern web browser.
3.  Select a design module from the sidebar.
4.  Input your geometric and material parameters.
5.  Click **Calculate** to see detailed step-by-step derivations and visualizations.

---
*Developed for educational and preliminary design verification purposes.*

[!GitHub Pages](https://danielthegfosji-cloud.github.io/reinforcedConcrete/)
