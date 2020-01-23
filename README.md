# Github Workflow

## 第一步：从仓库中 Fork 项目

1. 访问目标项目：https://github.com/yangwenmai/github-workflow
2. 在页面上点击 `Fork` ，给自己的仓库复制一个。

## 第二步：Clone fork 的项目到本地

Clone 你 fork 的项目到你本地的 `$working_dir`

```sh
mkdir -p $working_dir
cd $working_dir
git clone https://github.com/$user/github-workflow.git
# or: git clone git@github.com:$user/github-workflow.git

cd $working_dir/github-workflow
git remote add upstream https://github.com/yangwenmai/github-workflow.git
# or: git remote add upstream git@github.com:yangwenmai/github-workflow.git

# Never push to the upstream master.
git remote set-url --push upstream no_push

# Confirm that your remotes make sense:
# It should look like:
# origin    git@github.com:$(user)/github-workflow.git (fetch)
# origin    git@github.com:$(user)/github-workflow.git (push)
# upstream  https://github.com/yangwenmai/github-workflow (fetch)
# upstream  no_push (push)
git remote -v
```

## 第三步：开新分支

保持你本地 master 分支为最新：

```sh
cd $working_dir/github-workflow
git fetch upstream
git checkout master
git rebase upstream/master
```

从 master 分支开新的特性分支：

```sh
git checkout -b myfeature
# or: gcb myfeature
```

## 第四步：开发

### 编码

你可以在你新创建的 `myfeature` 分支下编码。

## 第五步：保持你的特性分支 `myfeature` 是一直同步原始仓库的最新 master 代码

```sh
# While on your myfeature branch.
git fetch upstream
git rebase upstream/master
```

请不要用 `git pull` 代替 `fetch/rebase`，`git pull` 会创建一个 merge，并且会创建 merge commits。这些会使提交记录混乱和违反规则。你也可以考虑改变你的 `.git/config` 文件，通过 `git config branch.autoSetupRebase` 来改变 git pull 行为。

## 第六步：提交

提交你的变更.

```sh
git commit
```

## 第七步：推送

```sh
git push --set-upstream ${your_remote_name} myfeature
```

## 第八步：创建一个 Pull Request

1. 访问你 fork 的项目：https://github.com/$user/github-workflow
2. 点击 `Compare & Pull Request` 按钮，基于你的 `myfeature` 分支
3. 填充必要的 PR 模板信息。

----

接下来你就只需要等待原始项目的开发人员来审核你的提交即可。

以后如果你还要再开发新的特性或者修复一些 bug，你需要先同步更新项目，然后再创建新的分支，然后都可以按照以上步骤执行。
