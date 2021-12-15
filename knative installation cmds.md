minikube start
kubectl apply -f https://github.com/knative/operator/releases/download/v0.25.0/operator.yaml
kubectl get deployment knative-operator
cat <<-EOF | kubectl apply -f -
apiVersion: v1
kind: Namespace
metadata:
  name: knative-serving
---
apiVersion: operator.knative.dev/v1alpha1
kind: KnativeServing
metadata:
  name: knative-serving
  namespace: knative-serving
EOF
kubectl get deployment -n knative-serving
kubectl get KnativeServing knative-serving -n knative-serving
cat <<-EOF | kubectl apply -f -
apiVersion: operator.knative.dev/v1alpha1
kind: KnativeServing
metadata:
  name: knative-serving
  namespace: knative-serving
spec:
  ingress:
    kourier:
      enabled: true
  config:
    network:
      ingress.class: "kourier.ingress.networking.knative.dev"
EOF

kubectl --namespace knative-serving get service kourier

minikube tunnel
 
kubectl apply -f https://github.com/knative/serving/releases/download/v0.25.0/serving-default-domain.yaml

cat <<-EOF | kubectl apply -f -
apiVersion: v1
kind: Namespace
metadata:
  name: knative-eventing
---
apiVersion: operator.knative.dev/v1alpha1
kind: KnativeEventing
metadata:
  name: knative-eventing
  namespace: knative-eventing
EOF

kubectl get deployment -n knative-eventing
kubectl get KnativeEventing knative-eventing -n knative-eventing
kubectl get KnativeServing knative-serving -n knative-serving



MONGOOOO: helm install mongodb-release bitnami/mongodb --set architecture=standalone --set auth.enabled=false

sudo service mongod start


Robot-shop:
kubectl create ns robot-shop
cd robot-shop/K8s/helm
helm install robot-shop --namespace robot-shop .
and use minikube tunnel
