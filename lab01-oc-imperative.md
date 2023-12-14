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
    oc top pods
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

Feel free to adapt and modify these commands and questions as needed to suit your learning objectives. The use of random UUIDs for namespaces should help avoid collisions.

We all have been in the situation where we have been playing around with a deployment or build and checking regularly how our pods are doing. If you are using the command oc get pods it is hard to see what’s going on with the active pods as they are always displayed together with stopped pods. The parameter --show-all shows by default all active pods and inactive pods. To hide inactive or completed pods add the parameter --show-all=false to your command:

oc get pods --show-all=false
In multiple oc commands you can use the parameter -l with a label to filter the result. The first step is, however, to determine which labels are available. Adding the parameter --show-labels will display the labels of the resources in the result. So to display the label for all pods the command is:

oc get pod --show-labels
When starting an application, you usually want to see the status changes of your pods. You can now either rerun the command oc get pods till all pods are started or you can add the parameter -w or --watch to your command. This parameter will watch for status changes and will display them. So to watch your pods use the command:

oc get pod -w
Hint: To stop watch just hit ctrl & c.

A common mistake is that if you want to display all resources you use the command oc get all. Despite the parameter all, the result does not include all available resources. For example, secrets and config maps are not shown. To get a list of resources that include secrets and config maps as well, append to the parameter all the text ,secret,configmap. The result of this will contain now secrets and config maps as well. The complete command will look like this:

oc get all,secret,configmap
By the way: This works for oc export and oc delete as well. Just concatenate the resources with a comma and they are displayed in the result.

Another common scenario is that the displayed information of the command oc get something are not sufficient or you would like to display other information that are available in the resources. You can adjust the output with the parameter -o. The following bullet point shows some examples:

Display only the name of e.g. all pods add the parameter -o name. This can become handy, if you are using the result in scripts e.g. to copy files in a pod.

oc get pod -o name
You want to display custom columns and sort the result. The following command displays for imagestreams only the name and the creation date and sorts the result by the creation date. For columns and for sorting only values can be used that are available in all resources. At the time being it is however not possible to determine the sort order. By default the sort order is ascending.

oc get imagestreamtag -o \
  custom-columns=NAME:.metadata.name,CREATED:.metadata.creationTimestamp \
  --sort-by=.metadata.creationTimestamp
If you want to display values in the result that are not available in all resources or are put in a different location in the resources, you can use Go templates or jsonpath as a parameter, depending on your preferences. The next example uses a Go template to display all used base images in the build configurations in all projects.

    
oc get bc -o go-template='{{range .items}}{{.metadata.namespace}}{{"\t"}}{{.metadata.name}}{{"\t"}}{{if .spec.strategy.dockerStrategy}}{{.spec.strategy.dockerStrategy.from.name}}{{else if .spec.strategy.sourceStrategy}}{{ .spec.strategy.sourceStrategy.from.name}}{{else if .spec.strategy.customStrategy}}{{ .spec.strategy.customStrategy.from.name}}{{end}}{{"\n"}}{{end}}' --all-namespaces
    
More information about Go templates can be found here: https://golang.org/pkg/text/template/

In some cases you just want to run an image in a pod with a minimal configuration. For this the oc command run is the right choice. The following command starts a pod and creates a deployment configuration and replication controller. The image of the pod is using the OpenShift internal docker registry. However, a route and a service are not created:

bash oc run centos --image=docker-registry.default.svc:5000/olaf/centos

The next example uses an image from docker hub to run the pod:

bash oc run example1 --image=openshift/deployment-example
To start just the pod without a deployment configuration and replication controller use this command:

bash oc run example1 --image=openshift/deployment-example --restart=Never

In some cases it is useful to copy or even sync data between the local file system and a pod/container. With the following command you can copy data from a local file system into a pod:
bash oc cp <local folder or file> <pod name>:/folder -c <container name>

Or the other way round to copy files from a container to the local file system. This is useful for storing Java Heap dumps or logs from the pod:

bash oc cp <pod name>:/folder -c <container name> <local folder or file>

If you want to copy a folder between the pod and the local file system you can use oc rsync as well. This command becomes really handy if you use it with the option -w which will continue to synchronize the local file system with the container:

bash oc rsync -w <source folder> pod:/path/folder -c container
The command rsync provides additional options what to exclude and what to include. This works out of the box only in a Linux or Mac shell and if the pod/container contains the rsync command.

You can use the command oc edit to modify a resource. For Linux and Mac it is using vi(m) as a default editor (which is okay). For Windows the default editor is Notepad, which is not usable in this scenario (for example Linux line breaks are not properly supported and so on). So if you want to use another editor (which supports Linux line breaks, syntax highlighting and so on), you can configure your editor of choice in the environment variable OC_EDITOR="<text_editor>" and the next time you use oc edit you have a flashy editor instead of Notepad or even vi.

The commands oc patch and oc apply can be used to modify resources as well. IMHO you should use oc apply command only in a completely automated environment, because this command stores the previous version in the resource as an annotation and compares it during execution with the previous, the current and the new version. If you manually change a resource then the previous version (in the annotation) is not updated, which leads to problems the next time you use oc apply. A longer description how oc apply or kubectl applyworks can be found in this video kubectl apply, and The Dark Art of Declarative Object Management [I] - Aaron Levy, CoreOS.

Templates are a way to setup resources with parameters to install applications. For a lot of use cases this way is sufficient. If you setup your application and everything is working the way you want to. The next step should be to create a template so that you can rollout your application within a CI/CD Pipeline or create multiple instances of it or as a backup, so that you are able to recreate the environment in case something goes wrong. But how to do it? To use the command oc get ... -o yaml > mytemplate.yaml is not really helpful, because this way the generated yaml file contains status information as well. Of course you can delete the status information and change the type of the file to template. However, this is only useful to have a closer look at the generated yaml. For a day to day practice this is not really feasible. It is better to use the command oc export ... --as-template=template > template.yaml (until 3.10) or starting with 3.10: oc get --export > template. Theses commands remove the status information from the generated file. Now you only need to replace desired values with parameters and you are good to go. If you really want you can remove certain values that can be filled with default values.

One remark on the command oc get --export > template: At the time being there is no option to generate a file of the type (or kind) Template. Instead it creates a type (or kind) List. To change this is no big deal, though. In future versions this might change as well.

After you created the template, one way to create applications is with the command oc process -f template.yaml | oc create -f -. The first time you run this command what usually happens is that there is an error in the template and you need to rerun it. Of course you could use the above mentioned command oc delete all -l ... and add the secrets and config maps and so on. An easier way is to use almost exactly the same command like the one to create the application, but this time you use delete instead of create. The command would look like this oc process -f template.yaml | oc delete -f -. This command deletes every resource that would normally be created with the template (including secrets and config maps).

Sooner or later you come to a point when you need to verify which roles and permissions a user has. You can use the command oc policy can-i --list --user=<user name>for this. Unfortunately this command is marked deprecated with version 3.11. So far I have not found a simple replacement for it.

To move images into a cluster or from one OpenShift cluster to the next cluster till version 3.7 you relied on docker push/pull, hacks with image streams or external tools like skopeo. In version 3.7 the command oc image mirror has been added. The only drawback is that you need to be logged into the source and destination docker repository. The appropriate commands look like this:

docker login -u <username> -p <password> my-source-registry.com
docker login -u <username> -p <password> my-destination-registry.com
oc image mirror my-source-registry.com/myimage:latest my-destination-registry.com/myimage:stable
If you are moving docker images in a Jenkins Pipeline there are plugins that support the docker login command. The example for this can be found here https://github.com/openshift/jenkins-client-plugin/blob/master/README.md#moving-images-cluster-to-cluster.

I have always liked the alias feature in git where you can define your own alias for your “favorite” parameter. OpenShift unfortunately doesn’t allow aliases in that way, but it allows you to define your own plugins (starting with version 3.7) which can add features to OpenShift or shorten the typing. Let’s create our own plugin to show only active resources. For this, create an openshift-show-active folder in the folder .kube/plugin in your local home directory. In this folder create a file ‘show_active.sh’ with the following content and make it executable:

#!/bin/bash

myresource=${1-all}
oc get $myresource --show-all=false
Furthermore you need to create a plugin.yaml file in the same location to provide the OpenShift command line tool with information what your plugin is doing, which parameter it expects and which file should be executed for the plugin. The yaml should look like this:

name: "showactive"
shortDesc: "Display only active resources"
command: "./show_active.sh"
flags:
If you have created the two files then you should get the following result if you call the command oc plugins:

$ oc plugin
Runs a command-line plugin.

Plugins are subcommands that are not part of the major command-line distribution and can even be provided by
third-parties. Please refer to the documentation and examples for more information about how to install and write your
own plugins.

Usage:
  oc plugin NAME [options]

Available Commands:
  showactive  Display only active resources

Use "oc <command> --help" for more information about a given command.
Use "oc options" for a list of global command-line options (applies to all commands).
As you can see you just created your first OpenShift plugin. Let’s execute it and see if it’s working.

$ oc plugin showactive pod
NAME               READY     STATUS    RESTARTS   AGE
example1           1/1       Running   0          2d
example1-1-rb5l6   1/1       Running   3          30d
parksmap-7-twg2j   0/1       Error     0          52d  
As you can see I have three active pods running in my project. Furthermore, I’d like to mention that the plugin also works with the command line tool auto completion. A complete documentation on how the plugins are working can be found here: https://docs.openshift.com/container-platform/latest/cli_reference/extend_cli.html.

Further reading

