# ICN292 — Laboratorio 3: triage de devoluciones con n8n

## Parámetros
Semilla S=026,  dando como resultado U= $56.000 y D= 21 días 

## Repositorio
En este repositorio se construyeron tres flujos distintos en n8n.

| Archivo                                 | Qué es                           |
| --------------------------------------- | -------------------------------- |
| `ICN292-Lab3-Ruiz-Lorenzo.pdf`          | Informe                          |
| `ICN292-Lab3-Ruiz-Lorenzo.tex`          | Fuente del informe               |
| `ICN292-Lab3-Ruiz-Lorenzo-triage.json`  | Flujo 2, el triage               |
| `ICN292-Lab3-Ruiz-Lorenzo-emisor.json`  | Flujo 1, el emisor               |
| `ICN292-Lab3-Ruiz-Lorenzo-resumen.json` | Flujo 3, el resumen diario       |
| `registro_devoluciones.csv`             | Las 15 solicitudes ya procesadas |
| `Carpetas Capturas`                     | Evidencia de las ejecuciones     |

## Como leer este repositorio 
Si solo se quiere revisar los resultados, abriendo el PDF y el `registro_devoluciones.csv`, muestra todo el resultado obtenido de las 15 solicitudes enviadas.

## Como correr el sistema

1. **Crear la tabla.** En n8n, Overview → Data tables → Create. Nómbrala
   `registro_devoluciones` con estas columnas: `fecha`, `id_solicitud`, `sku`, `monto`,
   `dias_desde_compra`, `estado_producto`, `email_cliente`, `ruta`, `motivo`, `U`, `D`,
   `uf_valor`, `monto_uf`. Los montos, días, `U`, `D` y los valores en UF van como número; el
   resto como texto, salvo `fecha`, que va como fecha.

2. **Importar los flujos.** Workflows → Import from File, uno por cada `.json`.

3. **Conectar Gmail.** Los `.json` no traen credenciales. En los nodos de Gmail hay que crear
   una credencial propia y cambiar el destinatario. El nodo que consulta la UF usa
   `https://mindicador.cl/api`, que es público.

4. **Ejecutar.** Abre el triage, copia la Production URL del Webhook y activa el flujo. Pega esa
   URL en el nodo `Enviar a triage` del emisor y ejecútalo. Las 15 solicitudes quedan
   registradas.

5. **Ver el resumen.** El flujo de resumen corre solo una vez al día, pero puede dispararse a
   mano con Execute workflow.

## Resultado esperado

| Ruta | Solicitudes | Monto |
|---|---|---|
| APROBACION | 4 | $125.950 |
| REVISION | 7 | $924.920 |
| RECHAZO | 4 | $200.950 |
| Total | 15 | $1.251.820 |

Tasa de aprobación automática: 26,7%.
