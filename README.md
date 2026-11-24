# NeuroPrenatal · IA — versión 0.1
Prototipo multiusuario para investigación con 30 casos simulados, 3 modelos y 3 repeticiones. No utilizar datos de pacientes reales. La PNC-20 no está validada.

## Instalación en Mac
Descomprimir el ZIP. Abrir Terminal y entrar en la carpeta del proyecto (escribir `cd `, arrastrar la carpeta y pulsar Intro). Ejecutar:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python app.py
```
Abrir http://127.0.0.1:8000 en el navegador. Mantener la Terminal abierta. Para detener, Ctrl+C. Para volver a iniciar: entrar en la carpeta, `source .venv/bin/activate` y `python app.py`.

## Acceso local inicial
| Usuario | Contraseña de prueba |
|---|---|
| admin | admin-demo-2026 |
| neuropediatra | neuropediatra-demo-2026 |
| ginecologa | ginecologa-demo-2026 |
| adjudicador | adjudicador-demo-2026 |

Cambiar todas las contraseñas antes de cualquier acceso público. En Render configurar las cuatro variables PASSWORD_* con contraseñas fuertes **antes del primer arranque**. Las variables de contraseña solo se aplican al inicializar la base de datos. SECRET_KEY debe ser estable y secreta.

## Flujo de trabajo
1. En modo real, administrador revisa los 30 enunciados provisionales, completa el patrón de referencia, fuentes y NA. Los casos son compartidos entre modos, las respuestas y evaluaciones están separadas. No cambiar un caso durante el estudio.
2. Registrar manualmente las respuestas anonimizadas de ChatGPT, Gemini y Claude. Conservar aparte los originales íntegros. Guardar versión, fecha, condiciones de acceso. No hay conexión automática con modelos.
3. Cada evaluador accede con su cuenta. El orden de respuestas es diferente, los códigos no muestran el modelo y no se ven las valoraciones ajenas. El texto podría revelar su procedencia si no se anonimiza previamente.
4. PNC-20 se calcula automáticamente; GQS, PEMAT-P e INFLESZ se introducen manualmente (PEMAT-P e INFLESZ deben calcularse con instrumentos externos). Las evaluaciones se cierran al guardar.
5. Si existe discrepancia, el adjudicador ve las valoraciones originales y registra una valoración definitiva. Sin discrepancia, se usa media de puntuaciones numéricas y categorías concordantes. Se excluyen adjudicaciones pendientes de los resultados finales.
6. El administrador exporta CSV con puntuaciones originales o definitivas. Estadística descriptiva e ICC(2,1); análisis inferencial externo. No hay cálculos de potencia, modelos mixtos ni IC automáticos.

## Demostración
270 respuestas genéricas ficticias; 90 con pares de puntuaciones sintéticas independientes del texto, para probar las discrepancias y resultados. No reproducen los datos inventados del manuscrito. No mezclar con datos reales. Modo real comienza sin respuestas y sin evaluaciones.

## Render / GitHub
Subir los archivos del proyecto (no la base de datos ni `.venv`) a un repositorio privado. Crear un Blueprint en Render con render.yaml y rellenar los secretos. Se ha previsto un servicio de pago con disco persistente, sujeto a los planes disponibles. Revisar configuración, costes y seguridad antes de publicar. SQLite está pensado para este equipo pequeño y una sola instancia. No eliminar el disco persistente. Para copias de seguridad coherentes, usar la API de backup de SQLite o detener el servicio antes de copiar el archivo; probar restauración. No se ha desplegado ni probado en Render.

## Estado de pruebas
Código compilado sintácticamente. El entorno de generación no dispone de Flask y no permite instalarlo desde internet; por ello no se ha podido ejecutar una prueba funcional de servidor. Revisar el flujo completo con datos de demostración antes de iniciar el estudio. Prototipo no auditado para seguridad ni validado científicamente.
