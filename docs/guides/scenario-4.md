---
title: Scenarios | Kubepack
menu:
  docs_0.1.0:
    identifier: s4-guides
    name: Scenario 4
    parent: guides
    weight: 70
menu_name: docs_0.1.0
section_menu_id: guides
---

> New to Kubepack? Please start [here](/docs/concepts/README.md).

# Scenario-4

**This docs trying to explain the behavior of Pack**
***

This section explain [test-4](https://github.com/kubepack/pack/tree/master/docs/_testdata/test-4).

If you look into this test's `dependency-list.yaml` file.

```console
$ cat dependency-list.yaml

items:
- package: github.com/kubepack/kube-a
  branch: test-4
- package: github.com/kubepack/kube-b
  branch: test-4
```

Here, [test-4](https://github.com/kubepack/pack/tree/master/docs/_testdata/test-4) depends on two repositories.  
  
1. branch `test-4` of [kube-a](https://github.com/kubepack/kube-a/tree/test-4).  
2. branch `test-4` of [kube-b](https://github.com/kubepack/kube-b/tree/test-4).

Both repositories(kube-a and kube-b) depends on two different branch of [kube-c](https://github.com/kubepack/kube-c). `kube-a` depends on branch `test-1` of `kube-c` and `kube-b` depends on `master` branch of `kube-c`.

 To clarify, see image.
 
![alt text](/docs/_testdata/test-4/test-4.jpg)

 Now, when run `$ pack dep -f . --v=10` command, `pack` could not resolve dependencies. As, this dependencies contradict with each other.
  Give below error.

  ```console
  $ pack dep -f . --v=10
  
  
  
  I0108 15:58:18.241539   16369 logs.go:19] No versions of github.com/kubepack/kube-a met constraints:
          master: Could not introduce github.com/kubepack/kube-a@master, as it is not allowed by constraint test-4 from project github.com/kubepack/pack/_testdata/test-4.
          dep-c: Could not introduce github.com/kubepack/kube-a@dep-c, as it is not allowed by constraint test-4 from project github.com/kubepack/pack/_testdata/test-4.
          test-1: Could not introduce github.com/kubepack/kube-a@test-1, as it is not allowed by constraint test-4 from project github.com/kubepack/pack/_testdata/test-4.
          test-10: Could not introduce github.com/kubepack/kube-a@test-10, as it is not allowed by constraint test-4 from project github.com/kubepack/pack/_testdata/test-4.
          test-2: Could not introduce github.com/kubepack/kube-a@test-2, as it is not allowed by constraint test-4 from project github.com/kubepack/pack/_testdata/test-4.
          test-3: Could not introduce github.com/kubepack/kube-a@test-3, as it is not allowed by constraint test-4 from project github.com/kubepack/pack/_testdata/test-4.
          test-4: Could not introduce github.com/kubepack/kube-a@test-4, as it has a dependency on github.com/kubepack/kube-c with constraint test-1, which has no overlap with existing constraint master from github.com/kubepack/kube-b@test-4
          test-6: Could not introduce github.com/kubepack/kube-a@test-6, as it is not allowed by constraint test-4 from project github.com/kubepack/pack/_testdata/test-4.
          test-7: Could not introduce github.com/kubepack/kube-a@test-7, as it is not allowed by constraint test-4 from project github.com/kubepack/pack/_testdata/test-4.
          test-8: Could not introduce github.com/kubepack/kube-a@test-8, as it is not allowed by constraint test-4 from project github.com/kubepack/pack/_testdata/test-4.
```

## Next Steps

- Want to publish apps using Kubepack? Please visit [here](/docs/concepts/how/publisher.md).
- Want to consume apps published using Kubepack? Please visit [here](/docs/concepts/how/user.md).
- To learn about `dependency-list.yaml` file, please visit [here](/docs/concepts/how/manifest.md).
- Learn more about `pack` cli from [here](/docs/concepts/how/cli.md).
