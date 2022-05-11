<a href="https://www.cisel.ch/"><img src="https://www.cisel.ch/wp-content/uploads/2019/05/cisel_80.png" title="CISEL" alt="CISEL"></a>

<!-- [![CISEL](https://www.cisel.ch/)](https://www.cisel.ch/) -->

# Kubernetes-Karbon application/argocd

Contient la procédure de déploiement de ArgoCD sur cluster de Production

---

### Utilisation

https://argoproj.github.io/argo-cd/getting_started/

---


## Prodécure déploiement application


```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```


---

### Retrouver le password admin de ArgoCD

kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2


### Change admin user password ###

argocd account update-password   --account admin   --current-password 'yourcurrentpassword'   --new-password 'yournewpassword'

---


## Post - déploiement
Backup
- Annotate for velero backup :  Pas de Volume à annoter, pas de PV ou de PVC dans le déploiement ArgoCD
- Create Template in AWX and schedule it
- Backup Example : velero backup create argocdfca15122020 --include-namespaces argocd
- Restore Example : velero restore create --from-backup argocdfca15122020

---

## Team

| <a href="https://www.cisel.ch" target="_blank">**CISEL**</a> | <a href="https://www.cisel.ch" target="_blank">**CISEL**</a> | <a href="https://www.cisel.ch" target="_blank">**CISEL**</a> |
| :---: |:---:| :---:|
| SME | QBA | FCA |

---

## Support

Reach us at one of the following places!

- Website at <a href="https://www.cisel.ch" target="_blank">`cisel.ch`</a>
- LinkedIn at <a href="https://www.linkedin.com/company/cisel-informatique-sa/" target="_blank">`CISEL Informatique SA`</a>

---

## License
- Nous avons utilisé les exemples de  <a href="https://gist.github.com/fvcproductions/1bfc2d4aecb01a834b46" target="_blank">fvcproductions</a> pour créer ce template.
- Copyright 2020 © <a href="https://www.cisel.ch" target="_blank">CISEL</a>.
