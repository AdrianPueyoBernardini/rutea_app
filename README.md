# RUTEA

**Prepara tu salida al Pirineo en segundos: material, normativa y tiempos según tu ruta, actividad y fecha.**

![Versión](https://img.shields.io/badge/versi%C3%B3n-0.0.0-blue)
![React Native](https://img.shields.io/badge/React%20Native-20232A?logo=react&logoColor=61DAFB)
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![.NET](https://img.shields.io/badge/.NET-512BD4?logo=dotnet&logoColor=white)
![Licencia](https://img.shields.io/badge/licencia-MIT-green)
![Build](https://img.shields.io/badge/build-passing-brightgreen)

---

##  Descripción

### ¿Qué problema resuelve?

Preparar una salida a la montaña implica consultar muchas fuentes: la meteorología, la normativa del espacio protegido, los horarios de luz y el material adecuado para la época. Esa información está dispersa, cambia con frecuencia y es fácil pasar algo por alto.

**Rutea** reúne todo en una sola ficha. Introduces tres datos:

1. **Nombre de la ruta** (por ejemplo, *Faja de las Flores* o *Aneto por la Renclusa*)
2. **Actividad** (senderismo, alta montaña, esquí de travesía, trail, escalada…)
3. **Fecha** de la salida

Y la app devuelve:

- 🎒 **Material recomendado**: checklist adaptada a la actividad, la época y la previsión.
- 📜 **Normativa aplicable**: reglas del espacio protegido, restricciones de acceso, bivac, perros, drones, fuego y zonas transfronterizas.
- ⏱️ **Tiempos**: duración estimada, hora de salida recomendada y hora límite de regreso según amanecer y ocaso.
- 🚦 **Nivel de riesgo** orientativo, combinando meteorología y dificultad.

### Público objetivo

- Senderistas y montañeros que quieren planificar con rapidez y seguridad.
- Personas que se inician en la alta montaña y no saben qué llevar ni qué normas aplican.
- Familias y grupos que necesitan saber si una ruta es adecuada para su nivel.

> ⚠️ **Aviso:** Rutea es una ayuda de planificación. No sustituye al boletín oficial de meteorología o aludes ni al criterio propio. Consulta siempre las fuentes oficiales enlazadas en la app.

---

## 🧠 Funcionalidades

- [x] Catálogo de rutas clásicas del Pirineo aragonés
- [x] Selección de actividad y fecha
- [x] Previsión meteorológica y horas de sol
- [x] Checklist de material generada por reglas
- [x] Resumen en lenguaje natural con IA
- [ ] Avisos de normativa con RAG sobre documentos oficiales
- [ ] Modo offline con descarga de la ficha y el track
- [ ] Exportación a PDF y GPX
- [ ] Reportes de la comunidad (estado de nieve, senderos, fuentes)

---

## 🛠️ Tecnologías (Provisional)

| Capa | Tecnología | Función |
|---|---|---|
| **Front end** | React Native (Expo) | Aplicación móvil multiplataforma |
| **Backend** | .NET 8 (ASP.NET Core Web API) | API REST, lógica de negocio y acceso a datos |
| **IA y módulos** | Python 3.11 + FastAPI | Generación de resúmenes, RAG y estimación de tiempos |
| **Base de datos** | PostgreSQL + PostGIS | Rutas, zonas protegidas y datos geoespaciales |
| **Datos externos** | AEMET OpenData, Open-Meteo, OpenStreetMap | Meteorología, cartografía y refugios |

### Arquitectura

```
┌────────────────┐      HTTPS      ┌──────────────────┐      HTTP      ┌───────────────────┐
│  React Native  │ ──────────────► │   .NET Web API   │ ─────────────► │  Python (FastAPI) │
│   (móvil)      │ ◄────────────── │    (backend)     │ ◄───────────── │   IA y módulos    │
└────────────────┘                 └────────┬─────────┘                └─────────┬─────────┘
                                            │                                    │
                                   ┌────────▼─────────┐                ┌─────────▼─────────┐
                                   │ PostgreSQL/PostGIS│                │  APIs externas    │
                                   └──────────────────┘                │ (AEMET, Open-Meteo)│
                                                                       └───────────────────┘
```

---

## 🗂️ Estructura del proyecto (Provisional)

```
piriruta/
├── mobile/                      # Front end (React Native)
│   ├── src/
│   │   ├── components/          # Componentes reutilizables
│   │   ├── screens/             # Pantallas (Búsqueda, Ficha, Ajustes)
│   │   ├── navigation/          # Configuración de rutas de navegación
│   │   ├── services/            # Llamadas a la API
│   │   ├── hooks/               # Hooks personalizados
│   │   └── utils/
│   ├── App.tsx
│   └── package.json
│
├── backend/                     # Backend (.NET)
│   ├── PiriRuta.Api/            # Controladores y configuración
│   ├── PiriRuta.Core/           # Entidades y lógica de dominio
│   ├── PiriRuta.Infrastructure/ # Acceso a datos y servicios externos
│   └── PiriRuta.sln
│
├── ai-service/                  # IA y módulos (Python)
│   ├── app/
│   │   ├── main.py              # Punto de entrada FastAPI
│   │   ├── routers/             # Endpoints
│   │   ├── services/            # LLM, RAG, estimación de tiempos
│   │   └── models/              # Esquemas de datos
│   ├── data/                    # Normativas y documentos para RAG
│   ├── tests/
│   └── requirements.txt
│
├── docs/                        # Documentación y recursos visuales
│   └── media/
├── docker-compose.yml
├── LICENSE
└── README.md
```

---

## 📦 Instalación local (Provisional)

### Requisitos previos

- [Node.js](https://nodejs.org/) 18 o superior
- [.NET SDK](https://dotnet.microsoft.com/download) 8.0
- [Python](https://www.python.org/downloads/) 3.11 o superior
- [PostgreSQL](https://www.postgresql.org/) con la extensión PostGIS (o Docker)
- La app [Expo Go](https://expo.dev/go) en el móvil, o un emulador Android/iOS

## 🤝 Contribuir

1. Haz un *fork* del repositorio.
2. Crea una rama: `git checkout -b feature/mi-mejora`
3. Haz *commit* de tus cambios: `git commit -m "Añade mi mejora"`
4. Sube la rama: `git push origin feature/mi-mejora`
5. Abre un *Pull Request*.

---

## 👥 Autores

| Nombre | Rol | GitHub |
|---|---|---|
| **Adrian Pueyo Bernardini** | Desarrollo y arquitectura | [@AdrianPueyoBernardini]([https://github.com/tu-usuario](https://github.com/AdrianPueyoBernardini)) |
| **Daniel Sanchez Bartolome** | Desarrollo y arquitectura | [@DanielSB93]([https://github.com/usuario](https://github.com/DanielSB9)) |
| **Adrian Rodriguez Machado** | Desarrollo y arquitectura | [@20adrianr02-arch]([https://github.com/usuario](https://github.com/20adrianr02-arch)) |

---

## 📄 Licencia

Distribuido bajo la licencia **MIT**. Consulta el archivo [`LICENSE`](LICENSE) para más información.

---

Hecho con ❤️ y mucha montaña en el Pirineo.

