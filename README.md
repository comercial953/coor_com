# Portal Coordinadoras Biogreen Chile

Dashboard interno para el equipo de coordinadoras comerciales de Biogreen Chile,
hosteado como sitio estático en GitHub Pages.

Link público (una vez activado GitHub Pages):
**https://comercial953.github.io/coor_com/**

## Estructura del repo

```
/
├── index.html                     Portal (SPA en HTML+JS puro)
├── .nojekyll                      Le dice a GitHub Pages que no procese como Jekyll
├── data/
│   ├── ciclos_index.json          Índice de ciclos disponibles (en claro, solo metadatos)
│   └── ciclos/
│       └── 2025-2026__C##.json    Datos personales cifrados con AES-GCM 256
└── README.md
```

## Seguridad

Los archivos `data/ciclos/*.json` están **cifrados con AES-GCM 256**,
usando PBKDF2-SHA256 (100.000 iteraciones) sobre la clave del portal.
Solo quien tenga la clave puede descifrarlos.

- El repo puede ser público sin exponer datos personales.
- El `ciclos_index.json` va en claro pero solo contiene metadatos
  (número de ciclo, fecha de carga, cantidad total de personas — sin nombres).

## Cargar un ciclo nuevo (dueña del sistema)

Flujo manual, sin necesidad de tokens de GitHub:

1. Abre el portal desde el link público.
2. Ingresa tu clave. En el dashboard ve a **"Resumen por Ciclo"**.
3. Click en **"Cargar ciclo"** → arrastra el Excel del cierre (por ejemplo, `Ciclo 16 - 2025-2026.xlsx`).
4. Confirma. El portal procesa localmente y **descarga 2 archivos** a tu carpeta de *Descargas*:
   - `2025-2026__C##.json` (datos cifrados del ciclo)
   - `ciclos_index.json` (índice actualizado)
5. Ve a este repo en github.com:
   - Entra a la carpeta `data/ciclos/` → **"Add file" → "Upload files"** → arrastra `2025-2026__C##.json` → **"Commit changes"**.
   - Vuelve a la carpeta `data/` → **"Add file" → "Upload files"** → arrastra `ciclos_index.json` (reemplaza el existente) → **"Commit changes"**.
6. GitHub Pages redeploya en ~30-60 segundos y todas las coordinadoras al refrescar ven el ciclo nuevo.

## Publicar cambios de código

Si actualizas `index.html` (por ejemplo, un fix o feature nueva):
- Sube el archivo modificado a la raíz del repo.
- GitHub Pages redeploya automáticamente.
- Los ciclos ya cargados **no se pierden** (siguen en `data/`).

## Cumplimiento — Ley 19.628 y Ley 21.719

Este portal maneja datos personales y aplica:

- **Cifrado en reposo** (AES-GCM 256) para los datos personales de todas las coordinadoras.
- **Cifrado en tránsito** (HTTPS de GitHub Pages).
- **Identificador interno** (código Bionet) — nunca RUT ni otros identificadores nacionales.
- **Aviso de privacidad** dentro del portal.
- **Anti-bot** (honeypot, tiempo mínimo, lockout) para prevenir accesos automatizados.

---

Portal generado con [Claude Code](https://claude.com/claude-code).
