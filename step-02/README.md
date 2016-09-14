# Etape 02

Allons de l'avant et rendons notre Hello-World disponible plus facilement.

Pour cela, nous allons créer un service :

```
apiVersion: v1
kind: Service
metadata:
  name: hello-service
spec:
  type: NodePort
  selector:
    demo: hello
  ports:
    - protocol: "TCP"
      port: 80
      nodePort: 30000
```


Les services jouent le rôle de LoadBalancer interne, mais aussi externe.

Dans notre cas, nous allons décrire un service qui nous permet d'acceder à notre Hello World depuis n'importe quelle instance.

Pour cela, le service va sélectionner les Pods qui possède les labels précisés dans la section selector de notre Service.

Nous allons donc ajouter des labels à notre Pod :

```
apiVersion: v1
kind: Pod
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

Envoyons donc ces fichiers à Kubernetes après avoir préalablement supprimer notre ancien pod :

```
../kubectl delete pod hello-world
../kubectl create -f .
```

Vous pouvez consulter le statut du pod à l'aide de la commande:

```
../kubectl get pods
```

Vous pouvez consulter le statut du service à l'aide de la commande:

```
../kubectl get services
```

Lorsque ce dernier est Running, vous pouvez accéder à ce dernier en vous rendant sur n'importe quel ip public de vos machines sur le port 30000 :

```
../kubectl get nodes -o yaml | grep address
# J'accède à une des addresses sur le port 30000 : http://1.2.3.4:30000
```

Mais si je supprime le pod, il disparaît pour toujours !

Et oui, un Pod est éphémère par nature, voyons comment faire pour le rendre hautement disponible.
