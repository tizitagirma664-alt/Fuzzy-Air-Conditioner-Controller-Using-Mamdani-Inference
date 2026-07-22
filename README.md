# Fuzzy Air Conditioner Controller

A from-scratch Mamdani fuzzy expert system that determines an air conditioner's fan speed and cooling power from room temperature and relative humidity readings.

The project is provided as a self-contained Jupyter notebook. It implements the membership functions, fuzzy rules, inference engine, visualizations, interactive controls, examples, and tests without using an external fuzzy-logic library.

## Features

- Accepts temperature from `10` to `40` degrees Celsius.
- Accepts relative humidity from `0` to `100%`.
- Produces fan-speed and cooling-power recommendations from `0` to `100%`.
- Implements triangular and trapezoidal membership functions from scratch.
- Uses a complete nine-rule temperature-by-humidity rule base.
- Applies MIN for fuzzy AND and implication, MAX for aggregation, and centroid defuzzification.
- Explains which rules fired and their firing strengths.
- Generates membership-function, control-surface, and worked-example plots.
- Includes an interactive `ipywidgets` demonstration.
- Includes ten example scenarios and eight unit tests.

## Fuzzy Model

| Variable | Range | Linguistic terms |
| --- | ---: | --- |
| Temperature | 10–40 degrees Celsius | cold, warm, hot |
| Humidity | 0–100% | dry, normal, humid |
| Fan speed | 0–100% | low, medium, high |
| Cooling power | 0–100% | low, medium, high |

The inference process follows five stages:

1. Fuzzify the temperature and humidity inputs.
2. Evaluate each rule using the MIN operator.
3. Clip each output membership function at the rule's firing strength.
4. Aggregate the rule outputs using the MAX operator.
5. Defuzzify the result using the centroid method.

## Rule Base

| Temperature | Humidity | Fan speed | Cooling power |
| --- | --- | --- | --- |
| Cold | Dry | Low | Low |
| Cold | Normal | Low | Low |
| Cold | Humid | Medium | Low |
| Warm | Dry | Medium | Medium |
| Warm | Normal | Medium | Medium |
| Warm | Humid | High | Medium |
| Hot | Dry | Medium | High |
| Hot | Normal | High | High |
| Hot | Humid | High | High |

## Project Structure

```text
.
├── README.md
└── prism-uploads/
    └── Fuzzy_AC_Controller (1).ipynb
```

When the notebook runs, it creates an `outputs/` directory containing:

- `test_results.csv`
- `membership_functions.png`
- `control_surface.png`
- `worked_example.png`

## Requirements

- Python 3
- Jupyter Notebook or JupyterLab
- NumPy
- pandas
- Matplotlib
- ipywidgets

The core fuzzy inference system itself uses only Python's standard library; the additional packages support tabular results, plots, and notebook interaction.

## Running the Project

Start Jupyter from the project directory:

```bash
jupyter lab
```

Open `Fuzzy_AC_Controller (1).ipynb`, then select **Run All Cells**. The notebook is organized to run from top to bottom.

If the interactive sliders are unavailable, install or enable `ipywidgets` in the Jupyter environment and rerun the interactive-demo cell.

## Example

For a temperature of `27` degrees Celsius and humidity of `85%`, the notebook produces approximately:

```text
Fan speed:       83.0%
Cooling power:   57.1%
```

The explanation trace shows that the warm-and-humid and hot-and-humid rules contribute to this result.

## Testing

Run the notebook's final unit-test section to test membership-function boundaries, output ranges, expected cold/dry and hot/humid behavior, and deterministic inference. The notebook also evaluates ten labeled operating scenarios and exports their results to CSV.

## Notes

- Inputs are intended to remain within the model's defined temperature and humidity ranges.
- Output smoothness depends on the discretization resolution used for centroid defuzzification; the default is 401 points.
- This controller is an educational fuzzy-logic demonstration, not a production HVAC control system.

## Author

Tizita Girma  
MSIT5205 — Advanced Artificial Intelligence, Assignment II (Track C: Fuzzy Expert System)
