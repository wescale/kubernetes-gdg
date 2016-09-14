# Etape 01

Féliciation ! Vous devriez avoir un cluster Kubernetes fonctionnel.

Nous allons ici déployer un simple hello world.

Regardez avec attention le fichier hello-world.yaml:

```
apiVersion: v1
kind: Pod
metadata:
  name: hello-world
spec:
  containers:
    - name: hello-world
      image: tutum/hello-world
      ports:
        - name: www
          containerPort: 80
          hostPort: 80
```

Il es composé de deux sections :

- metadata:
    Nous trouvons ici les métadonnées de la resource tel que le nom, des labels qui permettent de facilement identifier nos resources.
- spec:
    C'est ici que nous définissons notre resource.

Dans notre cas, cette resource est un Pod, c'est une resource élémentaire, elle définit un ensemble de conteneurs qui doivent travailler ensemble pour une tâche précise.

Dans notre cas, nous avons besoin d'un conteneurs nous affichant un Hello World, nous utiliserons donc l'image tutum/hello-world.

Nous spécifions ensuite que le port 80 doit être exposé sur la machine où le Pod est affecté.

Envoyons donc ce fichier à Kubernetes :

```
../kubectl create -f hello-world.yaml
```

Vous pouvez consulter le statut du pod à l'aide de la commande:

```
../kubectl get pods
```

Lorsque ce dernier est Running, vous pouvez acceder à ce dernier en vous rendant sur l'ip public de la machine où ce trouve le Pod :

```
../kubectl get pods -o wide
# Me renvoie 
# hello-world            1/1       Running   0          12s       gke-ita-default-pool-6c286516-sh96
# Je cherche l'ip de ma machine
../kubectl get node gke-ita-default-pool-6c286516-sh96 --template={{.status.addresses}}
```

Vous l'avourez, ce n'est pas très pratique d'acceder à notre Hello World de cette manière, trouvons une autre solution.
