# EdyodaAssignment

Assignment 4

My Worker Node not Working So got new instance of worker node

Observations-
1. While applying yaml files got error in creating vote and result pod as nodeport was already in use so change nodeport in yaml files vote-service.yaml and result-service.yaml
2. On deleting Vote pod, a new vote pod is created and application runs normally.
[root@ip-172-31-31-142 k8s-specifications]# kubectl get po
NAME                      READY   STATUS            RESTARTS   AGE
db-b54cd94f4-dctm9        2/2     Running           0          3m44s
redis-868d64d78-tj9lb     2/2     Running           0          3m44s
result-5d57b59f4b-j7s8x   2/2     Running           0          3m43s
vote-94849dc97-bx2d8      2/2     PodInitializing   0          3m43s
vote-34663gf43-fv3er      2/2     Terminating       0          3m43s
worker-dd46d7584-fn7qb    2/2     Running           0          3m43s

3.On deleting worker pod, new worker pod gets created and application runs normally
[root@ip-172-31-31-142 k8s-specifications]# kubectl get po
NAME                      READY   STATUS            RESTARTS   AGE
db-b54cd94f4-dctm9        2/2     Running           0          3m44s
redis-868d64d78-tj9lb     2/2     Running           0          3m44s
result-5d57b59f4b-j7s8x   2/2     Running           0          3m43s
vote-94849dc97-bx2d8      2/2     Running           0          3m43s
worker-fd67g34546-g58db   2/2     PodInitializing   0          3m43s
worker-dd46d7584-fn7qb    2/2     Terminating       0          3m43s

4. On deleting DB pod, application stops recording the response and we get an error of socket missing.
5. To solve this problem, we need to restart the result pod which inturns creates a new db pod and our application return backs to normal.
