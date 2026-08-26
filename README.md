<hr style="border: 6px solid#003262;" />

<div align="center">
    <img src="./images/thumbnails/ehcastroh_teach_banner_flower.png" align="center" width="20%" />
</div>

<br>

# Introduction to Data Visualization

A four-notebook series covering visualization principles, Python charting libraries, zero-code tools (Tableau), and interactive dashboards (Plotly + Dash). Built for self-learners who want both the theory behind good visualization and the practical skills to produce it.

---

## Learning Objectives

By completing this series, a learner will be able to:

- Explain why humans create visualizations and apply Tufte's five principles to evaluate or improve any chart.
- Produce line, scatter, box, and histogram charts in Matplotlib and Seaborn using the object-oriented API.
- Compare Python's major visualization libraries (Pandas, Matplotlib, Seaborn, Plotnine, Plotly, Altair) by building the same chart in each and articulating the key trade-off.
- Build interactive Plotly charts (hover, zoom, linked selections) and turn them into a running Dash web application.
- Navigate Tableau Online to connect data, create worksheets, combine them into a dashboard, and apply a Filter Action.

---

## Data / File Dictionary

| File | Description |
|---|---|
| `data/Iris.csv` | Fisher's Iris dataset - 150 samples, 4 numeric features, 1 species label. Used throughout notebooks 01-02 for chart examples. |
| `data/bii_data_w_categories.csv` | BII (Behavioral Intelligence Index) survey scores - 8 trait features, 1 composite score, department categories. Used in notebooks 02 and 04. |
| `data/bii_data.csv` | BII scores without category labels. |
| `data/bii_categories .csv` | Category label reference for the BII dataset. |
| `data/tableau_images/` | Screenshots of Tableau Online UI used in notebook 03. |
| `data/story_images/` | Visualization critique images used in breakout 02. |
| `resources/` | PDFs and cheatsheets: Grammar of Graphics, Visual Display of Quantitative Information, Matplotlib/Seaborn/Pandas cheatsheets. |
| `DASH_Plotly/dash_intro.py` | Standalone Dash application demonstrating the layout-and-callback pattern from notebook 04. Run as a Python script, not in Jupyter. |

---

## Workflow Diagram

```
01_visualization_principles_matplotlib_seaborn.ipynb
    |-- visualization theory (Part 1)
    |-- matplotlib (Part 2)
    |-- seaborn (Part 3)
    |
    v
02_one_chart_several_libraries.ipynb
    |-- data types review (Part 0)
    |-- pandas / matplotlib / seaborn / plotnine comparison (Part 1)
    |-- plotly / altair interactive charts (Part 2)
    |-- static vs interactive vs 3D (Part 3)
    |
    +-----> 03_tableau_and_zero_code_visualization.ipynb
    |           (zero-code track - no Python required for Parts 0-1)
    |
    v
04_plotly_dash_dashboards.ipynb
    |-- when interactivity helps (Part 0)
    |-- plotly box + scatter + heatmap (Part 1)
    |-- dash layout and callbacks (Part 2)
```

Breakout exercises in `breakouts/` are practice problems keyed to each notebook. Complete `breakout_01_matplotlib.ipynb` after notebook 01, `breakout_02_multi_library.ipynb` after notebook 02, and `breakout_03_interactive_dashboards.ipynb` after notebook 04.

---

## Step-by-Step Walkthrough

**Notebook 01 - Visualization Principles, Matplotlib, and Seaborn**

Start here. Part 1 builds the mental model: why do humans visualize data at all, and what does it mean for a visualization to be honest or misleading? The historical examples are not decoration - each one illustrates a failure mode or a design principle that still appears in modern dashboards. Part 2 introduces Matplotlib through its object-oriented hierarchy rather than the procedural API. The object-oriented approach takes more code upfront but scales to complex multi-axes figures without ambiguity about which axes is being modified. Part 3 shows Seaborn, which sits on top of Matplotlib and handles common statistical chart types with a DataFrame-aware API.

**Notebook 02 - One Chart Across Several Libraries**

This notebook exists to answer the most common question a new data scientist has: "which library should I use?" Rather than answering abstractly, it produces the same four chart types in Pandas, Matplotlib, Seaborn, and Plotnine, making the trade-offs visible. Part 2 adds Plotly and Altair for interactive work. The Grammar of Graphics section explains why Plotnine and Altair have a fundamentally different API than Matplotlib - they separate data from geometry from aesthetics rather than building charts from drawing primitives.

**Notebook 03 - Tableau and Zero-Code Visualization**

Tableau addresses a different audience than the Python notebooks: analysts and stakeholders who need self-service dashboards, not reproducible code artifacts. This notebook explains when to reach for Tableau rather than Python, then walks through the Tableau Online UI. Part 1.3 covers TabPy, which bridges Tableau and Python when you need Python's modeling power inside a Tableau workbook.

**Notebook 04 - Plotly and Dash**

This notebook goes deeper on Plotly than notebook 02 and adds Dash, Plotly's dashboard framework. The key concept in Part 2 is the callback model: an `@app.callback` function is a Python function that Dash calls whenever the user changes a control component. Understanding this pattern unlocks every Dash feature - multiple inputs, chained callbacks, server-side caching.

---

## How to Run

```bash
git clone <this-repo>
cd Visual_Types_and_Data_Visualization
pip install -r requirements.txt
jupyter notebook
```

Open any of the four notebooks in the root directory. Run cells from top to bottom after a clean kernel restart. All file paths in notebooks are relative to the repo root.

To run the standalone Dash application:

```bash
python DASH_Plotly/dash_intro.py
# open http://127.0.0.1:8050 in a browser
```

---

## Key Concepts Glossary

**Artist (Matplotlib):** Any object that renders something visible in a figure: lines, text, tick labels, patches. Artists are tied to an Axes object and cannot be shared across figures.

**Axes (Matplotlib):** The actual plot area with x/y coordinate systems, tick marks, and labels. A Figure can contain multiple Axes. Do not confuse with "axis" (a single x or y dimension).

**Figure (Matplotlib):** The top-level container for all plot elements. Corresponds to the window or page. Contains one or more Axes objects.

**Grammar of Graphics:** A layered framework for describing charts as compositions of data, geometric objects (geoms), and aesthetic mappings (color, shape, size). The basis for ggplot2 (R), Plotnine, and Altair.

**FacetGrid (Seaborn):** A class that creates a grid of axes, one per unique value of a column. Automates the creation of small multiples - the same chart repeated for each subset of data.

**Callback (Dash):** A Python function decorated with `@app.callback` that Dash invokes whenever an `Input` component changes. Returns new content for one or more `Output` components. The mechanism behind Dash interactivity.

**Filter Action (Tableau):** A configuration in a Tableau Dashboard that connects two sheets: clicking a mark in the source sheet filters the marks displayed in the target sheet.

**TabPy:** Tableau's Python server. Allows Tableau calculated fields to call Python functions by sending data to the TabPy server and returning results as a column.

**Nominal data:** Categories with no inherent order (species, country, department). Encode with color hue or shape, never with a continuous color scale that implies magnitude.

**Ordinal data:** Categories with a meaningful order but no consistent spacing (low/medium/high, Likert scales). Encode with ordered color scales or position on an axis where spacing is not misread as quantitative.

---

## Further Reading

- *The Grammar of Graphics* - formal specification of the visualization framework underlying Plotnine and Altair (copy in `resources/`)
- *The Visual Display of Quantitative Information* - Tufte's canonical text on data-ink ratio and chart clarity (copy in `resources/`)
- *Design for Information* - broader survey of information design with historical examples
- *Storytelling with Data* - practitioner guide to communicating with charts in business settings
- Matplotlib documentation: https://matplotlib.org/stable/
- Seaborn documentation: https://seaborn.pydata.org/
- Plotly documentation: https://plotly.com/python/
- Dash documentation: https://dash.plotly.com/
- Altair documentation: https://altair-viz.github.io/
- Tableau training: https://www.tableau.com/learn/training

---

## Credits and Acknowledgements

Visualization principles and historical examples draw from Leland Wilkinson's *The Grammar of Graphics*, Edward Tufte's *The Visual Display of Quantitative Information*, and the curriculum of the Data Visualization Techniques course materials (CS 448B). Nicolas P. Rougier's Matplotlib tutorial is the basis for portions of the Matplotlib section.

<hr style="border: 2px solid#003262;" />

## Contact

<div align="center">
  <img src="images/thumbnails/ehcastroh_teach_banner_flower.png" alt="ehcastroh" width="90" style="border-radius: 50%;" />

  <sub>ehcastroh</sub>

  <a href="https://github.com/ehcastroh">GitHub</a> · <a href="https://www.linkedin.com/in/ehcastroh/">LinkedIn</a>
</div>
