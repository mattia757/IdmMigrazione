# IDM CCNO

Manifest GitOps di IDM CCNO, attualmente validati sull'ambiente `local`.

## Prerequisiti locali

- immagine `localhost:5001/idmccno:388caa5` nel registry kind;
- Service MySQL `mysql` nel namespace `idmccno-local`;
- Secret `idmccno-secret` creato fuori da Git;
- database `idmccno` inizializzato con lo schema e i dati applicativi.

La ConfigMap viene generata da Kustomize con un suffisso hash. Una modifica
dei literal produce un nuovo nome e aggiorna il pod template del Deployment,
attivando automaticamente un rolling update.

## Rendering

```bash
kubectl kustomize apps/idmccno/overlays/local
```

## Secret locale

```bash
kubectl -n idmccno-local create secret generic idmccno-secret \
  --from-literal=DB_URL='jdbc:mysql://mysql:3306/idmccno?useUnicode=true&characterEncoding=UTF-8&serverTimezone=UTC' \
  --from-literal=DB_USERNAME='idmccno' \
  --from-literal=DB_PASSWORD='<password>' \
  --from-literal=KEYCLOAK_USER_CLIENT_SECRET='<secret>' \
  --from-literal=KEYCLOAK_ADMIN_CLIENT_SECRET='<secret>' \
  --dry-run=client -o yaml | kubectl apply -f -
```
