# ANÁHUAC Ads Analytics

Herramienta de análisis de creativos para campañas ANÁHUAC Global Minds.  
Procesa el reporte de Meta Ads + el CRM de matriculados directamente en el navegador — los datos nunca salen de tu computadora.

## ¿Qué hace?

- Cruza el reporte CSV de Meta Ads con el Excel del CRM de matriculados
- Extrae leads, gasto, CPL (USD y BRL), avanzados, matriculados y tasa de conversión por creativo
- Genera automáticamente el estado de cada creativo: ★ Top / ✓ Eficiente / ◎ Oportunidad / ⚠ Revisar / ✕ Pausar
- Muestra miniaturas de los creativos si se sube el PDF de pauta
- Filtros por programa (GMP Masters + Diplomados) y por estado
- Link directo a la carpeta de Drive con los archivos actualizados

## Archivos que necesitás

| Archivo | Descripción | Obligatorio |
|---------|-------------|-------------|
| `informe_de_meta.csv` | Reporte exportado desde Meta Business Suite (separador `;`, valores en BRL) | ✅ |
| `ANAHUAC_MATRICULADOS_Y_AVANZADOS.xlsx` | Excel del CRM con columnas UTM CONTENT, Resolución, Bases de datos, Programa de Interés | ✅ |
| `Pauta_Másters.pdf` | PDF de pauta con las creatividades (estructura: Estudioso págs 3-10, Ambicioso 12-19, Desbravador 21-28, Especialista 30-37) | ⬜ Opcional |

## Configuración

Antes de desplegar, editá estas dos constantes en `index.html` (líneas ~80):

```js
const CONFIG = {
  RATE: 5.07,  // Tipo de cambio BRL → USD. Actualizar periódicamente.
  DRIVE_URL: 'https://drive.google.com/drive/folders/...',  // Tu carpeta de Drive
};
```

## Deploy en Vercel (recomendado)

### Opción A — Desde GitHub (recomendado)

1. Creá un repo en GitHub y subí estos archivos:
   ```
   git init
   git add .
   git commit -m "Initial deploy"
   git branch -M main
   git remote add origin https://github.com/TU_USUARIO/anahuac-analytics.git
   git push -u origin main
   ```

2. Entrá a [vercel.com](https://vercel.com) → **New Project** → importá el repo

3. En la configuración de Vercel:
   - **Framework Preset:** Other
   - **Build Command:** *(dejar vacío)*
   - **Output Directory:** `.`
   - Hacé clic en **Deploy**

4. Cada vez que hagas `git push`, Vercel redespliega automáticamente.

### Opción B — Vercel CLI

```bash
npm i -g vercel
cd anahuac-analytics
vercel --prod
```

### Opción C — Drag & Drop

Arrastrá la carpeta `anahuac-analytics` a [vercel.com/new](https://vercel.com/new).

---

## Actualizar el tipo de cambio

Editá `CONFIG.RATE` en `index.html` y hacé push:

```js
const CONFIG = {
  RATE: 5.12,  // Nuevo valor
  ...
};
```

## Estructura del proyecto

```
anahuac-analytics/
├── index.html    # App completa (HTML + CSS + JS en un solo archivo)
├── vercel.json   # Configuración de Vercel
├── .gitignore    # Archivos ignorados por Git
└── README.md     # Este archivo
```

## Tecnologías

- [PapaParse](https://www.papaparse.com/) — parsing de CSV
- [SheetJS (xlsx)](https://sheetjs.com/) — parsing de Excel
- [Chart.js](https://www.chartjs.org/) — gráficos
- [PDF.js](https://mozilla.github.io/pdf.js/) — extracción de miniaturas del PDF
- Todo vanilla JS — sin frameworks, sin build step

## Soporte

Generado por NODS Technology for Education.
