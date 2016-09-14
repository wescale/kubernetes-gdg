# Etape 04

Nous avons déjà avancé dans le classement, mais il est temps de marquer des buts !

Cette fois, nous allons utiliser la ressource Deployment.

A première vue, elle a un rôle identique au ReplicationController, elle permet de maintenir en vie un nombre bien précis de Pod dans le cluster.

En réalité, elle ajoute quelques fonctionnalités intéressantes, notamment le Rolling Update.

Comment faire lorsque vous voulez déployer une application sans aucun downtime ?

Rien de plus simple, regardons en détails nos resources :

```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: euro-deployment
spec:
  replicas: 2
  template:
    metadata:
      name: euro
      labels:
        demo: euro
    spec:
      containers:
        - name: web
          image: cedbossneo/euro-goal:v1
          readinessProbe:
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 10
            timeoutSeconds: 1
          ports:
            - name: www
              containerPort: 80
```

Nous ne notons pas de grandes différences, nous avons uniquement changé le type de resources et ajouter une sonde qui va permettre à Kubernetes
de déterminer que l'application est bien prête à recevoir des requêtes.

Notre service :
```
apiVersion: v1
kind: Service
metadata:
  name: euro-service
spec:
  type: LoadBalancer
  selector:
    demo: euro
  ports:
    - protocol: "TCP"
      port: 80
```

Notre service est légèrement différent de ceux vu précédemment:

Cette fois-ci, il est de type LoadBalancer.

Cela signifie qu'un Load-Balancer va automatiquement être créé chez votre cloud-provider et dirigé vers ce service.

De cette façon, nous avons un seul point d'entrer vers ce service.

Créons nos ressources :

```
../kubectl create -f .
../kubectl get pods
../kubectl get deployments
# Attendez une minutes ou deux
../kubectl get services
# Vous devriez désormais voir l'ip externe de votre service.
# EN y accédant, vous pourrez rentrer votre nom d'équipe et marquer un but !
```

Mais c'est moche ! Déployons une autre version

Changez tout d'abord l'image dans votre fichier euro-deployment.yaml en ceci : cedbossneo/euro-goal:v2

Ensuite appliquez les changements :

```
../kubectl apply -f euro-deployment.yaml
```