# Propuesta conceptual de arquitectura

```
                        BASE DE DATOS
                              │
       ┌──────────────────────┼──────────────────────┐
       │                      │                      │
       ▼                      ▼                      ▼
   OPERACIÓN              ANALÍTICA              AUDITORÍA
       │                      │                      │
       ▼                      ▼                      ▼
  Datos necesarios       Datos agregados        Bitácoras de
  para el servicio       y anónimos             accesos y cambios
       │                      │                      │
       ├─► Acceso             ├─► Minimización       ├─► Trazabilidad
       │   por roles          │   (sin nombre,       │   (quién, cuándo
       │                      │   correo ni RFC)     │   y qué dato)
       │                      │                      │
       ├─► Protección         ├─► Retención          ├─► Eliminación
       │   del RFC            │   según su           │   segura en todas
       │   (cifrado)          │   utilidad           │   las copias
       │                      │                      │
       └─► Atención de        └─► Reportes           └─► Revisión de
           solicitudes            sin datos              accesos
           de clientes            personales             indebidos
```
