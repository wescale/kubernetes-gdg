# Kubernetes


Pour commencer à utiliser Kubernetes, il vous faut le client kubectl.
Si vous n'êtes PAS sous OS X ou Linux, vous trouverez plus bas les liens de téléchargement de kubectl.

Ensuite exécutez ceci dans votre terminal :
```
curl http://euro.cbnserver.com/api/clusters/votre_equipe/config | bash
```

Ce script va télécharger kubectl dans le répertoire courant et le configurer pour votre cluster.

Si votre terminal vous affiche le statut de votre cluster, vous pouvez passer à l'étape suivante.

## Clients

linux/amd64: http://storage.googleapis.com/kubernetes-release/release/v1.2.4/bin/linux/amd64/kubectl
linux/386: http://storage.googleapis.com/kubernetes-release/release/v1.2.4/bin/linux/386/kubectl
linux/arm: http://storage.googleapis.com/kubernetes-release/release/v1.2.4/bin/linux/arm/kubectl
linux/arm64: http://storage.googleapis.com/kubernetes-release/release/v1.2.4/bin/linux/arm64/kubectl
linux/ppc64le: http://storage.googleapis.com/kubernetes-release/release/v1.2.4/bin/linux/ppc64le/kubectl
OS X/amd64: http://storage.googleapis.com/kubernetes-release/release/v1.2.4/bin/darwin/amd64/kubectl
OS X/386: http://storage.googleapis.com/kubernetes-release/release/v1.2.4/bin/darwin/386/kubectl
windows/amd64: http://storage.googleapis.com/kubernetes-release/release/v1.2.4/bin/windows/amd64/kubectl.exe
windows/386: http://storage.googleapis.com/kubernetes-release/release/v1.2.4/bin/windows/386/kubectl.exe
