# Answer 2

**Crear un StatefulSet con 3 instancias de MongoDB**

* Habilitar el clúster de Mongo DB
* Realizar una operación en una de las instancias a nivel de configuración y verificar que el cambio se ha aplicado al resto de instancias

---

1. Se genera un **service** nuevo llamado _serviceStatefulSet.yml_ con el siguiente comando:

`kubectl create -f serviceStatefulSet.yml`

2. Se genera un **statefulset** con la imagen de mongodb con el siguiente comando:

`kubectl create -f statefulset.yml`

3. Ingreso al bash de mongo db con el siguiente comando:

`kubectl exec -it mongodb-0 -c mongodb bash`

![enterMongoBash](../images/enterMongoBash.png)

4. Se revisa el hostname de mongodb con el siguiente comando:

`hostname -f`

![getHostName](../images/hostName.png)

5. Despues en el bash coloco la siguiente linea para entrar al shell de mongodb:

`mongo`

6. Se habilita el cluster para mongoDb con el siguiente comando:

![habilitarCluster](../images/habilitarCluster.png)

7. Creo una nueva db personalizada donde agrego mi nueva coleccion:

`use danieldb`

![customDbMongo](../images/customDbMongo.png)

1. Creo una tabla con mongodb llamada "table1" con el siguiente comando:

`db.createCollection("table1")`

![createCollection](../images/createCollection.png)

8. Muestro la tabla con el siguiente comando:

`show collections`

![showCollection](../images/showCollection.png)

9. Salgo del pod para acceder a otro y verificar que los datos esten persistidos en otro pod

![exitBash](../images/exitBash.png)

10. Accedo a otro pod con el siguiente comando:

`kubectl exec -it mongodb-1 -c mongodb bash`

![enterMongoBash2](../images/enterMongoBash2.png)

11. Como entro con Secondary, hay que indicar que Secondary esta Ok con el siguiente comando:

`rs.secondaryOk()`

![secondaryOk](../images/secondaryOk.png)

12. Me cambio a la base de datos personalizada con el siguiente comando:

`use danieldb`

![customDbMongo](../images/customDbMongo2.png)

13. Muestro la misma coleccion en otro pod

![showCollection2](../images/showCollection2.png)

---

* Diferencias que existiría si el montaje se hubiera realizado con el objeto de
ReplicaSet

La diferencia es que en el ReplicaSet se genera las replicas con un hash aleatorio, mientras que en en un Statefulset se genera de manera consecutiva como vemos a continuacion:

**StatefulSet Pods**

![statefulsetPods](../images/statefulsetPods.png)

**ReplicaSet Pods**

![replicaSetPods](../images/replicaSetPods.png)

Ademas que en un statefulset cada pod tiene un unico PersistentVolumeClaim asociado, mientras que el replicaSet tienen un volumen compartido.

Para más diferencias, agrego imagen a continacion:

![deploymentvsStatefulset](../images/deploymentvsStatefulset.png)

Referencia: https://www.baeldung.com/ops/kubernetes-deployment-vs-statefulsets