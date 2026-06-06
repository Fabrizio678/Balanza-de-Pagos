# Balanza de Pagos - BCRP

Análisis de la Balanza de Pagos del Perú usando datos del BCRP (Banco Central de Reserva del Perú).

## Estructura

```
Balanza de Pagos/
├── assets/
│   └── Balanza_de_Pagos.csv    # Data fuente (ISO-8859-1)
├── analisis.ipynb               # Notebook principal
├── requirements.txt             # Dependencias
└── .gitignore
```

## Uso

```bash
python -m venv venv
source venv/bin/activate      # Linux/Mac
# .\venv\Scripts\activate     # Windows
pip install -r requirements.txt
jupyter notebook analisis.ipynb
```

## Fuente

[BCRP - Estadísticas](https://www.bcrp.gob.pe/estadisticas.html)
