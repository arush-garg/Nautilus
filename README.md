## Cheat Sheet of commands with kubectl

1. Seeing what is currently in the namespace

`kubectl get nodes`
Replace `nodes` with `pods`, `deployments` or `services` depending on the category you want

2. Launch a pod (.yaml file)

`kubectl create -f <filename>`

You can run `kubectl get pods` after a few seconds and see your pod. The name of the pod is defined by metadata > name in your file. Note that two pods cannot have the same filename

To get more information about it: `kubectl describe pod <pod_name>`

3. Monitoring the pods

To get the logs: `kubectl logs <pod_name>`

4. Logging onto the pods
You can run bash commands in the pod. First, access the pod's CLI using: `kubectl exec -it <pod_name> -- /bin/bash`
Exit using control-D

5. Deleting pods

`kubectl delete <pod_name>` or `kubectl delete -f <filename>`
Verify the pod has been deleted by running `kubectl get pods`

## Other Information

Pods are standalone - They can run commands but everything is deleted once they are deleted or restarted.

Deployments create pods with memory - They have some folders (bin, home, media, etc.) which persist across pods, even if one pod is deleted.

## Jupyter notebooks

1. Create a pod - `kubectl create -f <filename>`
2. Login into the pod - `kubectl exec -it <pod_name> -- bash`
3. In the pod terminal - `jupyter notebook --ip='0.0.0.0'`

Now, do not close this terminal window or terminate it. Open a new terminal for the following steps

1. `kubectl port-forward <pod_name> 8888:8888`
2. Open `localhost:8888` in a browser
3. Go to the original terminal window and find the token
It will be something like: `http://jupyter-pod-example:8888/tree?token=2cfe15e404c0ab9a0437f1a3ffbed0b4ce451b765aa36ff1` and you need everying after `token=`

Then, you can either create a new notebook or upload existing files

To finish off, exit the pod terminal using the command `exit`