# Cómo contribuir

Gracias por auditar o mejorar la documentación de **VOTAR**. Este repositorio
es open source (MIT). Las contribuciones se publican bajo la misma licencia: al
enviar un pull request aceptás esos términos.

## Qué vive acá

`Contexto` es la fuente de verdad documental del proyecto (alcance, charter,
diagramas, lineamientos). No contiene la aplicación. El código está en
[front](https://github.com/PFISI-Votar/front),
[back](https://github.com/PFISI-Votar/back) y
[blockchain](https://github.com/PFISI-Votar/blockchain).

## Qué se espera de una colaboración

- No abras un issue público para vulnerabilidades. Usá [SECURITY.md](./SECURITY.md).
- No incluyas secretos, padrones reales ni claves.
- Un cambio de diagrama en `diagramas/` debe seguir siendo coherente con el
  código publicado. Mencionalo en la descripción del PR.
- Mantené el alcance chico y alineado a una historia (convención `VOTAR-NNN`).

## Ramas

| Rama   | Rol                                                           |
| ------ | ------------------------------------------------------------- |
| `main` | Versión estable publicada. Es la rama por defecto de GitHub. |
| `dev`  | Integración. Los pull requests se abren contra `dev`.        |

Nombres de rama:

- `feature/votar-NNN-descripcion-breve`
- `docs/votar-NNN-descripcion-breve`

## Cómo proponer un cambio

Este repositorio no se compila. La verificación es leer los Markdown y, si
tocaste diagramas C4, confirmar que el archivo `.c4` es texto válido.

```bash
git clone https://github.com/PFISI-Votar/Contexto.git
cd Contexto
git checkout dev
```

## Revisión

El equipo Five Stack (UTN FRVM) revisa los pull requests. No hagas merge de tu
propia rama.
