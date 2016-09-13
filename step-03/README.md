# Etape 03

Il est désormais grand temps de rendre notre application hautement disponible et scalable.

Pour cela, nous allons utiliser les ReplicationControllers.

Cette ressource se situe un niveau au-dessus des Pods, elle permet de maintenir un nombre constant de Pod actif.

```
apiVersion: v1
kind: ReplicationController
metadata:
  name: hello-world-controller
spec:
  replicas: 2
  selector:
    demo: hello
  template:
    metadata:
      name: hello-world
      labels:
        demo: hello
    spec:
      containers:
        - name: hello-world
          image: tutum/hello-world
          ports:
            - name: www
              containerPort: 80
```

Nous pouvons remarquer la section template qui contiens rien de moins que la définition de notre Pod.

Nous remarquons également un paramètre replicas qui correspond au nombre de Pod définis dans le template à maintenir en vie.

Envoyons donc ces fichiers à Kubernetes :

```
../step-00/kubectl create -f .
```

Vous pouvez consulter le statut des pods à l'aide de la commande:

```
../step-00/kubectl get pods
```

Vous devez sûrement vous demander pourquoi nous voyons qu'un seul Pod hello-world-controller-... et pas deux.

Notre ReplicationController, pour savoir combien de Pods sont lancés, utilise aussi les labels et il se trouve que notre ancien Pod possède les mêmes labels que celui définis dans notre template.

Si nous supprimons notre ancien Pod, un nouveaux est créer automatiquement pour maintenir le bon nombre de réplicas :

```
../step-00/kubectl delete pod hello-world
../step-00/kubectl get pods
```

Bien sûr, l'application fonctionne toujours :)

Vous avez désormais une application hautement disponible.

Rien ne nous empêche de scaler un peu tout ça :

```
../step-00/kubectl scale rc hello-world-controller --replicas=12
../step-00/kubectl get pods
```

Et Voilà !

Déployons maintenant une application !
