# 분기 또는 버전별로 프로젝트 분리

\{% hint style="warning" %\} This feature is currently in Open Beta. There are areas where it is not fully supported. Currently [Snyk Open Source](https://github.com/snyk/user-docs/blob/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/products/snyk-open-source) is supported. \{% endhint %\}

Your project may have multiple states which you want to monitor separately, for example, branches, releases, or deployments. You can use the `--target-reference` option to separate projects into these specific groupings.

`--target-reference` takes any text so you can combine it with a command to automatically set it to a value. Examples follow.

Set `--target-reference` to the current Git branch.

```
snyk monitor --target-reference="$(git branch --show-current)"
```

Use the latest Git tag.

```
snyk monitor --target-reference="$(git describe --tags --abbrev=0)"
```

You can adjust the option for the developer tools used in your project. Any valid Git target can be used.

`--target-reference` allows you to create sub-groupings on the Projects page.

![](https://github.com/snyk/user-docs/raw/5e52535b78618f57eda40eb08fc8fbf91e16f1f0/docs/.gitbook/assets/Screenshot%202021-10-21%20at%2013-08-58%20Projects.png)
