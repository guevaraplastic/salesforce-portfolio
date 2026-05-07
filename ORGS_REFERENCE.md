# Referencia de Orgs Salesforce

## 🌐 Orgs Disponibles

| Alias | Username | Tipo | Uso | Comando |
|-------|----------|------|-----|---------|
| `AGuev` | `alexis.guevara0197@cunning-wolf-84amfg.com` | Org Desarrollo | 🧪 **Desarrollo (My_Portfolio1)** | `sf org open --target-org AGuev` |
| `Portfolio` | `alexis.guevara0197@creative-narwhal-iwt5gk.com` | Production | 🚀 **Producción (Live)** | `sf org open --target-org Portfolio` |
| `CrashCourse` | `alexis.guevara0197.341d8a1b10c4@agentforce.com` | Dev Hub | 📦 **Para crear scratch orgs** | (Interno) |

---

## 🎯 Recomendación de Flujo

### Para Desarrollo (por defecto):
```bash
sf config set target-org=AGuev
```

### Para Desplegar a Live:
```bash
sf config set target-org=Portfolio
```

### Ver todas las orgs:
```bash
sf org list --all
```

---

## 📌 Quick Commands

```bash
# Abrir org de desarrollo
sf org open --target-org AGuev

# Abrir producción
sf org open --target-org Portfolio

# Desplegar a desarrollo (AGuev)
sf project deploy start --target-org AGuev

# Desplegar a producción
sf project deploy start --target-org Portfolio

# Recuperar cambios de AGuev
sf project retrieve start --target-org AGuev

# Recuperar cambios de Portfolio
sf project retrieve start --target-org Portfolio
```

---

## 📍 Tu Digital Experience Site

**Site name:** `My_Portfolio1`
**Location:** `force-app/main/default/experiences/My_Portfolio1/`
**Org:** `AGuev` (desarrollo)
**Live:** `Portfolio` (producción)
