These are the steps I came up to get the plan-net app to run:

# Already in image
 apt install -y postgresql
 apt install -y vim

# Start postgres
pg_ctlcluster 11 main start 

# Set postgres password
passwd postgres
 
su - postgres
psql
\password
# Set password to: passw0rd

bundle exec rails db:setup
bundle exec rails server -b 0.0.0.0

The operations here were turned into a K8S manifest, such that the only thing needed now is to run:

# Deploy plan-net
kubectl apply -f plan-net.yaml
# Log into the pod:
kubectl exec plan-net-6b8586d7b8-q6xhj --tty -i -- bash

