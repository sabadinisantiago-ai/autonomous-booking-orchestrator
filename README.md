🤖 AI Appointment Agent: Gestionando turnos como un Pro

Este es un proyecto de automatización donde armé un Agente de IA que no solo chatea, sino que "hace cosas". La idea fue salir del típico bot de opciones aburridas y crear un sistema que entienda qué quiere el usuario, revise la agenda y tome decisiones por su cuenta.

🛠️ Cómo funciona la magia (Arquitectura)
Para que esto no fuera un lío de cables, dividí la lógica en tres bloques clave. Así me aseguré de que el bot sea inteligente y, sobre todo, que no anote cualquier cosa en el calendario:

Bloque A - ¿Qué me están pidiendo?: El agente analiza el mensaje y detecta al toque si alguien quiere un turno, si quiere cancelar o si solo está preguntando cualquier cosa.

Bloque B - Acción Real: Antes de decir "dale, te anoto", el bot va y chequea Google Calendar. Si el hueco está libre, anota al cliente en Google Sheets y crea el evento. Todo en un paso.

Bloque C - El "Plan B": Si alguien cancela, el bot no se queda de brazos cruzados; está pensado para ofrecer ese lugar a alguien en lista de espera.

<img width="1280" height="644" alt="image" src="https://github.com/user-attachments/assets/1637f069-46f3-404e-a500-53da0cf2f7de" />


🏗️ El Stack Técnico: n8n + IA
Usé n8n (corriendo en localhost) para orquestar todo. Lo más interesante fue configurar el AI Agent para que use herramientas (Tools) de forma dinámica.

Google Calendar Tool: Su mano derecha para ver cuándo hay lugar.

Google Sheets Tool: Nuestra base de datos para que no se pierda ni un contacto.

Memoria: Para que el bot no sea un "desmemoriado" y se acuerde de qué venían hablando.

<img width="1280" height="561" alt="image" src="https://github.com/user-attachments/assets/3e698280-0f63-4dd6-a773-cd5ef0829e4c" />


🧠 Prompt Engineering: El cerebro del bot
Acá está el secreto. No le dije simplemente "ayudame a dar turnos". Diseñé un System Prompt para que el bot actúe como un asistente ejecutivo nivel Senior:

Formato estricto: Lo obligué a escupir un JSON. ¿Por qué? Porque así n8n puede leer los datos fácil y sin errores.

Validación primero: Tiene prohibido confirmar nada sin antes mirar el calendario. Cero margen de error.

JSON
// Así es como el bot piensa y me devuelve la data:
{
  "intencion": "agendar_turno",
  "datos_cliente": {
    "nombre": "Juan Perez",
    "fecha": "2024-05-20",
    "hora": "15:00"
  },
  "mensaje": "¡Listo Juan! Te espero ese día."
}
🚀 ¿Lo querés probar?
Si te bajás el repo, vas a encontrar el archivo workflow.json. Lo importás en tu n8n, conectás tus API Keys de OpenAI y Google, y ya lo tenés funcionando.

Nota: Vas a ver unos iconos de advertencia en las capturas. Es normal, son las credenciales que saqué por seguridad (¡no voy a regalar mi API Key! 😂).
