# 🤖 TermMant Bot — Demo Interactiva

Sitio en vivo: 🔗 **[https://termmant-bot.netlify.app/](https://termmant-bot.netlify.app/)**  
*(Reemplaza con la URL real de tu despliegue en Netlify)*

---

## 📖 Descripción

**TermMant Bot** es una demo interactiva de un asistente de mantenimiento industrial vía WhatsApp. Muestra cómo los técnicos pueden:

- Recibir órdenes de trabajo.
- Completar checklists interactivos en el chat.
- Reportar fallas con criticidad y fotos.
- Consultar el historial de equipos y órdenes pendientes.

La demo está diseñada para simular la experiencia real de un técnico en terreno usando solo WhatsApp, sin necesidad de apps adicionales.

---

## 🧠 Metodología

Este proyecto utiliza la misma metodología que otros recursos de TermIng Chile SPA:

- **`index.html`**: Estructura, estilos y lógica del bot.
- **`bot-data.json`**: Todos los mensajes, opciones, flujos y configuraciones del bot.

**Ventaja**: Puedes modificar cualquier mensaje, añadir nuevas opciones o cambiar el flujo de conversación sin tocar el HTML. Solo editas el JSON, haces commit en GitHub, y Netlify lo despliega automáticamente.

---

## 📂 Estructura de archivos
📁 termmant-bot/
├── index.html # Página del bot (estructura, estilos, lógica)
├── bot-data.json # Contenido del bot (mensajes, flujos, opciones)
└── README.md # Este archivo

text

---

## ⚙️ Cómo funciona

El bot carga los datos desde `bot-data.json` mediante `fetch()` y renderiza los mensajes, opciones y flujos de forma dinámica. Los flujos están definidos como objetos JSON que permiten:

- Mensajes de texto (con soporte HTML básico).
- Tiempos de escritura simulados (`typing`).
- Opciones de respuesta rápida (`quickReplies`).
- Checklists interactivos.
- Entrada de texto libre (`input`).

---

## ✏️ Personalización

### Cambiar mensajes u opciones

Edita el archivo `bot-data.json` y modifica los valores que necesites:

```json
{
  "flows": {
    "inicio": [
      {
        "type": "message",
        "sender": "bot",
        "text": "👋 Buenos días, <b>Carlos</b>.\n\nTienes <b>2 órdenes</b> para hoy."
      }
    ]
  }
}
Añadir una nueva opción de respuesta rápida
Agrega la opción en config.quickReplies:

json
"quickReplies": {
  "nuevas_opciones": ["Opción 1", "Opción 2"]
}
Crea un flujo que la maneje:

json
"flows": {
  "handleNuevaOpcion": {
    "opcion_1": [
      { "type": "typing", "duration": 600 },
      { "type": "message", "sender": "bot", "text": "Has elegido la Opción 1." }
    ],
    "opcion_2": [
      { "type": "typing", "duration": 600 },
      { "type": "message", "sender": "bot", "text": "Has elegido la Opción 2." }
    ]
  }
}
Modificar el checklist
Busca el flujo handleOrden y dentro de compresor o bomba, edita el array items:

json
{
  "type": "checklist",
  "items": ["Nivel de aceite", "Temperatura", "Presión"],
  "next": "handleChecklist"
}