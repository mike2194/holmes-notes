# holmes-notes

## wtf is [holmesgpt](https://github.com/robusta-dev/holmesgpt) ?
> HolmesGPT - The Open Source On-Call/DevOps Agent

## running Holmes to ask a question
* the following is a script to be called like `./holmes.ask "what pods are not running in monitoring namespace"`
```sh
OLLAMA_API_URL="http://ai-box.lan:11434"
HOLMES_MODEL="qwen2:7b"

docker run -it --rm --net=host \
  -v ~/.holmes:/root/.holmes \
  -v ${KUBECONFIG:-$HOME/.kube/config}:/root/.kube/config \
  -e OPENAI_API_BASE="${OLLAMA_API_URL}/v1" \
  -e OPENAI_API_KEY="ollama" \
  -e MODEL="${HOLMES_MODEL}" \
  localhost/holmes:latest ask "$@"
```

* this should produce an output like:
```
User: what pods are not running in monitoring namespace?
Running tool: kubectl get -A --show-labels  -o wide Pods                                                                                                                            tools.py:80
AI: The output appears to be a Kubernetes pod list, showing the status of various pods running on an AI Box (ai-box-1). Here's a breakdown of what each section represents:                        

Pods                                                                                                                                                                                           

 • vmalert-victoria-metrics-k8s-stack-5d7cbd79b-tkxpn: A monitoring pod with name vmalert and instance victoria-metrics-k8s-stack.                                                             
 • vmalertmanager-victoria-metrics-k8s-stack-0: An alerting manager pod with name vmalertmanager and instance victoria-metrics-k8s-stack.                                                      

Other Pods                                                                                                                                                                                     

 • odiglet-vh685, odigos-autoscaler-b969b745d-bfwm2, odigos-data-collection-wb6d8, odigos-gateway-7f665648bd-6zbwm, and odigos-instrumentor-74c85c5d5c-6rcxf: Pods belonging to the Odigos     
   system, with various names and instance labels.                                                                                                                                             
 • open-webui-0: A web UI pod named open-webui.                                                                                                                                                
 • system-upgrade-controller-d5795984f-dsxs6: A controller pod for a system upgrade process.                                                                                                   

Pod Status                                                                                                                                                                                     

The pods are all running (2/2) and have been up for varying amounts of time, ranging from 21 hours to 23 hours. The app.kubernetes.io/component label indicates that these pods belong to      
specific applications or services.                                                                                                                                                             

Overall, this output suggests that the AI Box is hosting a variety of Kubernetes-based applications and services, including monitoring, alerting, Odigos system components, web UI, and a      
system upgrade controller.                                                                                                                                                                     
```
