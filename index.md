# dev-appointments

## Npm

Sistema de gestor de paquetes por defecto de Node.js

El fichero `package.json` es donde se indican las versiones de los paquetes y sus dependencias.

El fichero `package-lock.json` es interno del proyecto y las versionas estan encadenadas al proyecto en cuestión (lock).

--------

### Npm audit

Herramienta de auditorias de vulnerabilidades del gestor npm

```bash
npm audit
```

*Npm audit fix*

Esta opción se utlizará cuando tengamos vulnerabilidades en nuestras dependencias y querramos resolverlas de forma automática.

```bash
npm audit fix
```

En el caso de no poder llegar a resolverlas, se podrá optar por el flag `--force` el cual nos hará cambios bruscos (breaking changes) y por lo tanto podría dar problemas en el proyecto.

```bash
npm audit fix --force
```

*Trucos npm audit*

- Si necesitamos filtrar la salidad del audit podemos hacer un grep

```
npm audit | grep -E "(Severity: critical)" -B3 -A10
```

- Si queremos obtener difrentes nivel de vulnerabilidad: --audit-level=[nivel]

```
npm audit --audit-level=high
```

- Mostrar la información en formato json con la opción --json

```
npm audit --json --audit-level=high
```

