
# openshift的各种版本

OKD: Renaming of OpenShift Origin with 3.10 Release https://blog.openshift.com/okd310release/
> 这个讲了openshift的开源版本改名叫okd的过程。

OpenShift https://en.wikipedia.org/wiki/OpenShift
> OpenShift维基页面讲了OpenShift几个版本的关系：
- "**`OpenShift Container Platform`** (formerly known as **`OpenShift Enterprise`**) is Red Hat's on-premises private platform as a service product, built around a core of application containers powered by Docker, with orchestration and management provided by Kubernetes, on a foundation of Red Hat Enterprise Linux."
- "**`OpenShift Origin`**, also known since August 2018 as **`OKD`** (Origin Community Distribution) is the upstream community project used in OpenShift Online, OpenShift Dedicated, and OpenShift Container Platform."
- "**`Red Hat OpenShift Online (RHOO)`** is Red Hat's public cloud application development and hosting service which runs on AWS."
- "**`OpenShift Dedicated`** is Red Hat's managed private cluster offering, built around a core of application containers powered by Docker, with orchestration and management provided by Kubernetes, on a foundation of Red Hat Enterprise Linux. It is available on the Amazon Web Services (AWS) and Google Cloud Platform (GCP) since December 2016 marketplaces."
- "**`OpenShift.io`** is Red Hat's SaaS service that provides an application development environment."

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# openshift vs kubernetes

【[:star:][`*`]】 10 most important differences between OpenShift and Kubernetes https://cloudowski.com/articles/10-differences-between-openshift-and-kubernetes/

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# openshift official

OPENSHIFT Online https://manage.openshift.com/

OpenShift Documentation https://docs.openshift.com/
- Upgrading Clusters
  * Upgrade Methods and Strategies https://docs.openshift.com/container-platform/3.9/upgrading/index.html
- Understanding the Operator Lifecycle Manager https://docs.openshift.com/container-platform/4.1/applications/operators/olm-understanding-olm.html
- ~~Installing from the OperatorHub using the CLI https://docs.openshift.com/container-platform/4.1/applications/operators/olm-adding-operators-to-cluster.html#olm-installing-operator-from-operatorhub-using-cli_olm-adding-operators-to-a-cluster~~  -->  https://docs.openshift.com/container-platform/4.4/operators/olm-adding-operators-to-cluster.html#olm-installing-operator-from-operatorhub-using-cli_olm-adding-operators-to-a-cluster
  >>//notes：4.1版本的已经过时，表现在这部分开头这句：`"Use the oc command to create or update a CatalogSourceConfig object, then add a Subscription object."` --> 目前从`4.4.x`、`4.5.0`版本看，不再需要手动创建`CatalogSourceConfig`类型的对象了（`oc api-resources`看了下，这个对象类型倒是还在）。
  >>> INSTALL KUBERNETES OPERATORS IN OPENSHIFT USING ONLY THE CLI https://www.itix.fr/blog/install-operator-openshift-cli/

OpenShift Installation and Configuration Management https://install.openshift.com || https://github.com/openshift/openshift-ansible

Software Collections https://github.com/sclorg
> Software Collections https://www.softwarecollections.org/

## okd official

~~OKD: The Origin Community Distribution of Kubernetes https://github.com/openshift/origin~~  -->  OKD: The Origin Community Distribution of Kubernetes https://github.com/openshift/okd
>> //notes：【origin这个仓库只有到3.11的了，新的4.x系列的OCP开源版都到这个叫okd的仓库了，但是原来那个仓库并没有删，只是作为3.x版本的开源版仓库。想下老版本的`oc`还得去这个仓库的release页面。】
- https://github.com/openshift/origin/releases/tag/v3.11.0
- https://github.com/openshift/okd/releases/tag/4.5.0-0.okd-2020-07-14-153706-ga

okd -- The Origin Community Distribution of Kubernetes that powers Red Hat OpenShift. https://www.okd.io/

okd Documentation https://docs.okd.io/
- Planning your installation https://docs.okd.io/latest/install/index.html
- REST API Reference https://docs.okd.io/latest/rest_api/index.html

## openshift blog

- Deploying your storage backend using OpenShift Container Storage 4 https://www.openshift.com/blog/deploying-your-storage-backend-using-openshift-container-storage-4
- Rook.io Container Native Storage on OpenShift https://www.openshift.com/blog/rook-container-native-storage-openshift
- OpenShift 4.3: Managing Catalog Sources in the OpenShift Web Console https://www.openshift.com/blog/openshift-4-3-managing-catalog-sources-in-the-openshift-web-console

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

##

Django Example: This is a Django project that you can use as the starting point to develop your own and deploy it on an OpenShift cluster. https://github.com/sclorg/django-ex/tree/master

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# openshift general

谁最良心？选我选我！【:star:业界良心！+3 :star::star::star:】
- Foundations of OpenShift -- By OpenShift https://www.katacoda.com/openshift/courses/introduction
- OpenShift Playgrounds -- By OpenShift https://www.katacoda.com/openshift/courses/playgrounds

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# openshift安装

Install an OpenShift cluster https://github.com/openshift/installer

Simple all-in-one localhost Installation fails with "Failed to start Atomic OpenShift Master API." #7379 https://github.com/openshift/openshift-ansible/issues/7379

离线生产级部署openshift https://github.com/xiaoping378/openshift-deploy

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# openshift系列笔记

https://blog.csdn.net/huqigang/article/category/7157977
- openshift/origin学习记录（0）——Ansible安装多节点openshift集群 https://blog.csdn.net/huqigang/article/details/77962156
- openshift/origin学习记录（12）——离线安装集群 https://blog.csdn.net/huqigang/article/details/78318266

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# openshift技巧

## 从命令行获取webconsole地址

https://www.ibm.com/support/knowledgecenter/SSFC4F_1.2.0/install/prep.html
```sh
The OpenShift Container Platform web console can be found by running the `kubectl -n openshift-console get route` 
command. You can see a similar output to the following example:

  openshift-console          console             console-openshift-console.apps.new-coral.purple-chesterfield.com                       console                  https   reencrypt/Redirect     None

The console URL in this example is https://console-openshift-console.apps.new-coral.purple-chesterfield.com. Open the URL 
in your browser and check the result. If the console URl is like console-openshift-console.router.default.svc.cluster.local, 
set openshift_master_default_subdomain when you install the OpenShift Container Platform.
```
```sh
# 个人实战：第一个确实就是openshift的webconsole地址

[root@anaemia-inf ~]# oc get route -n openshift-console
NAME        HOST/PORT                                                  PATH   SERVICES    PORT    TERMINATION          WILDCARD
console     console-openshift-console.apps.anaemia.os.fyre.ibm.com            console     https   reencrypt/Redirect   None
downloads   downloads-openshift-console.apps.anaemia.os.fyre.ibm.com          downloads   http    edge/Redirect        None
```

## system:admin VS kube:admin (kubeadmin)

```sh
# 至少最新的OCP 4.3（ocp 3.11是啥情况不记得了）装完，不用任何用户登陆，执行oc whoami会发现是一个叫system:admin的用户。
[root@anaemia-inf ~]# oc whoami
system:admin

# 然后提示的证书里会有一个叫kubeadmin的用户。后面这个一直还会用到，system:admin就基本不会用了。
Credentials:
    Username: kubeadmin
    Password: xxxxx-xxxxx-xxxxx-xxxxx
    
# 这俩用户啥关系呢？谷歌了一下，有本书（[《Architecting and Operating OpenShift Clusters》](https://link.springer.com/book/10.1007/978-1-4842-4985-7)）里提到了这么一段：
Once the cluster is successfully deployed, the installer displays the credentials for the kubeadmin user(see Listing 6-10). This is a 
cluster-admin user equivalent to the system admin user in the OCP3 11 x clusters, but the kubeadmin user can log in to the web console.
In OCP4, this is the user that configures and sets up the environment to enable other services or functionalities. 
To enable other users to access the new OCP cluster, the kubeadmin user must define a new identity provider.

# 但是我这边安完OCP 4.3初始的用户确实是system:admin，算了，不管了。反正最大的区别是system:admin不能登陆web console。但是这个用户肯定还是
# 存在的。参见： https://docs.openshift.com/container-platform/4.3/authentication/impersonating-system-admin.html
```

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# openshift组件

## DeploymentConfig

Deployments https://docs.okd.io/3.11/architecture/core_concepts/deployments.html

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# openshift security

Authentication https://docs.openshift.com/container-platform/3.11/architecture/additional_concepts/authentication.html

A reverse proxy that provides authentication with OpenShift via OAuth and Kubernetes service accounts https://github.com/openshift/oauth-proxy

OpenShift - Security https://www.tutorialspoint.com/openshift/openshift_security.htm

openshift 学习笔记-6 secret and quota https://blog.csdn.net/warrior_0319/article/details/78273717

解析 | OpenShift源码简析之oauth流程(上） http://www.10tiao.com/html/187/201809/2652137245/1.html

理解OpenShift（4）：用户及权限管理 https://www.cnblogs.com/sammyliu/p/10083659.html
  - Service Accounts https://docs.openshift.com/container-platform/3.11/dev_guide/service_accounts.html

:u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307::u6307:

## openshift安全与用户管理问题

利用Ansible的PlayBook自动化构建OpenShift Origin集群 https://christchen.me/archives/649.html
> `openshift_master_identity_providers=[{‘name’:’htpasswd_auth’,’login’:’true’,’challenge’:’true’,’kind’:’HTPasswdPasswordIdentityProvider’,’filename’:’/etc/origin/master/htpasswd’}]`
>> `openshift_master_identity_providers=[{'name':'htpasswd_auth','login':'true','challenge':'true','kind':'HTPasswdPasswordIdentityProvider','filename':'/etc/origin/master/htpasswd'}]`
>>> 上面机智地跳过中文引号的坑，然而还是掉进了已废弃参数的坑。。。报错如下：
```
Failure summary:

  1. Hosts:    openshift-single-node.sl.cloud9.ibm.com
     Play:     Verify Requirements
     Task:     Run variable sanity checks
     Message:  last_checked_host: openshift-single-node.sl.cloud9.ibm.com, last_checked_var: openshift_master_identity_providers;openshift_master_identity_providers contains a provider of kind==HTPasswdPasswordIdentityProvider and filename is set.  Please migrate your htpasswd files to /etc/origin/master/htpasswd and update your existing master configs, and remove the filename keybefore proceeding.
```
>>>> 后来网上查到这个帖子【[Ansible 部署 OKD 集群（v3.11）](https://www.jianshu.com/p/792899a49c8f)】，去掉了最后一个`filename`键值对才算好。

Bug 1565447 - installation fail due to HTPasswdPassword file is not mounted into master static pod https://bugzilla.redhat.com/show_bug.cgi?id=1565447

07-用户认证与授权 https://blog.csdn.net/weixin_33919941/article/details/87592779
- > 这些后端的用户信息管理系统在OpenShift中称为Identify Provider。通过配置，OpenShift可以连接到企业常用的用户信息管理系统。如LDAP系统、微软活动目录（Active Directory）等。同时也支持AllowALL、DenyAll、HTPasswd文件，GitHub、Google等众多后端。
查看master-config.ymal配置，可以看到当前实例集群使用的Provider的类型及配置。

### 安全与用户管理相关官方内容

Configuring Your Inventory File https://docs.okd.io/3.10/install/configuring_inventory_file.html
- Example Inventory Files https://docs.okd.io/3.10/install/example_inventories.html

Configuring authentication and user agent https://docs.openshift.com/container-platform/3.11/install_config/configuring_authentication.html
> https://github.com/openshift/openshift-docs/blob/master/install_config/configuring_authentication.adoc

Master and Node Configuration https://docs.openshift.com/container-platform/3.11/install_config/master_node_configuration.html

## openshift scc

**起因：在一个openshift 3.11单节点环境，发现nginx的容器起不来，进去看了下，报错如下**：
```
root@myopenshift:nginx-operator$ oc logs example-nginx-4gneicr7ynbwus1404tld50zo-57ff5fc959-844vr
2019/06/30 12:42:43 [warn] 1#1: the "user" directive makes sense only if the master process runs with super-user privileges, ignored in /etc/nginx/nginx.conf:2
nginx: [warn] the "user" directive makes sense only if the master process runs with super-user privileges, ignored in /etc/nginx/nginx.conf:2
2019/06/30 12:42:43 [emerg] 1#1: mkdir() "/var/cache/nginx/client_temp" failed (13: Permission denied)
nginx: [emerg] mkdir() "/var/cache/nginx/client_temp" failed (13: Permission denied)
```
**后来发现是openshift多事，自己搞了一套 SCC(Security Context Constraints) 导致的。下面甚至有issue说在openshift里不要用nginx做例子。。。**

Don't use nginx image for the Pod example https://github.com/openshift/openshift-docs/issues/1533

Volume mounted under /var/cache & permission denied https://github.com/minishift/minishift/issues/105

openshift跑app权限报错解决 https://blog.csdn.net/iiiiher/article/details/70170973
> Understanding Service Accounts and SCCs https://blog.openshift.com/understanding-service-accounts-sccs/

non-ROOT containers to show OpenShift some love https://medium.com/bitnami-perspectives/non-root-containers-to-show-openshift-some-love-3b32d7218ac6

:u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272::u5272:

# openshift其他

How To: Stop and start a production OpenShift Cluster https://eti.io/how-to-stop-and-start-a-production-openshift-cluster/
