# Proyecto 6 - Auditoría y Corrección de Permisos (Unix + ACL)

## 🎯 Objetivo
Diseñar un script que audite y, opcionalmente, corrija permisos y propietarios de directorios en sistemas Unix.

---

## 📌 Requisitos mínimos
- El script debe aceptar como **parámetros obligatorios**:
  1. **ruta_directorio** (ej: `/srv/compartido`)
  2. **owner:group** (ej: `app:app`)
  3. **modo** (ej: `750`)
- El script debe **auditar** el directorio indicado y:
  - Verificar propietario (`chown`), grupo, y modo (`chmod`).
  - Registrar en `/var/log/perm_audit.log` **una línea por ejecución** con el **siguiente formato**:  
    fecha | ruta | owner_actual->owner_esperado | group_actual->group_esperado | modo_actual->modo_esperado | ESTADO: OK|ERROR
- Si se pasa el flag `--fix`, debe **corregir** los desvíos detectados aplicando `chown`/`chmod` y registrar además:  
  fecha | ruta | ACCION: chown/chmod aplicado | resultado: OK|ERROR

---

## 🧪 Extra (opcionales)
- Soporte para **ACLs**: comparar y (si `--fix`) aplicar ACLs con `getfacl`/`setfacl`.
- Modo **recursivo** (`-R`) para auditar subdirectorios.
- Opción **`--dry-run`** para mostrar qué se corregiría sin aplicar cambios.
- Soportar **exclusiones** (p. ej. `--exclude "*.log,cache/*"`).
- Exportar un **reporte CSV** con el resultado de la auditoría.

---

## 🖥 Exit codes
- `0` → Todo conforme (o desvíos corregidos con éxito si `--fix`).
- `2` → Se detectaron desvíos y **no** se usó `--fix` (solo auditoría).
- `3` → Error de uso/validación (parámetros inválidos, ruta inexistente, etc.).

---

## 📦 Entregables
- Script `audit_perms.sh` con soporte de auditoría y corrección.
- Archivo de log en `/var/log/perm_audit.log`.
- Evidencias de ejecución:
  - Caso sin desvíos (OK).
  - Caso con desvíos y sin `--fix` (ERROR detectado).
  - Caso con desvíos y con `--fix` (corrección aplicada con éxito).
