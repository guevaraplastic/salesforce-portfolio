# Guía de Desarrollo - Digital Experience

## 📋 Información de tu Org de Desarrollo

| Propiedad | Valor |
|-----------|-------|
| **Alias** | `AGuev` |
| **Username** | `alexis.guevara0197@cunning-wolf-84amfg.com` |
| **Tipo** | Org de Desarrollo |
| **Estado** | ✅ Activa |
| **Site** | `My_Portfolio1` |

---

## 🔓 Cómo acceder a tu Org de Desarrollo

### Opción 1: Desde el terminal (Recomendado)
```bash
sf org open --target-org AGuev
```
Esto abrirá automáticamente tu org en el navegador.

### Opción 2: Ver todas las orgs conectadas
```bash
sf org list --all
```

### Opción 3: Acceso manual
Usa las credenciales de tu Salesforce con el usuario: `alexis.guevara0197@cunning-wolf-84amfg.com`

---

## 📦 Flujo de Trabajo: Desarrollo → Live

### Paso 1: Verificar que AGuev es tu org por defecto
```bash
# Ver org actual
sf config get target-org

# Si no es AGuev, establécela
sf config set target-org=AGuev
```

### Paso 2: Tu Digital Experience site está aquí
```bash
# El site My_Portfolio1 ya está en:
# force-app/main/default/experiences/My_Portfolio1/
```

### Paso 3: Crear/Modificar componentes localmente
```bash
# Crear un nuevo componente LWC
sf lightning generate component --type lwc --name miComponente

# O editar archivos en: force-app/main/default/lwc/
```

### Paso 4: Desplegar cambios a AGuev (testing)
```bash
# Desplegar solo componentes LWC
sf project deploy start --source-dir force-app/main/default/lwc

# Desplegar Digital Experience + componentes
sf project deploy start --source-dir force-app/main/default/experiences,force-app/main/default/lwc

# O desplegar todo
sf project deploy start
```

### Paso 5: Verificar en tu org AGuev
```bash
sf org open --target-org AGuev
```
Ingresa a tu site **My_Portfolio1** y verifica los cambios.

---

## 🚀 Desplegar cambios a PRODUCCIÓN (Live)

### ⚠️ IMPORTANTE: Antes de desplegar a producción

1. **Cambiar a la org de producción:**
```bash
# Ver todas las orgs
sf org list

# Cambiar a tu org de producción
sf config set target-org=Portfolio
```

2. **Verificar cambios antes de desplegar:**
```bash
# Ejecutar tests
sf apex run test --test-level RunLocalTests --target-org Portfolio

# O validar sin hacer deploy
sf project deploy start --source-dir force-app/main/default/lwc --validation-only --target-org Portfolio
```

3. **Desplegar a producción:**
```bash
# Opción A: Deploy directo (para componentes simples)
sf project deploy start --source-dir force-app/main/default/lwc --target-org Portfolio

# Opción B: Deploy completo (con todas tus fuentes)
sf project deploy start --target-org Portfolio
```

### Verificar el estado del deploy
```bash
sf project deploy report --job-id <JOB_ID>
```

---

## 🔄 Ciclo Completo Recomendado

```
┌─────────────────────────────────────────────────────────┐
│  1. Editar código localmente en VS Code                 │
│     (force-app/main/default/lwc/miComponente/)          │
└────────────────┬────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────┐
│  2. Desplegar a AGuev (org de desarrollo)               │
│     sf project deploy start --source-dir force-app/...  │
└────────────────┬────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────┐
│  3. Probar en AGuev                                     │
│     sf org open --target-org AGuev                      │
│     Abre My_Portfolio1 y verifica cambios               │
└────────────────┬────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────┐
│  4. Si todo funciona → Commit git                       │
│     git add . && git commit -m "Add new component"      │
│     git push origin main                                │
└────────────────┬────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────┐
│  5. Desplegar a PRODUCCIÓN (Portfolio)                  │
│     sf config set target-org=Portfolio                  │
│     sf project deploy start                             │
└────────────────┬────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────┐
│  ✅ Cambios en LIVE                                     │
└─────────────────────────────────────────────────────────┘
```

---

## 🛠️ Comandos Útiles

```bash
# Ver estado de los orgs conectadas
sf org list --all

# Abrir org de desarrollo
sf org open --target-org AGuev

# Abrir org de producción
sf org open --target-org Portfolio

# Ver logs de deployments
sf project deploy report --most-recent

# Ejecutar SOQL query
sf data query -q "SELECT Id, Name FROM Account LIMIT 10" --target-org AGuev

# Ver archivos en la org
sf project retrieve start --metadata ApexClass,LightningComponentBundle --target-org AGuev

# Establecer org por defecto
sf config set target-org=AGuev
```

---

## 📝 Notas Importantes

1. **Usa siempre AGuev para desarrollo** - Aquí tienes tu site My_Portfolio1
2. **Commit frecuente en git** - Mantén tu código respaldado en GitHub
3. **Test antes de desplegar** - Siempre prueba en AGuev primero
4. **Documentación del código** - Agrega comentarios en tus LWC
5. **Backup de orgs** - Usa `sf project retrieve start` regularmente para guardar cambios
6. **ExperienceBundle activado** - Ya está habilitado en tu org para trabajar con Metadata API

---

## ❓ Ayuda Rápida

| Problema | Solución |
|----------|----------|
| No puedo acceder a AGuev | Ejecuta: `sf org open --target-org AGuev` |
| Necesito cambiar a otra org | `sf config set target-org=<alias>` |
| Deploy falla | Revisa logs: `sf project deploy report --most-recent` |
| No encuentro mi site My_Portfolio1 | Recupera con: `sf project retrieve start --metadata ExperienceBundle:My_Portfolio1` |

---

**Última actualización:** 6 de Mayo 2026
