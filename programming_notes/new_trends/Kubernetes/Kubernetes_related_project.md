
# k8s vertical scale

Some materials about in-place POD resource update:
- https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler  (Vertical POD Autoscaler, it depends on and waiting for the in-place update feature)
- https://github.com/kubernetes/kubernetes/issues/9043  (In-place rolling update feature request)
- https://github.com/kubernetes/community/pull/1719 
- https://groups.google.com/forum/#!msg/kubernetes-dev/LIkZoIqCT20/t515CV2mAgAJ 
- https://github.com/kubernetes/community/pull/2908 
- https://github.com/kubernetes/kubernetes/issues/5774

设置 Pod CPU 和内存限制 https://kubernetes.io/zh/docs/tasks/administer-cluster/cpu-memory-limit/

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# k8s + jenkins (+其他) 直接将github项目编译构建完成发布

- Gitkube: 使用git push构建Docker镜像并将其部署到Kubernetes https://www.ctolib.com/hasura-gitkube.html
- Gitkube-使用Git直接推送部署Kubernetes服务 https://my.oschina.net/u/2306127/blog/1647205
- GitHub+Docker Hub实现自动构建镜像 https://blog.csdn.net/bbwangj/article/details/82084480

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# k8s operator and CRD

Custom Resources https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/

- Extend the Kubernetes API with CustomResourceDefinitions https://kubernetes.io/docs/tasks/access-kubernetes-api/custom-resources/custom-resource-definitions/
- 使用CRD(CustomResourceDefinitions)扩展Kubernetes API https://k8smeetup.github.io/docs/tasks/access-kubernetes-api/extend-api-custom-resource-definitions/

- 【From aleiwu】 KubeCon 2019 上海 CRD 相关 Session 小记 https://aleiwu.com/post/kubecon-shanghai-2019/

## from Red Hat

Getting started with the Operator SDK https://docs.openshift.com/container-platform/4.3/operators/operator_sdk/osdk-getting-started.html

Getting started with Golang Operators by using Operator SDK https://developers.redhat.com/blog/2019/10/04/getting-started-with-golang-operators-by-using-operator-sdk/
- >
  ```console
  The following are possible return options to restart the Reconcile:
  
  With the error:
      return reconcile.Result{}, err
  
  Without an error:
      return reconcile.Result{Requeue: true}, nil
  
  Therefore, to stop the Reconcile, use:
      return reconcile.Result{}, nil
  ```
- > Note: For more details, check the `Reconcile` and its `Result` [implementations](https://godoc.org/sigs.k8s.io/controller-runtime/pkg/reconcile).

How to use third-party APIs in Operator SDK projects https://developers.redhat.com/blog/2020/02/04/how-to-use-third-party-apis-in-operator-sdk-projects/

Kubernetes Operators Best Practices https://www.openshift.com/blog/kubernetes-operators-best-practices

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## OLM (Operator Lifecycle Management) related

Analysis of Operator Lifecycle Manager in Openshift 4 https://rcarrata.com/openshift/operators-in-opc4/

OpenShift Operator Lifecycle Management Guide: Integrating Operators in OLM Part IV https://keithtenzer.com/2020/04/23/openshift-operator-lifecycle-management-guide-integrating-operators-in-olm-part-iv/

### CSV

11.4. 生成 CLUSTERSERVICEVERSION (CSV) https://access.redhat.com/documentation/zh-cn/openshift_container_platform/4.2/html/operators/osdk-generating-csvs

Creating the ClusterServiceVersion https://redhat-connect.gitbook.io/certified-operator-guide/ocp-deployment/operator-metadata/creating-the-csv

Building a Cluster Service Version (CSV) for the Operator Framework https://github.com/operator-framework/operator-lifecycle-manager/blob/53f6fa42cbbc82c35c490071c6413b84921709ef/doc/design/building-your-csv.md

How to contribute an Operator https://operatorhub.io/contribute

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## Operator Framework

Operators https://coreos.com/operators/
- OperatorHub.io https://operatorhub.io/
- Prometheus Operator 0.17.0 Documentation https://coreos.com/operators/prometheus/docs/latest/
- etcd Operator 0.9.1 Documentation https://coreos.com/operators/etcd/docs/latest/

Operator Framework - Google Groups https://groups.google.com/forum/#!forum/operator-framework

Operator Framework Special Interest Group https://commons.openshift.org/sig/OpenshiftOperators.html

Operators based on Helm charts https://docs.okd.io/latest/operators/osdk-helm.html

【[:white_check_mark:][`podset-operator`]】 Writing Your First Kubernetes Operator https://medium.com/faun/writing-your-first-kubernetes-operator-8f3df4453234
- etcd operator creates/configures/manages etcd clusters atop Kubernetes https://coreos.com/blog/introducing-the-etcd-operator.html || https://github.com/coreos/etcd-operator

Extending Kubernetes: Create Controllers for Core and Custom Resources https://medium.com/@trstringer/create-kubernetes-controllers-for-core-and-custom-resources-62fc35ad64a3
- > A Deep Dive Into Kubernetes Controllers https://engineering.bitnami.com/articles/a-deep-dive-into-kubernetes-controllers.html
- > Kubewatch, An Example Of Kubernetes Custom Controller https://engineering.bitnami.com/articles/kubewatch-an-example-of-kubernetes-custom-controller.html

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## k8s external service and CNAME

Kubernetes Access External Services https://medium.com/@ManagedKube/kubernetes-access-external-services-e4fd643e5097

Kubernetes best practices: mapping external services https://cloud.google.com/blog/products/gcp/kubernetes-best-practices-mapping-external-services

Integrating External Services https://docs.okd.io/latest/dev_guide/integrating_external_services.html 【这个是openshift的，不过还是记到这里吧】

Accessing External Services https://stackoverflow.com/questions/36000717/accessing-external-services

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## 可能有用的operator相关项目

**`For CRD of VMs in k8s`**:
- Vm in kubernetes https://stackoverflow.com/questions/33953592/vm-in-kubernetes
- KubeVirt: Kubernetes Virtualization API and runtime in order to define and manage virtual machines. https://kubevirt.io ||  https://github.com/kubevirt/kubevirt
  * Kubernetes and Virtualization: kubevirt will let you spawn virtual machine on your cluster! https://medium.com/@alezzandro/kubernetes-and-virtualization-kubevirt-will-let-you-spawn-virtual-machine-on-your-cluster-e809914cc783
  * Re-Imagining Virtualization with Kubernetes and KubeVirt – Part II https://blog.openshift.com/re-imagining-virtualization-with-kubernetes-and-kubevirt-part-ii/
- The virtual machine CRD definition for kubernetes. https://github.com/petrkotas/virt-vmconfig-crd
- Kubernetes CRI implementation for running VM workloads https://github.com/Mirantis/virtlet 【[Virtlet: run VMs as Kubernetes pods](https://www.mirantis.com/blog/virtlet-run-vms-as-kubernetes-pods/) —— The Mirantis Blog】
  * > "To try out Virtlet follow the instructions from [Setting up the environment](https://docs.virtlet.cloud/dev/setup/) and [try out examples](https://github.com/Mirantis/virtlet/blob/master/examples/README.md) documents."
  * > "You can watch sample usage session under this [link](https://asciinema.org/a/1a6xp5j4o22rnsx9wpvumd4kt)."
  * > "You can also give Virtlet a quick try using our demo script (requires Docker 1.12+):"
  
💂 Kubernetes External Secrets https://github.com/godaddy/kubernetes-external-secrets

Cross-cloud cost allocation models for workloads running on Kubernetes http://kubecost.com || https://github.com/kubecost/cost-model

----------------------------------------------------------------------------------------------------

A resource tracking a number of Operators out in the wild. https://github.com/operator-framework/awesome-operators

Kuberneters(K8s)CRD简明及简用 https://www.jianshu.com/p/cc7eea6dd1fb

----------------------------------------------------------------------------------------------------

- 如何从零开始编写一个Kubernetes CRD http://www.servicemesher.com/blog/kubernetes-crd-quick-start/
  * Extend the Kubernetes API with CustomResourceDefinitions https://kubernetes.io/docs/tasks/access-kubernetes-api/custom-resources/custom-resource-definitions/
  * CustomResourceDefinition https://kubernetes.feisky.xyz/cha-jian-kuo-zhan/api/customresourcedefinition
  * Kubebuilder - SDK for building Kubernetes APIs using CRDs https://github.com/kubernetes-sigs/kubebuilder || https://book.kubebuilder.io/  【:star:】
  * Repository for sample controller. Complements sample-apiserver https://github.com/kubernetes/sample-controller
- Operator https://jimmysong.io/kubernetes-handbook/develop/operator.html
  * 使用自定义资源扩展API https://jimmysong.io/kubernetes-handbook/concepts/custom-resource.html
    + Introducing Operators: Putting Operational Knowledge into Software https://coreos.com/blog/introducing-operators.html
  * OperatorHub.io https://operatorhub.io/  【:star:】
- Kubernetes CRD Operator 实现指南 - 高策的文章 - 知乎 https://zhuanlan.zhihu.com/p/38372448
  * [Discussion] Operators vs. controller pattern #300 https://github.com/kubeflow/tf-operator/issues/300
- 开发operator扩展kubernetes 调研整理 https://yucs.github.io/2017/12/21/2017-12-21-operator/
- 带你入门operator-framework http://dockone.io/article/5877
- 【kubernetes/k8s概念】CRD CustomResourceDefinition 自定义资源类型 https://blog.csdn.net/zhonglinzhang/article/details/86553744

Kubernetes Operator 快速入门教程（Kubernetes Operator 101） https://github.com/cnych/opdemo || https://www.qikqiak.com/post/k8s-operator-101/

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## operator源码相关

https://github.com/operator-framework/operator-sdk/blob/05a106abd9ff94bb2f0cc84b5054d0a603c9474f/doc/user-guide.md

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## 各种operator项目

### shell-operator

- Shell-operator：用于简化Kubernetes operator的创建 https://mp.weixin.qq.com/s/byHSc-moGK28_Z9hiNG7Aw
- Announcing shell-operator to simplify creating of Kubernetes operators https://medium.com/flant-com/kubernetes-shell-operator-76c596b42f23
  * > Shell-operator is a tool for running event-driven scripts in a Kubernetes cluster https://github.com/flant/shell-operator
  * > flant/shell-operator https://hub.docker.com/r/flant/shell-operator

### python operator

无需框架和SDK！使用Python来写一个Kubernetes Operator https://mp.weixin.qq.com/s/cMlm0HrwRt1n5EApd0JsTw
> 原文链接： https://medium.com/flant-com/kubernetes-operator-in-python-451f2d2e33f3

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# kubernetes插件

Kubernetes 1.12 新的插件机制 https://mritd.me/2018/11/30/kubectl-plugin-new-solution-on-kubernetes-1.12/

cert-manager -- Automatically provision and manage TLS certificates in Kubernetes https://jetstack.io || https://github.com/jetstack/cert-manager

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# kubernetes-sigs

## kubebuilder and controller-runtime

Kubebuilder - SDK for building Kubernetes APIs using CRDs https://github.com/kubernetes-sigs/kubebuilder || https://book.kubebuilder.io/

controller-runtime - Repo for the controller-runtime subproject of kubebuilder (sig-apimachinery) https://github.com/kubernetes-sigs/controller-runtime

【虽然是knative的doc的网页，但是主要是看使用kubebuilder的过程】 Defining a custom resource definition as the source https://knative.dev/v0.14-docs/eventing/samples/writing-a-source/02-define-source/

Building your own kubernetes CRDs https://itnext.io/building-your-own-kubernetes-crds-701de1c9a161

深入解析 Kubebuilder：让编写 CRD 变得更简单 https://developer.aliyun.com/article/719215

使用kubebuilder开发kubernetes CRD https://juejin.im/post/6844903898222690311
- > 注意你得先有个kubernetes集群，一步安装走你
  >> 一条命令部署 Kubernetes 高可用集群 👋 https://github.com/fanux/sealos

## kind

kubeadm-dind-cluster: A Kubernetes multi-node test cluster based on kubeadm https://github.com/kubernetes-sigs/kubeadm-dind-cluster
- DIND: Docker in Docker https://github.com/jpetazzo/dind

KIND: Kubernetes IN Docker - local clusters for testing Kubernetes https://kind.sigs.k8s.io/ || https://github.com/kubernetes-sigs/kind

使用 Kind 搭建你的本地 Kubernetes 集群 https://juejin.im/post/5c99ed6c6fb9a0710e47ebeb

使用 KinD 加速 CI/CD 流水线 https://www.qikqiak.com/post/accelerate-ci-cd-pipelines-with-kind/ || https://mp.weixin.qq.com/s/RLZSPLZx1TLbxoAM4MgQFw
- > 原文链接：https://medium.com/better-programming/accelerate-your-ci-cd-pipelines-with-kubernetes-in-docker-kind-109a67b39c82

## kubespray

Deploy a Production Ready Kubernetes Cluster https://github.com/kubernetes-sigs/kubespray

## kustomize

kustomize: Customization of kubernetes YAML configurations https://github.com/kubernetes-sigs/kustomize

使用 Kustomize 配置 Kubernetes 应用 https://www.qikqiak.com/post/kustomize-101/

Introduction to Kustomize, Part 1: Creating a Kubernetes app out of multiple pieces https://www.mirantis.com/blog/introduction-to-kustomize-part-1-creating-a-kubernetes-app-out-of-multiple-pieces/  <br>  Introduction to Kustomize, Part 2: Overriding values with overlays https://www.mirantis.com/blog/introduction-to-kustomize-part-2-overriding-values-with-overlays/

## 其他kubernetes-sigs项目

Kubernetes controller-tools: Tools to use with the controller-runtime libraries https://github.com/kubernetes-sigs/controller-tools

Consume services in Kubernetes using the Open Service Broker API https://github.com/kubernetes-sigs/service-catalog
- https://svc-cat.io/
- Service Catalog https://kubernetes.io/docs/concepts/extend-kubernetes/service-catalog/

KubeFed: Kubernetes Cluster Federation https://github.com/kubernetes-sigs/kubefed

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# kubernetes-retired

~~Heapster: [EOL] Compute Resource Usage Analysis and Monitoring of Container Clusters https://github.com/kubernetes-retired/heapster~~
> RETIRED: Heapster is now retired. See the deprecation timeline for more information on support. We will not be making changes to Heapster.

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# 多集群相关

## Cluster Registry

Cluster Registry https://kubernetes.github.io/cluster-registry/ || https://github.com/kubernetes/cluster-registry

User Guide https://kubernetes.github.io/cluster-registry/userguide.html

Managing Clusters with Cluster Registry https://medium.com/@cgrant/managing-clusters-with-cluster-registry-aefb1205fe47

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# 其他k8s相关项目

## KubeVirt

https://kubevirt.io/user-guide/

### CDI

Containerized Data Importer https://github.com/kubevirt/containerized-data-importer
- Data Volumes https://github.com/kubevirt/containerized-data-importer/blob/master/doc/datavolumes.md

Experiment with the Containerized Data Importer (CDI) https://kubevirt.io/labs/kubernetes/lab2.html

【From official blog】
- Containerized Data Importer https://kubevirt.io/2018/containerized-data-importer.html
- How to import VM into KubeVirt https://kubevirt.io/2019/How-To-Import-VM-into-Kubevirt.html
- KubeVirt VM Image Usage Patterns https://kubevirt.io/2020/KubeVirt-VM-Image-Usage-Patterns.html

Live Migration https://github.com/kubevirt/user-guide/blob/24929ed53e841aa6fc1b20a584b658d80b8e98c9/installation/live-migration.md

https://kubevirt.io/user-guide/#/installation/image-upload?id=create-a-virtualmachineinstance
- > To create a VirtualMachinInstance from a DataVolume, you can execute the following:

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# 其他k8s相关项目 (not matured)

A K8s-native Pipeline resource. https://tekton.dev || https://github.com/tektoncd/pipeline

kurun https://github.com/banzaicloud/kurun
- > Run `main.go` in Kubernetes with one command, also port-forward your app into Kubernetes

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## k8s开发环境（说是开发环境，其实实质还是dashboard，不过多了些类似开发功能）

云原生应用开发新体验：Kui https://moelove.info/2019/05/24/%E4%BA%91%E5%8E%9F%E7%94%9F%E5%BA%94%E7%94%A8%E5%BC%80%E5%8F%91%E6%96%B0%E4%BD%93%E9%AA%8CKui/
> IBM Kui: A hybrid command-line/UI development experience for cloud-native development https://github.com/IBM/kui

Lens - The Kubernetes IDE https://k8slens.dev/ || https://github.com/lensapp/lens
> Kontena Lens - The Smart Dashboard for Kubernetes https://www.youtube.com/watch?v=04v2ODsmtIs
>> notes：从youtube的介绍视频来看，貌似早期名字叫Kontena Lens？然后我是从这个视频下面的评论里有人提到了weavescope才去搜的。

Monitoring, visualisation & management for Docker & Kubernetes https://www.weave.works/oss/scope/ || https://github.com/weaveworks/scope

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## k8s可视化类项目

K8Studio - A CROSS-PLATFORM IDE TO MANAGE KUBERNETES CLUSTERS https://uxxu.io/

konstellate - Free and Open Source GUI to Visualize Kubernetes Applications. https://github.com/containership/konstellate

Kuboard简介 https://github.com/eip-work/kuboard-press || https://kuboard.cn/
- 搭建 NFS Server https://kuboard.cn/learning/k8s-intermediate/persistent/nfs.html

kubectl-tree https://github.com/ahmetb/kubectl-tree

Sloop - Kubernetes History Visualization https://github.com/salesforce/sloop

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

# projects based on or related to k8s (relatively matured)

## Helm (Google --> CNCF)

### Helm official

HELM: The package manager for Kubernetes https://helm.sh/

Helm Docs https://helm.sh/docs/
- Using Helm https://helm.sh/docs/using_helm/

The Kubernetes Package Manager https://github.com/helm/helm

### Helm 3

KubeCon 参会记录之 -- Helm 3 Deep Dive https://yq.aliyun.com/articles/670636
> 这个应该是 Helm3最令人期待的特性了。当Maintainer show 出这个页面的时候，现场响起来掌声。可见tiller是一个大家公认不应该存在的玩意。Maintainer很尴尬的也跟着象征性的鼓鼓掌。去掉Tiller后主要有以下几个变化。

Helm 3 Preview系列博文：
- Helm 3 Preview: Charting Our Future – Part 1: A History of Helm https://helm.sh/blog/helm-3-preview-pt1/
```
In order, I’ll discuss:

1.The history of the creation of Helm
2.A Gentle Farewell to Tiller
3.Chart Repositories
4.Release Management
5.Changes to Chart Dependencies
6.Library Charts
7.What’s Next?
```
- Helm 3 Preview: Charting Our Future – Part 3: Chart Repositories https://helm.sh/blog/helm-3-preview-pt3/
  * > Docker’s [Distribution project](https://github.com/docker/distribution) (also known as Docker Registry v2) is the successor to the Docker Registry project, and is the de-facto toolset to pack, ship, store, and deliver Docker images.
  * > But did you know that the Distribution project was designed to distribute any form of content, not just container images?
  * > Thanks to the efforts of the [Open Container Initiative (or OCI for short)](https://www.opencontainers.org/), Helm Charts can be hosted on any instance of Distribution.
- ……
- Helm 3 Preview: Charting Our Future – Part 7: What's Next? https://helm.sh/blog/helm-3-preview-pt7/

### Helm books

Helm User Guide - Helm 用户指南 https://whmzsu.github.io/helm-doc-zh-cn/
- Helm 插件指南 https://whmzsu.github.io/helm-doc-zh-cn/quickstart/plugins-zh_cn.html

### helm系列文章

- 初探云原生应用管理（一）: Helm 与 App Hub https://www.infoq.cn/article/HRMBW_jsMFqXVEx7vj7Z
  * > 通常来说，我们可以直接使用别人已经做好的 Helm Chart，就跟使用 Docker 镜像一样。所以，Helm 社区已经维护了一个官方 [Helm Hub](https://github.com/helm/charts)
  * > 我们首先要为你介绍一个叫做“开放云原生应用中心” (Cloud Native App Hub，简称 AppHub) 的服务，它的主页是：https://developer.aliyun.com/hub
  * > Helm v3 跟 Helm v2 的区别就像 Python 2 和 3 那么大，而且还比 Helm v2 要好用的多（比如：不需要安装服务端组件 Tiller）。我们下周的《为什么你必须尽快转向 Helm v3 》文章，会为你解释这个事情。
  * > 是的，你可以通过 https://github.com/cloudnativeapp/charts 来随时对这个 Helm Hub 中国小站点提出你的改进思路。
- 初探云原生应用管理（二）: 为什么你必须尽快转向 Helm v3 https://www.infoq.cn/article/JL6H7bgTy7X*1usthCP0

### Helm articles

Kubernetes Helm Tips and Tricks: Updating an App that uses ConfigMap https://rancher.com/blog/2018/2018-07-10-helm-tips-and-tricks-updating-app-with-configmap/

Using Kubernetes Helm to install applications: A quick and dirty guide https://www.mirantis.com/blog/install-kubernetes-apps-helm/

Simplify Kubernetes deployments with Helm (Part 3) – Creating configmaps and secrets https://www.nclouds.com/blog/simplify-kubernetes-deployments-helm-part-3-creating-configmaps-secrets/

是时候使用Helm了：Helm, Kubernetes的包管理工具 https://www.kubernetes.org.cn/3435.html

使用Helm管理kubernetes应用 https://jimmysong.io/kubernetes-handbook/practice/helm.html

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## k8s-conformance (CNCF)

🧪CNCF K8s Conformance Working Group https://cncf.io/ck || https://github.com/cncf/k8s-conformance
- > Sonobuoy is a diagnostic tool that makes it easier to understand the state of a Kubernetes cluster by running a set of Kubernetes conformance tests in an accessible and non-destructive manner. https://github.com/heptio/sonobuoy

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## minikube (k8s official)

minikube, Run Kubernetes locally https://github.com/kubernetes/minikube

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## microk8s (Ubuntu)

Microk8s: Kubernetes for workstations and appliances https://microk8s.io/

Microk8s: A kubernetes cluster in a snap https://github.com/ubuntu/microk8s

穷人也能用得起 K8s - VPS 单节点部署 Kubernetes 的方法与对比 https://avnpc.com/pages/kubernetes-for-single-vps
> 从易用角度来看，microk8s 是安装最简单，门槛最低的；minikube 适合对 minikube 比较熟悉的用户。
无论以何种方式安装 k8s， 都需要注意安全问题， 因为在 k8s 的设计中， Master 节点是不会暴露到外网的，用户服务都会安装到 Worker 节点，但是在单节点的情况下，k8s 所监听的端口都没有设防，容器的权限也有可能过大，这些安全问题在 minikube 的文档中也有提到， 需要对网络端口设置 iptables 限制可访问的 IP 等方式来提升安全性，如果是安全性敏感的项目，建议放弃单节点 k8s 的方案。

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## kops - Kubernetes Operations (k8s official)

Kubernetes Operations (kops) - Production Grade K8s Installation, Upgrades, and Management https://github.com/kubernetes/kops
- > Example Kops Demo on AWS https://asciinema.org/a/97298

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## kubeflow (Google)

Machine Learning Toolkit for Kubernetes https://github.com/kubeflow/kubeflow

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## k3s (Rancher Labs)

Lightweight Kubernetes. 5 less than k8s. https://k3s.io || https://github.com/rancher/k3s

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## kube-hunter (Aqua Security)

Kube-hunter - an open source tool for Kubernetes penetration testing https://blog.aquasec.com/kube-hunter-kubernetes-penetration-testing 
- > kube-hunter website https://kube-hunter.aquasec.com/
- > On Securing the Kubernetes Dashboard https://blog.heptio.com/on-securing-the-kubernetes-dashboard-16b09b1b7aca
- > 【kube-hunter github page】 Hunt for security weaknesses in Kubernetes clusters https://github.com/aquasecurity/kube-hunter

## kube-bench (Aqua Security)

Kube-Bench: An Open Source Tool for Running Kubernetes CIS Benchmark Tests https://blog.aquasec.com/announcing-kube-bench-an-open-source-tool-for-running-kubernetes-cis-benchmark-tests
- > CIS Benchmark for Kubernetes 1.6 https://blog.aquasec.com/cis-benchmark-for-kubernetes-security
- > CIS Benchmarks for Securing Kubernetes https://www.cisecurity.org/benchmark/kubernetes/
- > 【kube-bench github page】 The Kubernetes Bench for Security is a Go application that checks whether Kubernetes is deployed according to security best practices https://github.com/aquasecurity/kube-bench

## other materials from (Aqua Security)

Container Technology Wiki https://www.aquasec.com/wiki

Aqua Operator: Automating Security for Kubernetes https://blog.aquasec.com/aqua-security-kubernetes-operators

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## Kubewatch (Bitnami)

Kubewatch, An Example Of Kubernetes Custom Controller https://engineering.bitnami.com/articles/kubewatch-an-example-of-kubernetes-custom-controller.html

Watch k8s events and trigger Handlers https://github.com/bitnami-labs/kubewatch

## Kubeapps (Bitnami)

A web-based UI for deploying and managing applications in Kubernetes clusters https://github.com/kubeapps/kubeapps || https://kubeapps.com/

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:
