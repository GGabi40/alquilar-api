# 🏙️ API de Provincias y Localidades de Argentina

Este repositorio contiene un archivo JSON con **todas las provincias y sus localidades de Argentina**, extraídas del sitio oficial de Correo Argentino y estructuradas con **IDs únicos**.  
Está pensado para ser utilizado como fuente de datos (API estática) en proyectos web, académicos o de software libre.

---

## 🌐 Enlace de la API

📁 JSON público disponible en:  

👉 **[https://raw.githubusercontent.com/GGabi40/alquilar-api/main/provincias_localidades_argentina.json](https://raw.githubusercontent.com/GGabi40/alquilar-api/main/provincias_localidades_argentina.json)**

👉 **[https://ggabi40.github.io/alquilar-api/provincias_localidades_argentina.json](https://ggabi40.github.io/alquilar-api/provincias_localidades_argentina.json
)**

Podés consumirlo con cualquier cliente HTTP o directamente desde tu frontend usando <code>fetch()</code>.

---

## 🧱 Estructura del archivo

El JSON tiene la siguiente estructura:

```json
{
  "provincias": [
    {
      "id": 1179588662,
      "nombre": "Buenos Aires",
      "localidades": [
        { "id": 781059593, "nombre": "ABEL (PEHUAJO)" },
        { "id": 2116172094, "nombre": "ACHAVAL (GENERAL VIAMONTE)" },
        { "id": 2659506469, "nombre": "ACHUPALLAS (ALBERTI)" }
      ]
    },
    {
      "id": 2150813762,
      "nombre": "Córdoba",
      "localidades": [
        { "id": 135049221, "nombre": "CÓRDOBA" },
        { "id": 723819833, "nombre": "RÍO CUARTO" }
      ]
    }
  ]
}
```

- <code>id</code>: número único (estable) generado por hash MD5.  
- <code>nombre</code>: nombre de la provincia o localidad.  
- <code>localidades</code>: arreglo con todas las localidades pertenecientes a esa provincia.

---

## ⚙️ Cómo usarlo

### 🟢 Ejemplo básico en JavaScript

```js
fetch("https://ggabi40.github.io/alquilar-api/provincias_localidades_argentina.json")
  .then(res => res.json())
  .then(data => {
    const provincias = data.provincias;
    console.log("Provincias disponibles:", provincias.length);

    // Mostrar la primera provincia
    console.log(provincias[0].nombre);
  });
```

---

### 🟡 Cargar provincias y localidades en selects

```js
<select id="provincia">;
  <option value="">Seleccionar provincia</option>
</select>

<select id="localidad">;
  <option value="">Seleccionar localidad</option>
</select>

<script>
async function cargarProvincias() {
  const res = await fetch("https://ggabi40.github.io/alquilar-api/provincias_localidades_argentina.json");
  const data = await res.json();

  const selectProv = document.getElementById("provincia");
  data.provincias.forEach(p => {
    const opt = document.createElement("option");
    opt.value = p.id;
    opt.textContent = p.nombre;
    selectProv.appendChild(opt);
  });

  selectProv.addEventListener("change", (e) => {
    const idSeleccionado = parseInt(e.target.value);
    const provincia = data.provincias.find(p => p.id === idSeleccionado);
    const selectLoc = document.getElementById("localidad");

    selectLoc.innerHTML = "<option value=''>Seleccionar localidad</option>";
    provincia.localidades.forEach(l => {
      const opt = document.createElement("option");
      opt.value = l.id;
      opt.textContent = l.nombre;
      selectLoc.appendChild(opt);
    });
  });
}

cargarProvincias();
</script>
```

---

## 📦 Uso en Node.js

<code>npm install axios</code>

```js
import axios from "axios";

const url = "https://ggabi40.github.io/alquilar-api/provincias_localidades_argentina.json";

axios.get(url).then(res =>; {
  console.log("Provincias:", res.data.provincias.length);
});
```

---

## 📘 Datos técnicos

- **Fuente original:** [Correo Argentino – Código Postal Argentino](https://www.correoargentino.com.ar/formularios/cpa)
- **Extracción automatizada:** Script con Puppeteer optimizado
- **Formato:** JSON UTF-8
- **Total de provincias:** 24
- **Localidades:** +2.000 (según actualización)
- **Licencia:** MIT (uso libre con mención de fuente)

---

## 🪄 Créditos

Datos obtenidos de **Correo Argentino**, procesados y estructurados por [@GGabi40](https://github.com/GGabi40) para su proyecto académico *AlquilAR*.
