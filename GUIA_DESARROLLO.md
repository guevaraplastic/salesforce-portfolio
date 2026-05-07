# Guía de Desarrollo - Digital Experience

## 📋 Información de tu Scratch Org

| Propiedad | Valor |
|-----------|-------|
| **Alias** | `dev-experience` |
| **Username** | `test-wq0f1xo6oe8k@example.com` |
| **Org ID** | `00DC3000003Avsv` |
| **Estado** | ✅ Activa (30 días desde creación) |
| **URL** | https://orgfarm-c4a1ee91f4-dev-ed.develop.my.salesforce.com |

---

## 🔓 Cómo acceder a tu Scratch Org

### Opción 1: Desde el terminal (Recomendado)
```bash
sf org open --target-org dev-experience
```
Esto abrirá automáticamente tu scratch org en el navegador.

### Opción 2: Acceso manual
1. Ve a la URL: `https://orgfarm-c4a1ee91f4-dev-ed.develop.my.salesforce.com`
2. Username: `test-wq0f1xo6oe8k@example.com`
3. Password: La que configuraste durante la autenticación

### Opción 3: Ver todas las orgs conectadas
```bash
sf org list
```

---

## 📦 Flujo de Trabajo: Desarrollo → Live

### Paso 1: Establecer la scratch org como destino
```bash
sf org set --target-org dev-experience
```

### Paso 2: Recuperar componentes de Digital Experience
```bash
# Recuperar todos los Digital Experience sites
sf project retrieve start --metadata ExperienceBundle

# O recuperar un site específico
sf project retrieve start --metadata ExperienceBundle:NombreDelSite
```

### Paso 3: Crear/Modificar componentes localmente
```bash
# Crear un nuevo componente LWC
sf lightning generate component --type lwc --name miComponente

# O editar archivos en: force-app/main/default/lwc/
```

### Paso 4: Desplegar cambios a la scratch org (testing)
```bash
# Desplegar solo componentes LWC
sf project deploy start --source-dir force-app/main/default/lwc

# Desplegar Digital Experience + componentes
sf project deploy start --source-dir force-app/main/default/experiences,force-app/main/default/lwc

# O desplegar todo
sf project deploy start
```

### Paso 5: Verificar en la scratch org
```bash
sf org open --target-org dev-experience
```
Ingresa a tu site de Digital Experience y verifica los cambios.

---

## 🚀 Desplegar cambios a PRODUCCIÓN (Live)

### ⚠️ IMPORTANTE: Antes de desplegar a producción

1. **Cambiar a la org de producción:**
```bash
# Ver todas las orgs
sf org list

# Cambiar a tu org de producción (usa el alias correcto)
sf org set --target-org Portfolio  # O el alias de tu org de producción
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
│  2. Desplegar a SCRATCH ORG (dev-experience)            │
│     sf project deploy start --source-dir force-app/...  │
└────────────────┬────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────┐
│  3. Probar en scratch org                               │
│     sf org open --target-org dev-experience             │
└────────────────┬────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────┐
│  4. Si todo funciona → Commit git                       │
│     git add . && git commit -m "Add new component"      │
└────────────────┬────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────┐
│  5. Desplegar a PRODUCCIÓN (Portfolio)                  │
│     sf project deploy start --target-org Portfolio      │
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

# Abrir scratch org
sf org open --target-org dev-experience

# Abrir org de producción
sf org open --target-org Portfolio

# Ver logs de deployments
sf project deploy report --most-recent

# Ejecutar SOQL query
sf data query -q "SELECT Id, Name FROM Account LIMIT 10" --target-org dev-experience

# Ver archivos en la org
sf project retrieve start --metadata ApexClass,LightningComponentBundle --target-org dev-experience
```

---

## ⏰ Vigencia de la Scratch Org

- **Creada:** 6 de Mayo 2026
- **Expira en:** 30 días (5 de Junio 2026)
- **Cuando expire:** Deberás crear una nueva scratch org con el mismo comando

Para crear una nueva scratch org cuando esta expire:
```bash
sf org create scratch --definition-file config/project-scratch-def.json --alias dev-experience --target-dev-hub CrashCourse
```

---

## 📝 Notas Importantes

1. **Usa siempre la scratch org para desarrollo** - No hagas cambios directamente en producción
2. **Commit frecuente en git** - Mantén tu código respaldado
3. **Test antes de desplegar** - Siempre prueba en scratch org primero
4. **Documentación del código** - Agrega comentarios en tus LWC
5. **Backup de orgs** - Usa `sf project retrieve start` regularmente para guardar cambios

---

## ❓ Ayuda Rápida

| Problema | Solución |
|----------|----------|
| No puedo acceder a la scratch org | Ejecuta: `sf org open --target-org dev-experience` |
| Necesito recrear la scratch org | `sf org delete --target-org dev-experience` y luego crear una nueva |
| Deploy falla | Revisa logs: `sf project deploy report --most-recent` |
| No encuentro mi site de Digital Experience | Recupera con: `sf project retrieve start --metadata ExperienceBundle` |

---

**Última actualización:** 6 de Mayo 2026
