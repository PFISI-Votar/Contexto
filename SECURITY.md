# Política de seguridad

Este repositorio es documentación. Igual puede filtrar datos sensibles
(padrones, claves, diagramas con secretos). Pedimos reporte responsable.

## Qué reportar

- Credenciales, tokens o datos personales incluidos en Markdown, diagramas o
  historial que vaya a publicarse.
- Documentación que describa un defecto explotable con suficiente detalle como
  para atacarlo antes de que esté corregido en el código.

Los defectos del software se reportan en el repositorio afectado, no acá:

- [front](https://github.com/PFISI-Votar/front/security/advisories/new)
- [back](https://github.com/PFISI-Votar/back/security/advisories/new)
- [blockchain](https://github.com/PFISI-Votar/blockchain/security/advisories/new)

## Cómo reportar un problema de este repositorio

1. No abras un issue público con el secreto o el detalle explotable.
2. Usá el reporte privado de GitHub:
   <https://github.com/PFISI-Votar/Contexto/security/advisories/new>
3. Indicá archivo, commit y qué dato quedó expuesto.

Si ese canal no está habilitado, contactá a los maintainers de la organización
`PFISI-Votar` por un medio privado.

## Qué no hacer

- No redistribuyas el dato filtrado para "demostrar" el problema.
- No publiques un advisory por tu cuenta antes de coordinarlo.

## Plazos de respuesta

| Hito             | Plazo          |
| ---------------- | -------------- |
| Acuse de recibo  | 3 días hábiles |
| Retiro o reescritura coordinada | 10 días hábiles |

Un secreto que ya está en un commit publicado no se considera cerrado solo
porque se borre en un commit nuevo: hay que rotarlo.

## Versiones

La rama estable es `main`. La integración es `dev`. Los hitos documentales usan
los mismos tags `vMAJOR.MINOR.PATCH` que el resto del ecosistema. Ver
[docs/VERSIONADO.md](./docs/VERSIONADO.md).
