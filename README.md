# holmes-notes

## running Holmes to ask a question
* the following is a script to be called like `./holmes.ask "what pods are not running in monitoring namespace"`
```sh
OLLAMA_API_URL="http://ai-box.lan:11434"
KUBECONFIG=${KUBECONFIG:-$HOME/.kube/config}

HOLMES_MODEL="qwen2:7b"

docker run -it --rm --net=host \
  -v ~/.holmes:/root/.holmes \
  -v ${KUBECONIFG}:/root/.kube/config \
  -e OPENAI_API_BASE="${OLLAMA_API_URL}/v1" \
  -e OPENAI_API_KEY="ollama" \
  -e MODEL="${HOLMES_MODEL}" \
  localhost/holmes:latest ask "$@"
```
