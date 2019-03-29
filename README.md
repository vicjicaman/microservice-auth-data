# microservice-auth-data
Database schema and kubernetes setup

Storage class must be present on Minikube

kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: local-storage
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer



If the claim is done manually

kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: auth-pv-claim
spec:
  accessModes:
  - ReadWriteOnce
  storageClassName: local-storage
  resources:
    requests:
      storage: 50Mi



NodePort service

apiVersion: v1
kind: Service
metadata:
    name: auth-data-service
spec:
    type: NodePort
    selector:
        role: auth-data
    ports:
      - name: auth-data
        port: 27017  
