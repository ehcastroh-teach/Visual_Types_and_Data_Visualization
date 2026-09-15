<hr style="border: 6px solid#003262;" />

<div align="center">
    <img src="./images/thumbnails/ehcastroh_teach_banner_flower.png" align="center" width="20%" />
</div>

<br>

# Introduction to Data Visualization

A four-notebook series covering the theory and practice of data visualization, from foundational principles through Python charting libraries, zero-code tools (Tableau), and interactive dashboards (Plotly and Dash). Each notebook explains not just how to build a chart but why a particular design choice, library, or API structure leads to clearer, more honest communication. Built for self-learners who want both a principled mental model and practical, reproducible skills.

---

## Learning Objectives

By completing this series, a learner will be able to:

- Articulate why humans create visualizations and apply Tufte's five design principles to evaluate or improve any chart.
- Explain how a plot is computationally structured - data, mappings, geometric objects, aesthetics, and guides - using the vocabulary introduced in notebook 01.
- Produce line, scatter, box, and histogram charts in Matplotlib and Seaborn using the object-oriented API.
- Build the same chart across Pandas, Matplotlib, Seaborn, Plotnine, Plotly, and Altair, and articulate the trade-off each library makes between expressiveness and concision.
- Explain the Grammar of Graphics framework and why Plotnine and Altair have a fundamentally different API design than Matplotlib.
- Build interactive Plotly charts with hover, zoom, and linked selections, and turn them into a running Dash web application.
- Decide when to reach for a zero-code tool like Tableau rather than a Python library, based on audience, deployment, and iteration constraints.
- Navigate Tableau Online to connect data, create worksheets, combine them into a dashboard, and configure a Filter Action.
- Critique a real-world chart using the good / bad / better framework and redesign it.

---

## Data / File Dictionary

| File or Directory | Description |
|---|---|
| `01_visualization_principles_matplotlib_seaborn.ipynb` | Main notebook: visualization theory (Part 1), Matplotlib object-oriented API (Part 2), Seaborn statistical charts (Part 3). |
| `02_one_chart_several_libraries.ipynb` | Main notebook: data type review (Part 0), same four chart types across Pandas / Matplotlib / Seaborn / Plotnine (Part 1), Plotly and Altair interactive charts (Part 2), static vs. interactive vs. 3D comparison (Part 3). |
| `03_tableau_and_zero_code_visualization.ipynb` | Main notebook: when to use a zero-code tool (Part 0), Tableau Online worksheets and dashboards (Part 1.1-1.2), TabPy bridge to Python (Part 1.3). |
| `04_plotly_dash_dashboards.ipynb` | Main notebook: static vs. interactive decision guide (Part 0), Plotly box / scatter / heatmap on the BII dataset (Part 1), Dash layout and callback model (Part 2). |
| `visualization_principles_matplotlib_seaborn_homework.ipynb` | Take-home exercises keyed to notebook 01. |
| `one_chart_several_libraries_homework.ipynb` | Take-home exercises keyed to notebook 02. |
| `tableau_and_zero_code_visualization_homework.ipynb` | Take-home exercises keyed to notebook 03. |
| `plotly_dash_dashboards_homework.ipynb` | Take-home exercises keyed to notebook 04. |
| `breakouts/S1/breakout_01_matplotlib.ipynb` | Breakout exercise: reproduce a multi-line stock chart with a secondary y-axis using Matplotlib. |
| `breakouts/S2/breakout_02_multi_library.ipynb` | Breakout exercise: identify Tufte violations in a given chart, recreate it, then produce an improved version. |
| `breakouts/S3/breakout_03_interactive_dashboards.ipynb` | Breakout exercise: apply the good / bad / better framework to a real-world chart and redesign it in Plotly. |
| `DASH_Plotly/dash_intro.py` | Standalone Dash application demonstrating the layout-and-callback pattern from notebook 04. Run as a plain Python script, not inside Jupyter. |
| `data/Iris.csv` | Fisher's Iris dataset - 150 samples, 4 numeric features, 1 species label. Primary dataset for chart examples in notebooks 01 and 02. |
| `data/bii_data_w_categories.csv` | Behavioral Intelligence Index (BII) survey scores with department category labels - 8 trait features and 1 composite score. Used in notebooks 02 and 04 and in `dash_intro.py`. |
| `data/bii_data.csv` | BII survey scores without category labels. |
| `data/bii_categories .csv` | Category label reference for the BII dataset. |
| `data/tableau_images/` | UI screenshots from Tableau Online, embedded in notebook 03. |
| `data/story_images/` | Visualization critique images used in breakout 02. |
| `resources/` | PDFs and cheatsheets: Grammar of Graphics, Visual Display of Quantitative Information, Matplotlib / Seaborn / Pandas quick references. |
| `requirements.txt` | Pinned minimum versions for all Python dependencies. |

---

## Workflow Diagram

```
01_visualization_principles_matplotlib_seaborn.ipynb
    |-- Part 1: visualization theory and Tufte's principles
    |-- Part 2: Matplotlib object-oriented API
    |-- Part 3: Seaborn statistical chart types
    |
    v
02_one_chart_several_libraries.ipynb
    |-- Part 0: data type review (nominal, ordinal, quantitative)
    |-- Part 1: four chart types across Pandas / Matplotlib / Seaborn / Plotnine
    |-- Part 2: Plotly and Altair interactive charts
    |-- Part 3: static vs. interactive vs. 3D
    |
    +-----> 03_tableau_and_zero_code_visualization.ipynb
    |           (zero-code parallel track - no Python required for Parts 0 and 1.1-1.2)
    |           |-- Part 0: when to use a zero-code tool
    |           |-- Part 1.1: navigating Tableau Online
    |           |-- Part 1.2: building a Tableau dashboard
    |           |-- Part 1.3: TabPy - calling Python from Tableau
    |
    v
04_plotly_dash_dashboards.ipynb
    |-- Part 0: when interactivity helps vs. hurts
    |-- Part 1: Plotly box, scatter, and heatmap on BII data
    |-- Part 2: Dash layout and callback model
         |
         v
    DASH_Plotly/dash_intro.py   (standalone running app)

Breakout exercises (run after the indicated notebook):
    breakouts/S1/breakout_01_matplotlib.ipynb    -- after notebook 01
    breakouts/S2/breakout_02_multi_library.ipynb -- after notebook 02
    breakouts/S3/breakout_03_interactive_dashboards.ipynb -- after notebook 04
```

---

## Step-by-Step Walkthrough

**Notebook 01 - Visualization Principles, Matplotlib, and Seaborn**

Start here regardless of prior experience. Part 1 builds the mental model: why do humans create visualizations at all, and what makes one chart more honest or effective than another? The historical case studies - the Challenger o-ring data, John Snow's cholera map, Galileo's moon drawings - are not decoration. Each one demonstrates a failure mode or a design principle that appears repeatedly in modern dashboards and business charts. Tufte's five principles (reveal data, add detail to clarify, invite comparison, make distinctions as subtle as possible but still clear, above all show the data) provide a checklist that applies to every chart you will build in the rest of the series.

Part 2 introduces Matplotlib through its object-oriented hierarchy - Figure, Axes, Artist - rather than the procedural `plt.*` API. The object-oriented approach takes slightly more code to set up but scales without ambiguity to multi-axes figures, subplots, and custom layouts. The procedural API becomes fragile when more than one axes is involved because it relies on a global current-axes pointer that changes implicitly. Part 3 covers Seaborn, which wraps Matplotlib with a DataFrame-aware API for common statistical chart types and handles things like FacetGrid (small multiples) with far less boilerplate.

**Notebook 02 - One Chart Across Several Libraries**

This notebook is organized around the question every new data scientist eventually asks: "which visualization library should I use?" Rather than answering it abstractly, the notebook produces four chart types (line, scatter, box, histogram) in Pandas, Matplotlib, Seaborn, and Plotnine side by side. The trade-offs become visible in the code itself: Pandas charts are the shortest but least customizable; Matplotlib is the most flexible but most verbose; Seaborn abstracts the statistical layer; Plotnine translates the Grammar of Graphics into Python.

Part 0 reviews data types (nominal, ordinal, quantitative) because the correct chart encoding depends on the type of data being mapped. Encoding an ordinal variable with a continuous color gradient, for example, implies that the gaps between levels are equal when they may not be. Part 2 adds Plotly and Altair, both of which produce browser-native interactive output. The Altair section specifically demonstrates linked selections: brushing a region in one chart automatically filters a second chart connected to the same data, which is the core pattern behind exploratory dashboards.

**Notebook 03 - Tableau and Zero-Code Visualization**

Tableau is not a replacement for Python libraries; it is a different tool for a different audience and deployment context. This notebook explains the decision: reach for Tableau when the primary consumer is a business stakeholder who needs to filter or explore data themselves, when the dashboard will be refreshed on a schedule against a live database, or when iteration speed matters more than code reproducibility. Reach for Python when the analysis requires custom logic, reproducible code artifacts, or integration with a modeling pipeline.

Part 1.1 covers the Tableau Online UI: how workbooks, worksheets, and dashboards relate to one another, and how to connect to a data source. Part 1.2 walks through building a dashboard by arranging multiple worksheets on a canvas and connecting them with a Filter Action - clicking a mark in one sheet filters the data shown in another. Part 1.3 introduces TabPy, which lets Tableau calculated fields call Python functions by sending data to a local TabPy server and returning results as a computed column. This is the bridge to use when you need Python's modeling power inside a Tableau workbook.

**Notebook 04 - Plotly and Dash**

This notebook goes deeper on Plotly than notebook 02 by working with the BII survey dataset - a real multi-feature dataset with department categories - and building box plots, scatter charts, and a correlation heatmap. The goal is to practice choosing chart types based on the question being answered, not just on habit.

Part 2 introduces Dash, Plotly's dashboard framework for Python. The key concept is the callback model: a Python function decorated with `@app.callback` is registered with the Dash server and called automatically whenever a user changes an input component (dropdown, slider, radio button). The function returns a new figure or value that updates the corresponding output component in the browser - with no JavaScript required. Understanding this reactive pattern - Input triggers, Output receives - unlocks every Dash feature: multiple inputs, chained callbacks, server-side caching. The `DASH_Plotly/dash_intro.py` file in this repo is a minimal but complete working application to read alongside the notebook.

---

## How to Run

Prerequisites: [Nix](https://nixos.org/download) with flakes enabled. `flake.nix` provides
Python and `uv` in a project-local devShell - nothing is installed system-wide.

```bash
git clone https://github.com/ehcastroh-teach/Visual_Types_and_Data_Visualization.git
cd Visual_Types_and_Data_Visualization

# Enter the project's dev shell - this also runs `uv sync` automatically
# the first time, creating .venv with every pinned dependency installed
nix develop

uv run jupyter notebook
```

Open any of the four main notebooks in the root directory. Run all cells from top to bottom after a clean kernel restart (`Kernel > Restart & Run All`). All file paths inside notebooks are relative to the repo root, so keep the working directory at the repo root when launching Jupyter.

**Note on Tableau (notebook 03):** Tableau Online requires a free trial or licensed account. The notebook can be read and the Python-side concepts followed without an active account, but the UI walkthrough sections require browser access to Tableau Online.

**Note on TabPy (notebook 03, Part 1.3):** TabPy is optional and must be installed separately:

```bash
uv add tabpy-server
```

**Note on k3d (3D charts, notebook 02):** k3d requires JupyterLab and ipywidgets and is not included in `pyproject.toml`:

```bash
uv add k3d
```

To run the standalone Dash application:

```bash
uv run python DASH_Plotly/dash_intro.py
# then open http://127.0.0.1:8050 in a browser
```

Note: `dash_intro.py` uses Dash 1.x import style (`dash_core_components`, `dash_html_components`). If you have Dash 2.x installed, update the imports at the top of the file to `from dash import dcc, html` before running.

---

## Key Concepts Glossary

**Figure (Matplotlib):** The top-level container for all plot elements. Corresponds to the window or the page. A Figure contains one or more Axes objects.

**Axes (Matplotlib):** The actual plot area - the region with x/y coordinate systems, tick marks, and labels. Do not confuse with "axis" (a single x or y dimension). A Figure can contain multiple Axes arranged in a grid or at arbitrary positions.

**Artist (Matplotlib):** Any object that renders something visible inside a Figure: lines, patches, text, tick labels, images. Artists are attached to an Axes object.

**Grammar of Graphics:** A layered framework that describes a chart as a composition of data, geometric objects (geoms), and aesthetic mappings (color, size, shape, position). The basis for ggplot2 in R, and for Plotnine and Altair in Python. Separating data from geometry from aesthetics makes chart specifications declarative and composable.

**FacetGrid (Seaborn):** A class that creates a grid of Axes, one per unique value of a grouping column. Automates the creation of small multiples - the same chart type repeated for each data subset - without manual iteration.

**Nominal data:** Categorical values with no inherent order (species, country, department). Map to color hue or shape. Never encode nominal data with a sequential or diverging color scale, which would imply a magnitude or direction that does not exist.

**Ordinal data:** Categorical values with a meaningful order but no guaranteed equal spacing between levels (low / medium / high, Likert-scale responses). Map to ordered color scales or axis positions where the spacing will not be misread as quantitative.

**Linked selection (Altair):** An interactive behavior where brushing or clicking a region in one chart automatically filters or highlights the same records in one or more other charts bound to the same data source. The core mechanism of exploratory dashboards.

**Callback (Dash):** A Python function decorated with `@app.callback` that Dash calls automatically whenever a registered Input component changes. The function receives the new Input values as arguments and returns new content for one or more Output components. All interactivity in a Dash application is expressed as callbacks.

**Filter Action (Tableau):** A dashboard configuration that connects two sheets - clicking a mark in the source sheet filters the marks visible in the target sheet. The Tableau equivalent of linked selection.

**TabPy:** Tableau's open-source Python server. Allows Tableau calculated fields to call Python functions by sending column data to the TabPy process and returning a computed result column. Used when Python's modeling or statistical capabilities are needed inside a Tableau workbook.

**Data-ink ratio (Tufte):** The proportion of a chart's ink that is devoted to displaying data, as opposed to decorative elements, redundant labels, or heavy gridlines. Tufte's principle is to maximize this ratio - remove everything that does not carry information the reader needs.

**Small multiples:** A design technique in which the same chart type is repeated once per category or time period and arranged in a grid, allowing direct comparison across panels without overloading a single chart with color or line style encodings.

---

## Further Reading

- *The Grammar of Graphics* - formal specification of the visualization framework underlying Plotnine and Altair (copy in `resources/`)
- *The Visual Display of Quantitative Information* - canonical text on data-ink ratio, chart clarity, and graphical integrity (copy in `resources/`)
- *Design for Information* - broad survey of information design with historical examples across many domains
- *Storytelling with Data* - practitioner guide to communicating with charts in business and presentation contexts
- Matplotlib documentation: https://matplotlib.org/stable/
- Seaborn documentation: https://seaborn.pydata.org/
- Plotly Python documentation: https://plotly.com/python/
- Dash documentation: https://dash.plotly.com/
- Altair documentation: https://altair-viz.github.io/
- Tableau training videos: https://www.tableau.com/learn/training
- Visual Vocabulary (Financial Times chart selection guide): https://ft.com/vocabulary

---

## Credits and Acknowledgements

Visualization principles and historical examples draw from Leland Wilkinson's *The Grammar of Graphics*, Edward Tufte's *The Visual Display of Quantitative Information*, and publicly available Data Visualization Techniques course materials. Portions of the Matplotlib section are based on Nicolas P. Rougier's Matplotlib tutorial. The Iris dataset is Fisher's classic 1936 dataset distributed via UCI Machine Learning Repository.

---

## Contact

<div align="center">
  <img src="images/thumbnails/ehcastroh_teach_banner_flower.png" alt="ehcastroh" width="90" style="border-radius: 50%;" />

  <sub>ehcastroh</sub>

  <a href="https://github.com/ehcastroh">GitHub</a> · <a href="https://www.linkedin.com/in/ehcastroh/">LinkedIn</a>
</div>
