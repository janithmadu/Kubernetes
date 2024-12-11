
/////////////////////////////////////////////////////// Install Nginx Ingress /////////////////////////////////////////////////////////////

If your Deploy Nginx Ingress in Single node on Master you  need to run below comand

    *kubectl describe node <node-name> | grep Taints // Check your taints



    *If taint is node-role.kubernetes.io/control-plane run bellow command
        kubectl taint nodes --all node-role.kubernetes.io/control-plane-



    *If taint is node-role.kubernetes.io/master run bellow command
        kubectl taint nodes --all node-role.kubernetes.io/master-

        

    *Install Nginx-ingress using helm chart 
        helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
        helm repo update
        
        helm install nginx-ingress ingress-nginx/ingress-nginx \
        --namespace ingress-nginx \
        --create-namespace \
        --set controller.service.type=NodePort ( This will install nginx ingress using node port if you wat install it with Load Balance you need to install without node port)

        helm install nginx-ingress ingress-nginx/ingress-nginx \
        --namespace ingress-nginx \
        --create-namespace \
        --set controller.service.type=NodePort \
        --set controller.service.nodePorts.http=30080 \
        --set controller.service.nodePorts.https=30443 (Aloso you can specify node port as per your requirement)


        After Installation you can Run the deployments. 

    