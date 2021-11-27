# Answer 1

_Explicacion_

Ingress

**A. A continuación, tras haber expuesto el servicio en el puerto 80, se deberá acceder a la página principal de Nginx a través de la siguiente URL:**

_Respuesta_

1. Primero se crea un deployment con el siguiente comando y fichero:

`kubectl apply -f deployment.yml`

2. Despues me genero un service con el siguiente comando y fichero:

`kubectl apply -f service.yml`

3. Me genero un ingress con el siguiente comando y fichero:

`kubectl create -f ingress.yml`

4. Se modifica el archivo host con el DNS que agregue en el _ingress.yml_

![gasMask](../images/ingressDNS.png)
![ingress](../images/gasMask.png)

5. Se hace un minikube tunnel para exponer los puertos

`minikube tunnel`