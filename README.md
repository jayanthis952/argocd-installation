# argocd-installation
document to install argocd

1.Install Argo CD
   kubectl create namespace argocd
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

2.Access The Argo CD API Server
   kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
   kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'

3. Install Argo CD cli
      curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
      sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
      rm argocd-linux-amd64

4.Login to argocd with user - "admin"
  To hey password:
     argocd admin initial-password -n argocd
          Vj4b0-tF2or54ZGF  -> Paste Password

5.Register A Cluster To Deploy Apps To (Optional)
    a. Login to Argocd from CLI->  argocd login 13.201.81.76:30271 {Public IPv4 address}              
          admin & Passwrd (Vj4b0-tF2or54ZGF)
    b. Add kube-config to argocd cluster
          - Get the kube-context to add to argocd
              kubectl config get-contexts -o name
          - Add context to Argocd 
              argocd cluster add <context_name>
