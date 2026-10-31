# MeasurePath Open-Source Construction & Architectural Takeoff Formulas

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Web Platform](https://img.shields.io/badge/Platform-MeasurePath-254f42.svg)](https://getcoatpath.com/)
[![Interactive Studio](https://img.shields.io/badge/2D%2F3D-CAD%20Studio-blue.svg)](https://getcoatpath.com/studio/)
[![Calculators](https://img.shields.io/badge/Calculators-19%20Live%20Tools-brightgreen.svg)](https://getcoatpath.com/calculators/)

Welcome to the official open-source formula repository and technical specification for [MeasurePath](https://getcoatpath.com/), the zero-telemetry 2D/3D architectural CAD takeoff studio and free construction calculation toolkit developed by [Kavory Labs](https://getcoatpath.com/about/).

Every formula documented here executes entirely client-side in pure vanilla JavaScript with zero network overhead, zero external tracking, and direct adherence to standard ASTM building standards, GA-214 gypsum finish guidelines, and published manufacturer material yields.

---

## Table of Contents
1. [Core Takeoff Calculation Engines](#core-takeoff-calculation-engines)
   - [1. 2D Boolean Floor & Wall Grid Engine](#1-2d-boolean-floor--wall-grid-engine)
   - [2. Roof Pitch, Gradient & Slope Multiplier Formula](#2-roof-pitch-gradient--slope-multiplier-formula)
   - [3. 1 Quart vs. 1 Gallon Paint Coverage Rates](#3-1-quart-vs-1-gallon-paint-coverage-rates)
   - [4. Concrete Cubic Yards, Slab Cost & Bag Yields](#4-concrete-cubic-yards-slab-cost--bag-yields)
   - [5. Drywall Sheets, Joint Mud & Fastener Takeoff](#5-drywall-sheets-joint-mud--fastener-takeoff)
   - [6. Epoxy Floor Coating & Flake Broadcast Rates](#6-epoxy-floor-coating--flake-broadcast-rates)
2. [Live Interactive Tools & Takeoff Calculators](#live-interactive-tools--takeoff-calculators)
3. [Technical Case Studies & Articles](#technical-case-studies--articles)
4. [License & Contributing](#license--contributing)

---

## Core Takeoff Calculation Engines

### 1. 2D Boolean Floor & Wall Grid Engine
The MeasurePath spatial takeoff engine converts room perimeter boundaries and ceiling elevations into exact net paintable and flooring areas by performing Boolean polygon deductions for architectural openings (doors, windows, alcoves, and stairwells).

#### Wall Area Formulation
$$\text{Gross Wall Area} = 2 \times (\text{Length} + \text{Width}) \times \text{Height}$$

$$\text{Net Paintable Wall Area} = \text{Gross Wall Area} - \sum (\text{Door Area} + \text{Window Area} + \text{Unpainted Voids})$$

- Standard door deduction: $21\text{ sq ft}$ ($1.95\text{ m}^2$) for a standard $3\times 7\text{ ft}$ interior door.
- Standard window deduction: $12\text{ to }15\text{ sq ft}$ ($1.11\text{ to }1.39\text{ m}^2$) per opening.
- Ceiling Area: $\text{Length} \times \text{Width}$.

---

### 2. Roof Pitch, Gradient & Slope Multiplier Formula
In architectural framing and roofing takeoff, horizontal plan footprint area must be adjusted to true sloping surface area using the pitch multiplier.

#### Mathematical Formulas
Given vertical rise $R$ in inches over a standard horizontal run of $12$ inches:

$$\text{Pitch Ratio} = \frac{R}{12}$$

$$\text{Pitch Multiplier} = \sqrt{1 + \left(\frac{R}{12}\right)^2}$$

$$\text{Pitch Angle } \theta = \arctan\left(\frac{R}{12}\right) \times \left(\frac{180}{\pi}\right)$$

$$\text{Slope Gradient } (\%) = \left(\frac{R}{12}\right) \times 100$$

$$\text{Sloping Rafter Length} = (\text{Run} \times \text{Multiplier}) + (\text{Overhang} \times \text{Multiplier})$$

#### Quick Reference Table
| Pitch Ratio | Pitch Angle ($\theta$) | Slope Gradient (%) | Pitch Multiplier | Takeoff Factor per 1,000 sq ft Footprint |
| :--- | :--- | :--- | :--- | :--- |
| **3/12** | $14.04^\circ$ | $25.0\%$ | **1.0308** | $1,030.8\text{ sq ft}$ (10.31 squares) |
| **4/12** | $18.43^\circ$ | $33.3\%$ | **1.0541** | $1,054.1\text{ sq ft}$ (10.54 squares) |
| **5/12** | $22.62^\circ$ | $41.7\%$ | **1.0833** | $1,083.3\text{ sq ft}$ (10.83 squares) |
| **6/12** | $26.57^\circ$ | $50.0\%$ | **1.1180** | $1,118.0\text{ sq ft}$ (11.18 squares) |
| **7/12** | $30.26^\circ$ | $58.3\%$ | **1.1577** | $1,157.7\text{ sq ft}$ (11.58 squares) |
| **8/12** | $33.69^\circ$ | $66.7\%$ | **1.2019** | $1,201.9\text{ sq ft}$ (12.02 squares) |
| **10/12** | $39.81^\circ$ | $83.3\%$ | **1.3017** | $1,301.7\text{ sq ft}$ (13.02 squares) |
| **12/12** | $45.00^\circ$ | $100.0\%$ | **1.4142** | $1,414.2\text{ sq ft}$ (14.14 squares) |

---

### 3. 1 Quart vs. 1 Gallon Paint Coverage Rates
Material coverage adheres to published ASTM D5150 architectural coatings testing and major manufacturer spread rate benchmarks:

$$\text{Gallons Required} = \left(\frac{\text{Net Surface Area}}{\text{Spread Rate}}\right) \times \text{Number of Coats} \times (1 + \text{Waste Factor})$$

- **1 US Gallon ($3.785\text{ L}$)**: Covers $350\text{ to }400\text{ sq ft}$ ($32.5\text{ to }37.2\text{ m}^2$) for 1 coat, or $175\text{ to }200\text{ sq ft}$ ($16.3\text{ to }18.6\text{ m}^2$) for 2 coats on primed smooth drywall.
- **1 US Quart ($0.946\text{ L}$)**: Covers $85\text{ to }100\text{ sq ft}$ ($7.9\text{ to }9.3\text{ m}^2$) for 1 coat, or $45\text{ to }50\text{ sq ft}$ ($4.2\text{ to }4.6\text{ m}^2$) for 2 coats (ideal for powder rooms, accent walls, and doors).
- **8 oz Sample Jar ($0.237\text{ L}$)**: Covers $20\text{ to }25\text{ sq ft}$ ($1.9\text{ to }2.3\text{ m}^2$) for color swatching.
- **Exterior Paint Yield**: $300\text{ to }350\text{ sq ft/gal}$ on primed wood siding; $200\text{ to }250\text{ sq ft/gal}$ on textured stucco or masonry.

---

### 4. Concrete Cubic Yards, Slab Cost & Bag Yields
Standard ACI 302 concrete slab volume geometry:

$$\text{Volume (yd}^3\text{)} = \frac{\text{Length (ft)} \times \text{Width (ft)} \times \left(\frac{\text{Depth (in)}}{12}\right)}{27} \times (1 + \text{Waste})$$

$$\text{Metric Volume (m}^3\text{)} = \text{Length (m)} \times \text{Width (m)} \times \text{Thickness (m)} \times (1 + \text{Waste})$$

#### Pre-mixed Bag Quantities
- **80 lb Bag**: Yields $0.60\text{ cu ft}$ $\rightarrow$ $45\text{ bags per cubic yard}$.
- **60 lb Bag**: Yields $0.45\text{ cu ft}$ $\rightarrow$ $60\text{ bags per cubic yard}$.
- **40 lb Bag**: Yields $0.30\text{ cu ft}$ $\rightarrow$ $90\text{ bags per cubic yard}$.

#### Complete Slab Cost Function
$$\text{Total Cost} = (\text{Volume}_{\text{yd}^3} \times \text{Price}_{\text{yd}^3}) + (\text{Area}_{\text{ft}^2} \times \text{Labor Rate}_{\text{ft}^2}) + \text{Site Prep} + \text{Reinforcement (Rebar/Mesh)} + \text{Delivery/Pumping}$$

---

### 5. Drywall Sheets, Joint Mud & Fastener Takeoff
Based on the Gypsum Association GA-214 standard specifications:

#### Sheet Estimation
$$\text{Sheets Needed} = \left\lceil \frac{\text{Total Surface Area}}{\text{Sheet Area}} \times (1 + \text{Waste Factor}) \right\rceil$$
- Standard $4\times 8\text{ ft}$ sheet $= 32\text{ sq ft}$ ($2.97\text{ m}^2$).
- High-efficiency $4\times 12\text{ ft}$ sheet $= 48\text{ sq ft}$ ($4.46\text{ m}^2$).

#### Joint Compound (Mud) & Tape Coverage
- **Level 4 Finish (Smooth Standard)**: $0.45\text{ US gallons per 4}\times 8\text{ sheet}$ (~$1.40\text{ gal per 100 sq ft}$, or 10 sheets per standard 4.5-gal ready-mix box).
- **Level 3 Finish (Heavy Texture Base)**: $0.32\text{ US gallons per sheet}$ (~$1.00\text{ gal per 100 sq ft}$).
- **Level 5 Skim Coat (Full Surface)**: $0.75\text{ US gallons per sheet}$ (~$2.35\text{ gal per 100 sq ft}$).
- **Joint Tape**: $12\text{ linear ft per 4}\times 8\text{ sheet}$ (~$37.5\text{ linear ft per 100 sq ft}$).
- **Drywall Screws**: 32 fasteners per $4\times 8$ board on 16" on-center studs.

---

### 6. Epoxy Floor Coating & Flake Broadcast Rates
Industrial floor coating takeoff for concrete slabs and garage floors:

- **100% Solids Commercial Epoxy**: $150\text{ to }200\text{ sq ft per gallon}$ at $8\text{ to }10\text{ mils}$ Dry Film Thickness (DFT).
- **Water-Based DIY Kits**: $250\text{ to }400\text{ sq ft}$ per packaged kit.
- **Decorative Color Flake Density (per 400 sq ft 2-car garage)**:
  - *Light Broadcast*: $8\text{ to }10\text{ lbs}$ ($0.02\text{ to }0.025\text{ lbs/sq ft}$).
  - *Medium Broadcast*: $20\text{ to }25\text{ lbs}$ ($0.05\text{ to }0.06\text{ lbs/sq ft}$).
  - *Full Broadcast to Rejection*: $50\text{ to }60\text{ lbs}$ ($0.125\text{ to }0.15\text{ lbs/sq ft}$).
- **Protective Clear Topcoat**: Polyaspartic or chemical-resistant polyurethane applied at $300\text{ to }350\text{ sq ft per gallon}$ to seal broadcast flakes.

---

## Live Interactive Tools & Takeoff Calculators

The formulas above power the entire free suite of interactive estimators on MeasurePath:

1. [MeasurePath Home — Free Construction & Painting Calculators](https://getcoatpath.com/)
2. [2D/3D Architectural CAD & Material Takeoff Studio](https://getcoatpath.com/studio/)
3. [All 19 Construction Calculators Hub](https://getcoatpath.com/calculators/)
4. [Roof Pitch, Slope & Gradient Calculator](https://getcoatpath.com/roof-pitch-calculator/)
5. [Room Paint & Primer Calculator](https://getcoatpath.com/paint-calculator/)
6. [1 Quart & 1 Gallon Paint Coverage Calculator](https://getcoatpath.com/paint-coverage-calculator/)
7. [Concrete Slab Cost Calculator](https://getcoatpath.com/concrete-slab-cost-calculator/)
8. [Concrete Volume & Bag Calculator](https://getcoatpath.com/concrete-calculator/)
9. [Epoxy Garage Floor Calculator](https://getcoatpath.com/epoxy-floor-calculator/)
10. [Roof Coating Cost & Gallon Calculator](https://getcoatpath.com/roof-coating-calculator/)
11. [Drywall Sheet Calculator](https://getcoatpath.com/drywall-calculator/)
12. [Drywall Mud & Tape Calculator](https://getcoatpath.com/drywall-mud-calculator/)
13. [Flooring & Carton Calculator](https://getcoatpath.com/flooring-calculator/)
14. [Primer Coverage Calculator](https://getcoatpath.com/primer-calculator/)
15. [Ceiling Paint Calculator](https://getcoatpath.com/ceiling-paint-calculator/)
16. [Exterior Paint Calculator](https://getcoatpath.com/exterior-paint-calculator/)
17. [Interior Painting Cost Calculator](https://getcoatpath.com/interior-painting-cost-calculator/)
18. [Roof Shingle & Square Calculator](https://getcoatpath.com/roof-shingle-calculator/)
19. [Gravel & Crushed Stone Calculator](https://getcoatpath.com/gravel-calculator/)
20. [Sonotube & Post Hole Concrete Calculator](https://getcoatpath.com/sonotube-concrete-calculator/)
21. [Deck & Fence Stain Calculator](https://getcoatpath.com/deck-stain-calculator/)
22. [Free Construction Estimate Generator](https://getcoatpath.com/construction-estimate-generator/)

---

## Technical Case Studies & Articles

For an in-depth architectural breakdown of our zero-telemetry client-side rendering pipeline, real-time 3D Three.js geometry generation, and tabular monospace design system:

- 📖 **Dev.to Technical Case Study**: [Building MeasurePath: A Zero-Telemetry 2D/3D Construction Studio & Calculator Toolkit in Pure JS](https://dev.to/kavorylabs/building-measurepath-a-zero-telemetry-2d-3d-construction-studio-calculator-toolkit-in-pure-js)
- 📝 **Medium Deep Dive**: [Building MeasurePath: A Zero-Telemetry 2D/3D Construction Studio & Calculator Toolkit in Pure JS](https://medium.com/@kavorylabs/building-measurepath-a-zero-telemetry-2d-3d-construction-studio-calculator-toolkit-in-pure-js)
- 🏢 **Parent Studio**: [Kavory Labs](https://getcoatpath.com/about/)

---

## License & Contributing

Distributed under the **MIT License**. See [LICENSE](LICENSE) for details. Contributions, benchmark citations, and pull requests for architectural standards are welcome!
