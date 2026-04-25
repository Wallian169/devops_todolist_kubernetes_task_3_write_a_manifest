# INSTRUCTION.md

## How to Apply All Manifests

To apply all manifests in your project, follow these steps:

1. **List and Apply Manifests**:
   First, create a namespace before other pods:
   ```sh
   kubectl apply -f .infrastructure/namespace.yml && kubectl apply -f .infrastructure/
   ```

2. **Check for Errors**:
   Review the output for any errors and make necessary adjustments.

3. **Verify Manifest Application**:
   Ensure that all manifests are applied correctly by checking logs or running specific commands to verify.
    ```sh
    kubectl get pods -n todoapp
    ```

## How to Test the ToDo Application Using Port-Forward

To test the ToDo application using the `port-forward` command, follow these steps:



1. **Start the ToDo Application**:
   Ensure that your ToDo application is running.

2. **Apply Port-Forward**:
   Use the `kubectl port-forward` command to forward traffic from your local machine to the ToDo application pod. Assuming your ToDo application is running in a pod named `todoapp`, and it exposes port 8000, you can use:
   ```sh
   kubectl port-forward pod/todoapp 8001:8000 -n todoapp
   ```

3. **Access the ToDo Application**:
   Open your web browser and navigate to `http://localhost:8001`. You should now be able to access and test the ToDo application.

5. **Check for Errors**:
   Ensure that there are no errors in the output from the `port-forward` command. If you encounter any issues, review them and make necessary adjustments.

6. **Verify Functionality**:
   Test various features of the ToDo application to ensure they work as expected.

## How to Test the ToDo Application Using busybox:curl

1. **Get internal IP Address for app pod**:
   Use the `kubectl get pods -n todoapp -o wide` command to find the internal IP address of your ToDo application pod. For example:
   ```bash
   kubectl get pods -n todoapp -o wide
   ```
   and find IP that belongs to todoapp pod.

2. **Enter interactive mode of busybox pod**
    ```bash
    kubectl exec -it busybox -n todoapp -- sh
    ```

3. **Test the ToDo Application**:
    Once you are in the interactive shell, you can test various features of the ToDo application by running curl commands to access the API, for example: 
   ```bash
   curl http://<internal-api-from-step-1>:8000/api/
   ```

**Stop all pods**
```bash
kubectl delete -f .infrastructure
```