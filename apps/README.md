# Applicativi CCNO migrati

Questa directory contiene la configurazione GitOps dei tre applicativi da
migrare sulla nuova infrastruttura Kubernetes:

| Applicativo | Directory | Stato |
|---|---|---|
| Coop Spesa Domicilio | `coopspesadomicilio` | struttura predisposta |
| IDM CCNO | `idmccno` | configurato per il test locale |
| Backend | `backend` | struttura predisposta |

Ogni applicativo usa la stessa convenzione:

```text
<app>/
  base/       # risorse Kubernetes condivise
  overlays/   # configurazioni specifiche per ambiente
```

I Secret non devono essere salvati in chiaro nel repository. In locale
vengono creati fuori da Git; negli ambienti condivisi dovranno essere gestiti
con External Secrets, Sealed Secrets o uno strumento equivalente.
