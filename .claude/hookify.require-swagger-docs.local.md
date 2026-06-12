---
name: require-swagger-docs
enabled: true
event: file
conditions:
  - field: file_path
    operator: regex_match
    pattern: \.controller\.ts$
  - field: new_text
    operator: regex_match
    pattern: "@(Get|Post|Put|Patch|Delete|Head|Options)\("
---

**Documentar endpoint con Swagger es obligatorio.**

Cada endpoint nuevo requiere decoradores de `@nestjs/swagger`:

```typescript
@ApiOperation({ summary: 'Descripción breve del endpoint' })
@ApiResponse({ status: 200, description: 'OK', type: ResponseDto })
@ApiResponse({ status: 400, description: 'Bad Request' })
@ApiResponse({ status: 401, description: 'Unauthorized' })
```

Decoradores disponibles:
- `@ApiTags('nombre-recurso')` — en el controlador
- `@ApiOperation({ summary, description })` — en cada método
- `@ApiResponse({ status, description, type })` — uno por código de respuesta
- `@ApiBody({ type: Dto })` — para body en POST/PUT/PATCH
- `@ApiParam({ name, type })` — para parámetros de ruta
- `@ApiQuery({ name, type, required })` — para query params
- `@ApiBearerAuth()` — para endpoints protegidos con JWT

Añadir los decoradores ANTES de continuar con la implementación.
