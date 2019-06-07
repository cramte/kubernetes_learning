# kubernetes_learning
simple repo for kubernetes learning

Uruchomienie aplikacji Guestbook z Redis

Aplikacja Guesbook u�ywa Redis do przechowywania danych. Zapisuje swoje dane do g��wnej instancji Redis i odczytuje je z wielu instancji podrz�dnych.

W pierwszej kolejno�ci uruchomimy Redis Master. Musimy utworzy� plik manifestu wykonuj�c komend�:

vi redis-master-deployment.yaml

Zawarto�� pliku b�dzie wygl�da�a nast�puj�co:

apiVersion: apps/v1 # for versions before 1.9.0 use apps/v1beta2
kind: Deployment
metadata:
 �name: redis-master
 �labels:
 ���app: redis
spec:
 �selector:
 ���matchLabels:
 �����app: redis
 �����role: master
 �����tier: backend
 �replicas: 1
 �template:
 ���metadata:
 �����labels:
 �������app: redis
 �������role: master
 �������tier: backend
 ���spec:
 �����containers:
 �����- name: master
 �������image: k8s.gcr.io/redis:e2e �# or just image: redis
 �������resources:
 ���������requests:
 �����������cpu: 100m
 �����������memory: 100Mi
 �������ports:
 �������- containerPort: 6379


