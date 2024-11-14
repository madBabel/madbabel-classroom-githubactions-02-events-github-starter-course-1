## Objetivo

Explorar distintas formas en las que se pueden ejecutar workflows en GitHub Actions.

## Tareas

1.  Crear un archivo '`02-workflow-events.yaml`' en la carpeta .github/workflows en la raíz de un repositorio. Los datos del workflow deben ser los siguientes:

*   nombre: 02 - Eventos
*   desencadente: push
*   Trabajos:
    *   `echo`, que se ejecuta en un runner tipo ubuntu-latest y tiene un solo step, llamado '`ShowTrigger`', que imprime de nombre del evento que desencadenó el workflow.

1.  Confirmar los cambios y subir (push) el código. Inspeccionar el resultado de la ejecución del workflow.
2.  Añadir más desencadenantes al workflow:
    *   pull\_request
    *   schedule (cron expression)
    *   workflow\_dispatch
3.  Confirmar los cambios y subir (push) el código. Inspeccionar las diferentes formas en que se activa el workflow.
4.  Crear un pull request en GitHub para ver cómo esto cambia el resultado de la ejecución del workflow.
5.  Probar a lanzar el workflow desde la interfaz de usuario:
    *   Acceder a la pestaña "Acciones" en la página de inicio del repositorio.
    *   Seleccionar el workflow '02 - Eventos' a la izquierda de la pantalla.
    *   Hacer clic en el botón "Ejecutar workflow" en el lado derecho de la pantalla".
    *   Observar cómo se activa el workflow.
6.  Reducir la lista de desencadenadores para dejar solo workflow\_dispatch, para evitar que este workflow se ejecute con cada push y ensucie la lista de ejecuciones de workflow.

## Tips

Utilizar una expresión cron válida. Para ello, tened en cuenta la sintáxis especificada en la documentación oficial de GitHub Actions (https://docs.github.com/es/actions/using-workflows/events-that-trigger-workflows#schedule) :

*   _"La sintaxis de cron tiene cinco campos separados por un espacio, y cada campo representa una unidad de tiempo."_Usar crontab guru para ayudar a generar la sintaxis cron y confirmar la hora en que se ejecutará: https://crontab.guru/

Para acceder al nombre del evento que desencadena el workflow, puede utilizar la variable: ${{ github.event\_name }}. Por ejemplo:

```
steps:
  - name: Event name
    run: |
      echo "Event name: ${{ github.event_name }}"
```

```
┌───────────── minute (0 - 59)
│ ┌───────────── hour (0 - 23)
│ │ ┌───────────── day of the month (1 - 31)
│ │ │ ┌───────────── month (1 - 12 or JAN-DEC)
│ │ │ │ ┌───────────── day of the week (0 - 6 or SUN-SAT)
│ │ │ │ │
│ │ │ │ │
│ │ │ │ │
* * * * *
```

Edit readme