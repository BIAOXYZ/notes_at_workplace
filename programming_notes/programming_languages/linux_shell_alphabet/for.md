
Linux下Shell的for循环语句 https://www.cnblogs.com/EasonJim/p/8315939.html

```sh
[root@lolls-inf ~]# for ((i=1;i<=5;i++)); do echo $i; done
1
2
3
4
5
[root@lolls-inf ~]#
[root@lolls-inf ~]# for ((i=1;i<=5;i++)); do echo $(expr $i \* 3 + 1); done
4
7
10
13
16
[root@lolls-inf ~]#
[root@lolls-inf ~]# for i in $(seq 1 5); do echo $(expr $i \* 3 + 1); done
4
7
10
13
16
[root@lolls-inf ~]#
[root@lolls-inf ~]# for i in {1..5}; do echo $(expr $i \* 3 + 1); done
4
7
10
13
16
[root@lolls-inf ~]#
[root@lolls-inf ~]# awk 'BEGIN{for(i=1; i<=5; i++) print i}'
1
2
3
4
5
[root@lolls-inf ~]#
```
```sh
[root@lolls-inf hybridapp-operator]# for i in {1..25}; do echo -e "TEST $i \n"; make test; done
TEST 1

go fmt ./cmd/... ./pkg/...
go vet ./cmd/... ./pkg/...
Version: version.Version{KubeBuilderVersion:"2.0.0-beta.0", KubernetesVendor:"1.14.1", GitCommit:"b12371ccabd1bc8de7ec7ec1a1ca7bfabe567701", BuildDate:"2019-07-19T19:02:15Z", GoOs:"unknown", GoArch:"unknown"}
go test `go list ./cmd/... ./pkg/... ` -coverprofile=cover.out
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/cmd/manager   [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis      [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis/app  [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis/app/v1alpha1 [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller        [no test files]
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmchannel     10.921s coverage: 90.7% of statements
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmdeployable  [no test files]
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmplacementrule       14.800s coverage: 94.1% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhchannel      11.004s coverage: 88.8% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhdeployable   16.752s coverage: 82.4% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhplacementrule        12.777s coverage: 94.1% of statements
TEST 2

go fmt ./cmd/... ./pkg/...
go vet ./cmd/... ./pkg/...
Version: version.Version{KubeBuilderVersion:"2.0.0-beta.0", KubernetesVendor:"1.14.1", GitCommit:"b12371ccabd1bc8de7ec7ec1a1ca7bfabe567701", BuildDate:"2019-07-19T19:02:15Z", GoOs:"unknown", GoArch:"unknown"}
go test `go list ./cmd/... ./pkg/... ` -coverprofile=cover.out
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/cmd/manager   [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis      [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis/app  [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis/app/v1alpha1 [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller        [no test files]
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmchannel     11.960s coverage: 90.7% of statements
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmdeployable  [no test files]
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmplacementrule       14.108s coverage: 94.1% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhchannel      11.802s coverage: 88.8% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhdeployable   17.024s coverage: 81.9% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhplacementrule        12.880s coverage: 94.1% of statements
TEST 3
...
...
...
TEST 25

go fmt ./cmd/... ./pkg/...
go vet ./cmd/... ./pkg/...
Version: version.Version{KubeBuilderVersion:"2.0.0-beta.0", KubernetesVendor:"1.14.1", GitCommit:"b12371ccabd1bc8de7ec7ec1a1ca7bfabe567701", BuildDate:"2019-07-19T19:02:15Z", GoOs:"unknown", GoArch:"unknown"}
go test `go list ./cmd/... ./pkg/... ` -coverprofile=cover.out
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/cmd/manager   [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis      [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis/app  [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis/app/v1alpha1 [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller        [no test files]
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmchannel     13.305s coverage: 87.9% of statements
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmdeployable  [no test files]
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmplacementrule       13.710s coverage: 94.1% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhchannel      11.613s coverage: 88.8% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhdeployable   18.473s coverage: 81.9% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhplacementrule        11.596s coverage: 94.1% of statements
[root@lolls-inf hybridapp-operator]#

// 这个版本更清楚点，且带时间。
[root@lolls-inf hybridapp-operator]# for i in {1..15}; do echo -e "***** TEST $i *****"; date; echo -e "\n"; make test; done
***** TEST 1 *****
Sun May 31 23:19:20 PDT 2020


go fmt ./cmd/... ./pkg/...
go vet ./cmd/... ./pkg/...
Version: version.Version{KubeBuilderVersion:"2.0.0-beta.0", KubernetesVendor:"1.14.1", GitCommit:"b12371ccabd1bc8de7ec7ec1a1ca7bfabe567701", BuildDate:"2019-07-19T19:02:15Z", GoOs:"unknown", GoArch:"unknown"}
go test `go list ./cmd/... ./pkg/... ` -coverprofile=cover.out
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/cmd/manager   [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis      [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis/app  [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis/app/v1alpha1 [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller        [no test files]
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmchannel     11.896s coverage: 87.9% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmdeployable  17.399s coverage: 81.7% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmplacementrule       13.766s coverage: 94.1% of statements
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmsubscription        [no test files]
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhchannel      11.960s coverage: 88.8% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhdeployable   17.311s coverage: 81.7% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhplacementrule        12.665s coverage: 94.1% of statements
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhsubscription 18.267s coverage: 87.2% of statements
***** TEST 2 *****
Sun May 31 23:21:26 PDT 2020


go fmt ./cmd/... ./pkg/...
go vet ./cmd/... ./pkg/...
...
...
...
```
```sh
# 但是其实如果测试通过并且代码没有改动，会用缓存的结果（但是我也碰到过前面正确，后面又跑出临时错误的情况）。
# 所以推荐用下面的语句 `go test -count=1 ./pkg/...` 来代替 `make test`。其中起到不缓存作用的主要是`-count=1`

[root@lolls-inf hybridapp-operator]# for i in {1..150}; do echo -e "***** TEST $i *****"; date; echo -e "\n"; go test -count=1 ./pkg/...; done
***** TEST 1 *****
Mon Jul  6 00:14:38 PDT 2020


?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis      [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis/app  [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis/app/v1alpha1 [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller        [no test files]
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/cluster        10.865s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmchannel     11.864s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmdeployable  17.318s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmplacementrule       13.241s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmsubscription        16.990s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhchannel      11.372s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhdeployable   16.919s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhplacementrule        12.399s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhsubscription 15.026s
***** TEST 2 *****
Mon Jul  6 00:16:21 PDT 2020


?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis      [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis/app  [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/apis/app/v1alpha1 [no test files]
?       github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller        [no test files]
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/cluster        9.963s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmchannel     11.067s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmdeployable  17.589s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmplacementrule       14.054s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/ibmsubscription        15.741s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhchannel      10.608s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhdeployable   18.540s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhplacementrule        12.556s
ok      github.ibm.com/IBMPrivateCloud/hybridapp-operator/pkg/controller/rhsubscription 16.596s
***** TEST 3 *****
Mon Jul  6 00:18:16 PDT 2020
...
...
...
```
