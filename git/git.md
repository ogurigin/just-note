### 关于git

一般建立新的 git仓库后 所要做的

```

git init  //初始化
git add README.md  // 添加说明文档
git commit -m "first commit" // 提交到本地版本库
git remote add origin git@github.com:ogurigin/just-note.git  // 添加远程仓库
git push -u origin master // 上传到远程仓库
```

#### 工作流
对于工作流程方式，常用 3 种方式
-  Git flow
-  Github flow
-  Gitlab flow

#### Merge
建议合并的时候 加上no-off ，即策略合并，这这种方式会多以合并提交，好处是保证一个非常清楚的提交历史，可以看到被合并分支的存在


#### git flow

1. master 主分支 ：用来发布稳定的版本，版本发布后记得打上 git 标签。好处是，在测试的时候，不影响下一个版本功能并行开发

2. Hotfix修复分支：用于线上紧急 bug 修复，修复后，合并回 Master 和 Develop，然后删除分支

3. Release预发分支： 版本提测后，删除 Feature，发现 bug，从 Develop 检出 Release 分支，修改后提交，测试发布后，合并到 Master 和 Develop，然后删除分支

4. Develop开发分支： 用于日常开发，存放最新的开发版，完成一个版本合并到这里

5. Feature功能分支 ： 用来做分模块功能开发，本次版本有 5 个人开发就建 5 个分支，完成后合并到 Develop


#### Github flow
最简单的一种工作流程方式，开源项目就是采用这种方式，含Master + Feature(含 Hotfix)。

- Master 主分支
- Feature 功能分支（Hotfix 补丁分支，补丁也可以看做功能）

#### Gitlab flow
代码的变化，必须由"上游"向"下游"发展，即合并顺序，按环境依次推送，确保代码测试过，从上游分支合并到下游分支。紧急情况下，才允许跳过上游，直接合并到下游分支，即 upstream first，上游优先。
1. Master开发分支 ： 功能分支是开发分支的"上游"

2. Pre-production预发分支： 开发分支是预发分支的"上游"

3. Production生产分支 :  	预发分支又是生产分支的"上游"
