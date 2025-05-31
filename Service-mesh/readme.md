### **Prerequisites**
- **Ubuntu system**: 20.04/22.04 LTS or similar.
- **Kubernetes cluster**: Running locally (e.g., Minikube) or on a cloud provider. Install Minikube if needed:
  ```bash
  curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
  sudo install minikube-linux-amd64 /usr/local/bin/minikube
  minikube start --driver=docker
  ```
- **kubectl**: Kubernetes CLI installed:
  ```bash
  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
  sudo install kubectl /usr/local/bin/kubectl
  kubectl version --client
  ```
- **Docker**: Already installed (from your previous query).
- **System resources**: At least 4 CPU cores, 8 GB RAM for Minikube + Istio (more for production).

### **Steps to Install Istio Service Mesh on Ubuntu**

1. **Download Istio**:
   - Download the latest Istio release (e.g., 1.25.0 as of May 2025):
     ```bash
     curl -L https://istio.io/downloadIstio | sh -
     ```
   - Move to the Istio directory (e.g., `istio-1.25.0`):
     ```bash
     cd istio-*
     ```
   - Add `istioctl` to your PATH:
     ```bash
     export PATH=$PWD/bin:$PATH
     sudo cp bin/istioctl /usr/local/bin/
     ```

2. **Install Istio on Kubernetes**:
   - Use the `demo` profile for testing (balanced resource usage):
     ```bash
     istioctl install --set profile=demo -y
     ```
   - This installs the Istio control plane (`istiod`) and components in the `istio-system` namespace.

3. **Verify Istio installation**:
   - Check that Istio pods are running:
     ```bash
     kubectl get pods -n istio-system
     ```
     Look for `istiod`, `istio-ingressgateway`, etc., with `Running` status.
   - Verify Istio version:
     ```bash
     istioctl version
     ```

4. **Enable automatic sidecar injection**:
   - Label the namespace where your applications will run (e.g., `default`):
     ```bash
     kubectl label namespace default istio-injection=enabled
     ```

5. **(Optional) Install Istio add-ons** (e.g., Kiali, Jaeger, Prometheus for observability):
   - Apply add-on manifests from the Istio directory:
     ```bash
     kubectl apply -f samples/addons/kiali.yaml
     kubectl apply -f samples/addons/jaeger.yaml
     kubectl apply -f samples/addons/prometheus.yaml
     ```
   - Access Kiali dashboard:
     ```bash
     istioctl dashboard kiali
     ```

6. **Deploy a test application**:
   - Deploy the BookInfo sample application to test the service mesh:
     ```bash
     kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
     ```
   - Verify services:
     ```bash
     kubectl get services
     ```
   - Access the application via the Istio ingress gateway:
     ```bash
     export INGRESS_HOST=$(minikube ip)
     export INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].nodePort}')
     curl http://$INGRESS_HOST:$INGRESS_PORT/productpage
     ```

7. **(Optional) Configure for production**:
   - Use the `default` profile for production:
     ```bash
     istioctl install --set profile=default -y
     ```
   - Enable mTLS for secure communication:
     ```bash
     kubectl apply -f - <<EOF
     apiVersion: security.istio.io/v1beta1
     kind: PeerAuthentication
     metadata:
       name: default
       namespace: istio-system
     spec:
       mtls:
         mode: STRICT
     EOF
     ```
