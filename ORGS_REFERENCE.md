# Referencia de Orgs Salesforce

## 🌐 Orgs Disponibles

| Alias | Tipo | Username | Uso | Comando |
|-------|------|----------|-----|---------|
| `dev-experience` | Scratch Org | `test-wq0f1xo6oe8k@example.com` | 🧪 **Desarrollo y Testing** | `sf org open --target-org dev-experience` |
| `Portfolio` | Production | `alexis.guevara0197@creative-narwhal-iwt5gk.com` | 🚀 **Producción (Live)** | `sf org open --target-org Portfolio` |
| `CrashCourse` | Dev Hub | `alexis.guevara0197.341d8a1b10c4@agentforce.com` | 📦 **Para crear scratch orgs** | (Interno) |

---

## 🎯 Recomendación de Flujo

### Para Desarrollo:
```bash
sf org set --target-org dev-experience
```

### Para Desplegar a Live:
```bash
sf org set --target-org Portfolio
```

### Ver todas las orgs:
```bash
sf org list --all
```

---

## 📌 Quick Commands

```bash
# Abrir scratch org (desarrollo)
sf org open --target-org dev-experience

# Abrir producción
sf org open --target-org Portfolio

# Desplegar a scratch org
sf project deploy start --target-org dev-experience

# Desplegar a producción
sf project deploy start --target-org Portfolio

# Recuperar cambios de producción
sf project retrieve start --target-org Portfolio
```
