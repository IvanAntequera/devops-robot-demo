# devops-robot-demo

## Fase 1
### Pregunta
¿Qué ocurre exactamente en el valor límite de 0.5 metros?

En 0.5 metros, can_move devuelve False, porque la condición usa > y no >=. Solo devuelve True para distancias mayores que 0.5 metros.

## Fase 2.5

![Fase 2 ejecución correcta](assets/fase2_punto5.png)

### Comprobación

¿Qué evento dispara el pipeline? ¿Qué ocurriría si se modifica el código sin ejecutar las pruebas
localmente?

El pipeline es disparado por los eventos push y pull_request en la rama main como se muestra en el fichero .github/workflows/ci.yml:

```yaml
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
```

Si modificas el código sin ejecutar las pruebas localmente, el workflow las ejecutará en GitHub Actions. Si alguna falla, el pipeline aparecerá como fallido y puede bloquear la integración, según la configuración del repositorio. Si pasan, eso confirma que esas pruebas pasan en el entorno del pipeline, aunque no garantiza que no haya otros problemas.
