# API Catálogo de Autos

Microservicio web en **Node.js + Express** que recupera un catálogo básico de autos con los atributos **marca, modelo, año, precio y color**. Publicado en Render.

- **Repositorio:** https://github.com/USUARIO/catalogo-autos
- **Servicio en Render:** https://catalogo-autos.onrender.com

## Ejecutar localmente

```bash
npm install
npm start
# http://localhost:3000
```

## Estructura

```
catalogo-autos/
├── data/autos.json   # datos del catálogo
├── server.js         # servidor Express y rutas
├── package.json
└── README.md
```

## Modelo de datos

| Campo  | Tipo   | Ejemplo  |
|--------|--------|----------|
| id     | número | 1        |
| marca  | texto  | Toyota   |
| modelo | texto  | Corolla  |
| anio   | número | 2022     |
| precio | número (MXN) | 389900 |
| color  | texto  | Blanco   |

## Rutas

| Método | Ruta | Descripción |
|--------|------|-------------|
| GET | `/` | Información del servicio y lista de rutas |
| GET | `/api/autos` | Catálogo completo (acepta filtros) |
| GET | `/api/autos/:id` | Un auto por id |
| GET | `/api/autos/marca/:marca` | Autos de una marca |
| GET | `/api/marcas` | Marcas disponibles |
| GET | `/api/salud` | Estado del servicio |

### Filtros de `/api/autos` (query string, todos opcionales)

| Parámetro | Ejemplo | Efecto |
|-----------|---------|--------|
| marca | `?marca=toyota` | Marca exacta (sin importar mayúsculas/acentos) |
| modelo | `?modelo=cor` | Modelo que contenga el texto |
| color | `?color=blanco` | Color exacto |
| anio | `?anio=2023` | Año exacto |
| precioMin / precioMax | `?precioMin=300000&precioMax=500000` | Rango de precio |
| orden | `?orden=precio_asc` | `precio_asc`, `precio_desc`, `anio_asc`, `anio_desc` |

### Ejemplo

`GET /api/autos?precioMax=350000&orden=precio_asc`

```json
{
  "total": 3,
  "autos": [
    { "id": 6, "marca": "Chevrolet", "modelo": "Aveo", "anio": 2022, "precio": 279900, "color": "Plata" },
    { "id": 2, "marca": "Nissan", "modelo": "Versa", "anio": 2023, "precio": 329900, "color": "Gris" },
    { "id": 7, "marca": "Kia", "modelo": "Rio", "anio": 2024, "precio": 334900, "color": "Blanco" }
  ]
}
```

### Códigos de respuesta

- `200` Correcto
- `400` Parámetro inválido (ej. `?anio=abc`)
- `404` Auto, marca o ruta no encontrados

## Despliegue en Render

New → Web Service → elegir este repositorio → Runtime **Node** → Build `npm install` → Start `node server.js` → plan **Free** → Create Web Service.
