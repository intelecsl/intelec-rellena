# Intelec — Rellena Formularios v1.2

Complemento de Outlook que detecta adjuntos (DOCX, XLSX, PDF), los analiza con IA (Claude), rellena automáticamente los campos con los datos de INTELEC S.L. y permite descargar el resultado en PDF.

---

## Estructura del repositorio

```
intelec-rellena/
├── index.html       ← App principal (todo en un fichero)
├── manifest.xml     ← Manifiesto de Outlook
├── icon-16.png      ← Icono 16×16 (añadir manualmente)
├── icon-32.png      ← Icono 32×32 (añadir manualmente)
├── icon-64.png      ← Icono 64×64 (añadir manualmente)
├── icon-128.png     ← Icono 128×128 (añadir manualmente)
└── README.md
```

---

## Despliegue en GitHub Pages

1. **Crear repositorio** en GitHub (ej: `intelecsl/intelec-rellena`)
2. Subir todos los ficheros
3. Ir a **Settings → Pages → Branch: main → / (root)** → Save
4. URL resultante: `https://intelecsl.github.io/intelec-rellena/`
5. **Editar `manifest.xml`**: reemplazar `intelecsl` por tu usuario de GitHub en todos los campos

---

## Instalar en Outlook

### Opción A — Archivo XML (más rápida, administrador)
1. En Outlook desktop: **Archivo → Administrar complementos** (o en OWA: Configuración → Ver todos los complementos de Outlook)
2. Seleccionar **"Agregar desde archivo"** (requiere Exchange/M365 administrador)
3. Subir el `manifest.xml`

### Opción B — URL del manifiesto
1. Outlook Web (OWA) → **Configuración → Complementos → Mis complementos**
2. **Agregar complemento personalizado → Desde URL**
3. Pegar: `https://intelecsl.github.io/intelec-rellena/manifest.xml`

### Opción C — Prueba local con ngrok
```bash
npx serve . -p 3000
npx ngrok http 3000
# Usar la URL de ngrok en el manifest.xml para pruebas
```

---

## Uso

1. Abrir un email que contenga un adjunto (DOCX, XLSX o PDF con formulario)
2. Hacer clic en **"Rellena Formularios"** en la barra de Outlook
3. **Paso 1** — Seleccionar adjunto del email o subir archivo manualmente
   - Introducir clave API Anthropic (se guarda en localStorage)
4. **Paso 2** — Claude analiza el documento e identifica campos
   - Revisar campos detectados y valores
   - Editar si es necesario, omitir campos con ✕
5. **Paso 3** — Descargar
   - **PDF** → abre ventana de impresión (guardar como PDF)
   - **DOCX/XLSX** → descarga el fichero rellenado

---

## Datos precargados

| Campo | Valor |
|-------|-------|
| Razón social | INTELEC, S.L. |
| CIF | B28805398 |
| Domicilio | C/ Amado Nervo 13-15, Local — 28007 Madrid |
| Teléfono | 915 013 333 |
| Email empresa | intelecsl@intelecsl.com |
| Email contabilidad | contabilidad@intelecsl.com |
| IBAN | ES6400610370610017960114 (Banca March) |
| Representante | Carlos García Lucía · DNI 50.791.248-A |
| Poder notarial | 11 mayo 1998 · C. Ruiz-Rivas Hernando · Prot. 1344 |
| Contacto admin | Isabel · Administración |
| CNAE | 4321 | IAE | 504.1 |
| REA | 12-28-0019480 | EBTE | EBTE-216 |
| Reg. Mercantil | Madrid · T.6713 · Sec.3ª · L.5705 · H.57259 |
| Seguro RC | Póliza 053023029 · Allianz |

---

## Requisitos

- Microsoft 365 con Outlook (desktop o web)
- Clave API de Anthropic (`sk-ant-api03-...`)
- Repositorio GitHub Pages (HTTPS obligatorio para Office add-ins)

---

## Iconos

Crear iconos PNG con el logo de Intelec en los tamaños: 16×16, 32×32, 64×64, 128×128.  
Colocarlos en la raíz del repositorio con los nombres `icon-16.png`, `icon-32.png`, `icon-64.png`, `icon-128.png`.

---

## Notas técnicas

- **Office.js** — acceso a adjuntos del email (`getAttachmentContentAsync`)
- **JSZip** — manipulación DOCX (ZIP con XML interno)
- **SheetJS (xlsx)** — lectura/escritura de XLSX
- **pdf-lib** — relleno de campos de formularios PDF
- **Claude API** — análisis inteligente de campos del documento
- **Sin servidor** — todo procesamiento en el navegador (cliente puro)

---

*Intelec S.L. · Desarrollado sobre la misma base que Firma Digital Intelec*
