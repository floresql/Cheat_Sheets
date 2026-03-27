# Marimo Cheat Sheet: Reactive Python Notebooks

### 1. Installation & Getting Started
`marimo` is a reactive notebook that stores everything as a pure Python (`.py`) file.

```bash
# Install marimo
pip install marimo

# Create a new notebook or edit an existing one
marimo edit

# Edit a specific file
marimo edit notebook.py

# Run a notebook as a shared web app
marimo run notebook.py

# Convert a Jupyter notebook to marimo
marimo convert your_notebook.ipynb > notebook.py
```

---

### 2. Basic Markdown & Layout
Use `mo.md` to create rich text. You can interpolate Python variables directly into the strings.

```python
import marimo as mo

# Basic Markdown
mo.md("# Hello Marimo!")

# Dynamic Markdown with Python variables
name = "User"
mo.md(f"Welcome back, **{name}**!")

# Layout: Horizontal and Vertical stacks
mo.hstack([
    mo.md("Left Column"),
    mo.md("Right Column")
])

mo.vstack([
    mo.md("Top Row"),
    mo.md("Bottom Row")
])
```

---

### 3. Interactive UI Elements
Marimo's reactivity means when you move a slider, all dependent cells automatically update.

```python
# Sliders and Numeric Inputs
slider = mo.ui.slider(start=0, stop=100, value=50, label="Select Value")

# Text and Dropdowns
text_input = mo.ui.text(label="Enter Name")
dropdown = mo.ui.dropdown(options=["Option A", "Option B"], label="Choose")

# Accessing values (reactive)
mo.md(f"The slider is at: {slider.value}")

# Displaying elements (must be the last line in a cell to show)
mo.hstack([slider, text_input, dropdown])
```

---

### 4. Data & Tables
Built-in tools for exploring DataFrames and structured data.

```python
import pandas as pd
df = pd.read_csv("data.csv")

# Interactive Table (allows sorting/filtering)
table = mo.ui.table(df, selection="multiple")

# Get selected rows from the table
selected_data = table.value

# Dataframe Transformer (GUI for cleaning data)
transformer = mo.ui.dataframe_transformer(df)
```

---

### 5. Media & Plots
Displaying images, plots, and other media types.

```python
# Displaying Plots (Matplotlib/Seaborn/Plotly)
import matplotlib.pyplot as plt
plt.plot([1, 2, 3], [4, 5, 6])
mo.as_html(plt.gca()) # Wrap plots for best rendering

# Images and Audio
mo.image("path/to/image.png", width=200)
mo.audio("path/to/audio.mp3")

# Mermaid Diagrams
mo.mermaid('''
graph TD
    A[Start] --> B{Is it reactive?}
    B -- Yes --> C[Use marimo]
    B -- No --> D[Use Jupyter]
''')
```

---

### 6. Control Flow & Utility
Tools to manage the reactive execution of your notebook.

```python
# Stop execution if a condition is met
mo.stop(slider.value == 0, "Please move the slider to continue.")

# Display a status spinner for long tasks
with mo.status.spinner(title="Calculating..."):
    # Expensive code here
    pass

# Display statistics
mo.stat(value="98%", label="Accuracy", caption="Model Performance")
```
