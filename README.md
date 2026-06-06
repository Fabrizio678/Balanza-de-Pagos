# Balanza de Pagos - BCRP

Análisis de la Balanza de Pagos del Perú usando datos del BCRP (Banco Central de Reserva del Perú).

## Estructura del proyecto

```
Balanza de Pagos/
├── assets/
│   └── Balanza_de_Pagos.csv    # Data fuente (ISO-8859-1)
├── output/
│   ├── tables/                  # Tablas en formato APA (PNG)
│   │   ├── tabla_1_resumen_bp.png
│   │   ├── tabla_2_componentes_cc.png
│   │   ├── tabla_3_desglose_bienes_servicios.png
│   │   ├── tabla_4_ingreso_primario_secundario.png
│   │   ├── tabla_5_componentes_cf.png
│   │   ├── tabla_6_activos_pasivos_sector.png
│   │   └── tabla_7_resultado_bp_rin.png
│   └── graph/                   # Gráficos (PNG)
│       ├── grafico_1_resumen_bp_apilado.png
│       ├── grafico_2_balanza_comercial_servicios.png
│       ├── grafico_3_ingreso_primario_secundario.png
│       ├── grafico_4_cf_componentes.png
│       ├── grafico_5_activos_pasivos_sector.png
│       └── grafico_6_resultado_bp_rin.png
├── analisis.ipynb               # Notebook principal
├── requirements.txt             # Dependencias
├── README.md
└── .gitignore
```

## Variables del dataset

El dataset contiene 27 series de la Balanza de Pagos del Perú (2016–2026), en millones de US$.

### Cuenta Corriente

| Variable | Descripción |
|----------|-------------|
| `CC_Bienes_Export` | Exportaciones de bienes |
| `CC_Bienes_Import` | Importaciones de bienes |
| `CC_Bienes` | Saldo neto de bienes = Export - Import |
| `CC_Servicios_Export` | Exportaciones de servicios |
| `CC_Servicios_Import` | Importaciones de servicios |
| `CC_Servicios` | Saldo neto de servicios = Export - Import |
| `CC_Ingreso_Primario_Pub` | Ingreso primario - sector público |
| `CC_Ingreso_Primario_Priv` | Ingreso primario - sector privado |
| `CC_Ingreso_Primario` | Ingreso primario total = Pub + Priv |
| `CC_Remesas` | Remesas (componente del ingreso secundario) |
| `CC_Ingreso_Secundario` | Ingreso secundario (incluye remesas) |
| `Cuenta_Corriente` | = CC_Bienes + CC_Servicios + CC_Ingreso_Primario + CC_Ingreso_Secundario |

### Cuenta Financiera

**Convención de signos del BCRP:**
- **CF positivo** = aumento de activos externos netos (salida de capitales)
- **CF negativo** = aumento de pasivos externos netos (entrada de capitales)

| Variable | Descripción |
|----------|-------------|
| `CF_SectorPrivado_Activos` | Activos del sector privado |
| `CF_SectorPrivado_Pasivos` | Pasivos del sector privado |
| `CF_SectorPrivado` | Sector privado neto = Activos - Pasivos |
| `CF_SectorPublico_Activos` | Activos del sector público |
| `CF_SectorPublico_Pasivos` | Pasivos del sector público |
| `CF_SectorPublico` | Sector público neto = Activos - Pasivos |
| `CF_CortoPlazo_Activos` | Activos de corto plazo |
| `CF_CortoPlazo_Pasivos` | Pasivos de corto plazo |
| `CF_CortoPlazo` | Corto plazo neto = Activos - Pasivos |
| `Cuenta_Financiera` | = CF_Sector_Privado + CF_SectorPublico + CF_CortoPlazo |

### Resultado y RIN

| Variable | Descripción |
|----------|-------------|
| `Resultado_BP` | Resultado de Balanza de Pagos |
| `Errores_Omisiones` | Errores y omisiones netos |
| `Financ_Excepcional` | Financiamiento excepcional |
| `Efecto_Valuacion` | Efecto de valuación del RIN |
| `Var_Saldo_RIN` | Variación del saldo de RIN |

### Fórmulas clave

```
Cuenta_Corriente = CC_Bienes + CC_Servicios + CC_Ingreso_Primario + CC_Ingreso_Secundario

CF_SectorPrivado   = CF_SectorPrivado_Activos - CF_SectorPrivado_Pasivos
CF_SectorPublico   = CF_SectorPublico_Activos - CF_SectorPublico_Pasivos
CF_CortoPlazo      = CF_CortoPlazo_Activos - CF_CortoPlazo_Pasivos
Cuenta_Financiera  = CF_Sector_Privado + CF_SectorPublico + CF_CortoPlazo

Resultado_BP       = Cuenta_Corriente - Cuenta_Financiera + Errores_Omisiones + Financ_Excepcional
Var_Saldo_RIN      = Resultado_BP + Efecto_Valuacion
```

**Nota:** El Resultado de Balanza de Pagos RESTA la Cuenta Financiera porque el BCRP registra CF negativo cuando hay entrada de capitales. Restar un valor negativo equivale a sumar la entrada neta de capitales.

## Tablas (output/tables/)

| Archivo | Contenido |
|---------|-----------|
| `tabla_1_resumen_bp.png` | Resumen de Balanza de Pagos: CC, CF, EO, FE, Resultado_BP |
| `tabla_2_componentes_cc.png` | Componentes de Cuenta Corriente: Bienes, Servicios, Ingresos |
| `tabla_3_desglose_bienes_servicios.png` | Desglose de Bienes y Servicios: Export, Import, Saldo neto |
| `tabla_4_ingreso_primario_secundario.png` | Ingreso Primario (Pub, Priv) y Secundario (Remesas) |
| `tabla_5_componentes_cf.png` | Componentes de Cuenta Financiera por sector |
| `tabla_6_activos_pasivos_sector.png` | Activos y Pasivos desglosados por sector |
| `tabla_7_resultado_bp_rin.png` | Resultado BP, Efecto Valuación y Variación RIN |

Las tablas siguen el formato **APA 7ma edición**: solo líneas horizontales (superior, bajo encabezado, inferior), fuente serif (Times New Roman), encabezados en negrita, valores numéricos centrados, año como entero.

## Gráficos (output/graph/)

| Archivo | Contenido |
|---------|-----------|
| `grafico_1_resumen_bp_apilado.png` | Barras apiladas de CC, CF, EO, FE + línea de Resultado_BP |
| `grafico_2_balanza_comercial_servicios.png` | Balanza Comercial y de Servicios (Export, Import, Saldo) |
| `grafico_3_ingreso_primario_secundario.png` | Ingreso Primario (Pub, Priv, Total) y Secundario + Remesas |
| `grafico_4_cf_componentes.png` | Barras apiladas de CF por sector + línea de CF neta |
| `grafico_5_activos_pasivos_sector.png` | Activos vs Pasivos por sector (3 paneles) |
| `grafico_6_resultado_bp_rin.png` | Resultado BP, Efecto Valuación y Variación RIN |

Todos los gráficos incluyen nota al pie: *"Elaboracion propia con datos del BCRP."*

## Requisitos

```
pandas>=2.0
numpy>=1.24
matplotlib>=3.7
openpyxl>=3.1
```

## Uso

```bash
python -m venv venv
.\venv\Scripts\activate      # Windows
pip install -r requirements.txt
jupyter notebook analisis.ipynb
```

Las imágenes se generan automáticamente en `output/tables/` y `output/graph/` al ejecutar el notebook.

## Fuente

[BCRP - Estadísticas](https://www.bcrp.gob.pe/estadisticas.html)
