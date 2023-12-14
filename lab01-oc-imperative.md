# OpenShift Lab

In this lab, we will explore the `oc` command-line tool in OpenShift.

## Prerequisites

Before starting the lab, ensure that you have:

- Access to an OpenShift cluster.
- `oc` command-line tool installed and configured with appropriate permissions.

## Lab Instructions

1. **Login to the OpenShift Cluster**

    ```bash
    oc login -u <your-username> -p <your-password>.  <cluster api>
    ```

2. **Create a New Project with a Random UUID as the Name**

    ```bash
    PROJECT_NAME="project-${RANDOM}"
    oc new-project $PROJECT_NAME
    ```

3. **Find Information About the User**

    ```bash
    oc whoami
    ```

4. **View Your Configuration**

    ```bash
    oc config view
    ```

5. **Update the Current Context**

    ```bash
    oc config set-context $PROJECT_NAME
    ```

6. **Get Help**

    ```bash
    oc --help
    ```

7. **Apply Help Command to Submenus**

    ```bash
    oc get --help
    oc describe --help
    oc policy --help
    ```

8. **Find Properties of Specific Objects**

    ```bash
    oc explain <resource-name>
    oc explain deployment
    ```

9. **Find Information About Specific Properties**

    ```bash
    oc explain deployment.spec
    oc explain deployment.spec.template.spec.containers.ports
    oc explain pod.spec.containers.ports
    ```

10. **Create a New App from a Remote Git Repository**

    ```bash
    oc new-app https://github.com/sclorg/cakephp-ex --name php
    ```

11. **List All Projects**

    ```bash
    oc projects
    ```

12. **Create and Switch to Another Project with a Random UUID as the Name**

    ```bash
    ANOTHER_PROJECT_NAME="project-${RANDOM}"
    oc new-project $ANOTHER_PROJECT_NAME
    oc project $ANOTHER_PROJECT_NAME
    ```

13. **Show High-Level Overview of the Current Project**

    ```bash
    oc status
    ```

14. **Deploy a New App**

    ```bash
    oc new-app openshiftkatacoda/blog-django-py --name blog-from-image
    ```

15. **Verify the Status of the App**

    ```bash
    oc status
    ```

16. **List All Pods**

    ```bash
    oc get pods
    ```

17. **Exec Into the Blog from Image Pod**

    ```bash
    oc exec -it blog-from-image-<pod-id> -- ls -alh Dockerfile
    ```

18. **Start a Debug Pod and Attach It**

    ```bash
    oc debug deployment/blog-from-image
    ```

19. **Modify a File in the Debug Pod**

    ```bash
    oc rsh debug/blog-from-image-<pod-id>
    ```

20. **Exec Back Into the Original Pod**

    ```bash
    oc rsh blog-from-image-<original-pod-id>
    ```

21. **Check All Services**

    ```bash
    oc get svc --all-namespaces
    ```

22. **Find the Service for the Blog from Image**

    ```bash
    oc get svc blog-from-image
    ```

23. **Extract Ports and IP for the Service**

    ```bash
    oc get svc blog-from-image -o jsonpath='{.spec.ports[*].port}, {.spec.clusterIP}'
    ```

24. **Verify Connectivity**

    Check connectivity to the service IP.

25. **Create a Temporary Pod**

    ```bash
    oc run temp-pod --image=<image-name> --command -- sleep infinity
    ```

26. **Exec Into the Temporary Pod**

    ```bash
    oc exec -it temp-pod -- /bin/bash
    ```

27. **Use RSH Subcommand to Get a Shell Inside a Running Pod**

    ```bash
    oc rsh <pod-name>
    ```

28. **Expose the Service to Create a Route**

    ```bash
    oc expose svc/blog-from-image
    ```

29. **Find the Hostname of the Route**

    ```bash
    oc get route/blog-from-image -o jsonpath='{.spec.host}'
    ```

30. **Access the Application from Your Browser**

    Open a web browser and enter the URL: `http://<hostname-of-the-route>`

31. **Copy All Files From the Pod Using Rsync**

    ```bash
    oc rsync blog-from-image-<pod-id>:/ /your/temp/directory
    ```

32. **Delete the Pod and Check Status**

    ```bash
    oc delete pod <pod-name>
    oc get pods
    ```

33. **Cleanup All Objects in the Namespace**

    ```bash
    oc delete all --all
    ```

34. **Scale Deployments**

    - Scale up a deployment:
    
    ```bash
    oc scale deployment/<deployment-name> --replicas=<desired-replica-count>
    ```

    - Scale down a deployment:

    ```bash
    oc scale deployment/<deployment-name> --replicas=<desired-replica-count>
    ```

35. **Check Logs of a Pod**

    ```bash
    oc logs <pod-name>
    ```

36. **Check Resource Usage of Pods**

    ```bash
    oc adm top pods
    ```
   or 
    ```bash
    kubectl top pods
    ```

37. **Create and Delete ConfigMaps**

    ```bash
    oc create configmap my-config --from-literal=key1=value1
    oc delete configmap my-config
    ```

38. **Create and Delete Secrets**

    ```bash
    oc create secret generic my-secret --from-literal=username=myuser --from-literal=password=mypassword
    oc delete secret my-secret
    ```

39. **Check Events in a Namespace**

    ```bash
    oc get events
    ```

40. **Check Cluster-Wide Resource Quotas**

    ```bash
    oc get clusterresourcequotas
    ```
