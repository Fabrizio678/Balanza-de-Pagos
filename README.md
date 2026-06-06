# Balance of Payments - BCRP

Analysis of Peru's Balance of Payments using data from BCRP (Central Reserve Bank of Peru).

## Project Structure

```
Balanza de Pagos/
├── assets/
│   └── Balanza_de_Pagos.csv    # Source data (ISO-8859-1)
├── output/
│   ├── tables/                  # APA-formatted tables (PNG)
│   │   ├── tabla_1_resumen_bp.png
│   │   ├── tabla_2_componentes_cc.png
│   │   ├── tabla_3_desglose_bienes_servicios.png
│   │   ├── tabla_4_ingreso_primario_secundario.png
│   │   ├── tabla_5_componentes_cf.png
│   │   ├── tabla_6_activos_pasivos_sector.png
│   │   └── tabla_7_resultado_bp_rin.png
│   └── graph/                   # Charts (PNG)
│       ├── grafico_1_resumen_bp_apilado.png
│       ├── grafico_2_balanza_comercial_servicios.png
│       ├── grafico_3_ingreso_primario_secundario.png
│       ├── grafico_4_cf_componentes.png
│       ├── grafico_5_activos_pasivos_sector.png
│       └── grafico_6_resultado_bp_rin.png
├── analisis.ipynb               # Main notebook
├── requirements.txt             # Dependencies
├── README.md
└── .gitignore
```

## Dataset Variables

The dataset contains 27 series from Peru's Balance of Payments (2016–2026), in millions of US$.

### Current Account

| Variable | Description |
|----------|-------------|
| `CC_Bienes_Export` | Goods exports |
| `CC_Bienes_Import` | Goods imports |
| `CC_Bienes` | Net goods balance = Exports - Imports |
| `CC_Servicios_Export` | Services exports |
| `CC_Servicios_Import` | Services imports |
| `CC_Servicios` | Net services balance = Exports - Imports |
| `CC_Ingreso_Primario_Pub` | Primary income - public sector |
| `CC_Ingreso_Primario_Priv` | Primary income - private sector |
| `CC_Ingreso_Primario` | Total primary income = Public + Private |
| `CC_Remesas` | Remittances (secondary income component) |
| `CC_Ingreso_Secundario` | Secondary income (includes remittances) |
| `Cuenta_Corriente` | = CC_Bienes + CC_Servicios + CC_Ingreso_Primario + CC_Ingreso_Secundario |

### Financial Account

**BCRP sign convention:**
- **Positive CF** = increase in net external assets (capital outflow)
- **Negative CF** = increase in net external liabilities (capital inflow)

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

CF_SectorPrivado   = CF_SectorPrivado_Activos - CF_SectorPrivado_Pasivos
CF_SectorPublico   = CF_SectorPublico_Activos - CF_SectorPublico_Pasivos
CF_CortoPlazo      = CF_CortoPlazo_Activos - CF_CortoPlazo_Pasivos
Cuenta_Financiera  = CF_Sector_Privado + CF_SectorPublico + CF_CortoPlazo

Resultado_BP       = Cuenta_Corriente - Cuenta_Financiera + Errores_Omisiones + Financ_Excepcional
Var_Saldo_RIN      = Resultado_BP + Efecto_Valuacion
```

**Note:** The Balance of Payments result SUBTRACTS the Financial Account because BCRP records CF as negative when there is capital inflow. Subtracting a negative value is equivalent to adding the net capital inflow.

## Tables (output/tables/)

| File | Content |
|---------|-----------|
| `tabla_1_resumen_bp.png` | Balance of Payments summary: CC, FA, EO, EF, BP Result |
| `tabla_2_componentes_cc.png` | Current Account components: Goods, Services, Income |
| `tabla_3_desglose_bienes_servicios.png` | Goods and Services breakdown: Exports, Imports, Net balance |
| `tabla_4_ingreso_primario_secundario.png` | Primary Income (Public, Private) and Secondary Income (Remittances) |
| `tabla_5_componentes_cf.png` | Financial Account components by sector |
| `tabla_6_activos_pasivos_sector.png` | Assets and Liabilities broken down by sector |
| `tabla_7_resultado_bp_rin.png` | BP Result, Valuation Effect and RIN Variation |

Tables follow **APA 7th edition** format: horizontal lines only (top, below header, bottom), serif font (Times New Roman), bold headers, centered numerical values, year as integer.

## Charts (output/graph/)

| File | Content |
|---------|-----------|
| `grafico_1_resumen_bp_apilado.png` | Stacked bars of CC, FA, EO, EF + BP Result line |
| `grafico_2_balanza_comercial_servicios.png` | Trade and Services balance (Exports, Imports, Balance) |
| `grafico_3_ingreso_primario_secundario.png` | Primary Income (Public, Private, Total) and Secondary + Remittances |
| `grafico_4_cf_componentes.png` | Stacked bars of FA by sector + net FA line |
| `grafico_5_activos_pasivos_sector.png` | Assets vs Liabilities by sector (3 panels) |
| `grafico_6_resultado_bp_rin.png` | BP Result, Valuation Effect and RIN Variation |

All charts include a footnote: *"Own elaboration with data from BCRP."*

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
jupyter notebook analisis.ipynb
```

Images are automatically generated in `output/tables/` and `output/graph/` when running the notebook.

## Source

[BCRP - Estadísticas](https://www.bcrp.gob.pe/estadisticas.html)
