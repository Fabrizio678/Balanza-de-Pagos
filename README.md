# Balance of Payments — Peru (BCRP)

Analysis of Peru's Balance of Payments (2016–2025) using BCRP data. Beamer slide deck + Jupyter notebook.

## Project Structure

```
Balanza de Pagos/
├── data/                        # Source data (CSV)
│   └── Balanza_de_Pagos.csv
├── img/                         # Charts, tables, logos
│   ├── grafico_*.png            # Charts (6)
│   ├── tabla_*.png              # APA-formatted tables (7)
│   └── ucsur.png                # University logo
├── notebooks/
│   └── analisis.ipynb           # Data analysis & figure generation
├── main.tex                     # Beamer slide deck
├── main.pdf                     # Compiled presentation
├── requirements.txt
├── .gitignore
└── README.md
```

## Presentation (`main.tex`)

Beamer slide deck (`aspectratio=169`, `metropolis` theme). Compile with:

```
pdflatex main.tex        # run twice for ToC
```

Dependencies: `metropolis`, `tikz`, `booktabs`, `xcolor`, `amsmath`.

Images resolved from `img/` via `\graphicspath{{img/}{./}}`. The `\grafico{}` command renders a placeholder if the referenced PNG is missing.

## Dataset Variables

27 series from Peru's Balance of Payments (2016–2026), in millions of US$.

### Current Account

| Variable | Description |
|----------|-------------|
| `CC_Bienes_Export` | Goods exports |
| `CC_Bienes_Import` | Goods imports |
| `CC_Bienes` | Net goods balance = Exports - Imports |
| `CC_Servicios_Export` | Services exports |
| `CC_Servicios_Import` | Services imports |
| `CC_Servicios` | Net services balance = Exports - Imports |
| `CC_Ingreso_Primario_Pub` | Primary income — public sector |
| `CC_Ingreso_Primario_Priv` | Primary income — private sector |
| `CC_Ingreso_Primario` | Total primary income = Public + Private |
| `CC_Remesas` | Remittances (secondary income component) |
| `CC_Ingreso_Secundario` | Secondary income (includes remittances) |
| `Cuenta_Corriente` | = CC_Bienes + CC_Servicios + CC_Ingreso_Primario + CC_Ingreso_Secundario |

### Financial Account

Sign convention (BCRP, MBPI6):
- **Negative CF** = capital inflow (net increase in external liabilities)
- **Positive CF** = capital outflow (net increase in external assets)

| Variable | Description |
|----------|-------------|
| `CF_SectorPrivado_Activos` | Private sector assets |
| `CF_SectorPrivado_Pasivos` | Private sector liabilities |
| `CF_SectorPrivado` | Net private sector = Assets - Liabilities |
| `CF_SectorPublico_Activos` | Public sector assets |
| `CF_SectorPublico_Pasivos` | Public sector liabilities |
| `CF_SectorPublico` | Net public sector = Assets - Liabilities |
| `CF_CortoPlazo_Activos` | Short-term assets |
| `CF_CortoPlazo_Pasivos` | Short-term liabilities |
| `CF_CortoPlazo` | Net short-term = Assets - Liabilities |
| `Cuenta_Financiera` | = CF_Sector_Privado + CF_SectorPublico + CF_CortoPlazo |

### Result and RIN

| Variable | Description |
|----------|-------------|
| `Resultado_BP` | Balance of Payments result |
| `Errores_Omisiones` | Net errors and omissions |
| `Financ_Excepcional` | Exceptional financing |
| `Efecto_Valuacion` | RIN valuation effect |
| `Var_Saldo_RIN` | Change in RIN balance |

### Key Formulas

```
Cuenta_Corriente = CC_Bienes + CC_Servicios + CC_Ingreso_Primario + CC_Ingreso_Secundario

CF_SectorPrivado  = CF_SectorPrivado_Activos - CF_SectorPrivado_Pasivos
CF_SectorPublico  = CF_SectorPublico_Activos - CF_SectorPublico_Pasivos
CF_CortoPlazo     = CF_CortoPlazo_Activos - CF_CortoPlazo_Pasivos
Cuenta_Financiera = CF_Sector_Privado + CF_SectorPublico + CF_CortoPlazo

Resultado_BP      = Cuenta_Corriente - Cuenta_Financiera + Errores_Omisiones + Financ_Excepcional
Var_Saldo_RIN     = Resultado_BP + Efecto_Valuacion
```

## Requirements

```
pandas>=2.0
numpy>=1.24
matplotlib>=3.7
openpyxl>=3.1
```

## Usage

```bash
python -m venv venv
.\venv\Scripts\activate      # Windows
pip install -r requirements.txt
jupyter notebook notebooks/analisis.ipynb
```

Images are generated in `img/` when running the notebook.

## Source

[BCRP — Estadísticas](https://www.bcrp.gob.pe/estadisticas.html)
