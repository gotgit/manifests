这是 [WHODO](http://www.worldhello.net/doc/whodo_howto/) 项目的 Manifests 版本库。
WHODO 项目中的每个文档使用独立的 Git 版本库进行维护，通过本 Manifests 版本库的 XML 文件组织在一起，
并使用源自 Android 项目的名为 [repo][repolink] 的工具进行管理。

* WHODO 项目中各个文档的版本库位于 [GitHub](https://github.com/gotgit/) 下以 ``doc-`` 前缀开头的版本库。

    一个文档对应一个唯一的版本库，例如 docbook_howto 文档对应于 [doc-docbook_howto 版本库](https://github.com/gotgit/doc-docbook_howto/) 。

* WHODO 项目编译后文档版本库，见 [doc 版本库](https://github.com/gotgit/doc) 。

    主要用于 Web 页面展示： <http://www.worldhello.net/doc/> 。

* [Manifests 版本库](https://github.com/gotgit/manifests/) 以及 Android repo 工具将各个零散版本库组织一起。

Repo 工具的用法，以及编译 WHODO 文档的过程如下：

1. 下载 repo 脚本。

        $ curl -L -k https://github.com/ossxp-com/repo/raw/master/repo > ~/bin/repo
        $ chmod a+x ~/bin/repo

2. 创建工作区目录。

        $ mkdir whodo
        $ cd whodo

3. Repo 初始化及下载 manifests.git 库。

        $ repo init -u git://github.com/gotgit/manifests.git

4. 下载所有相关版本库并检出到工作区。

        $ repo sync
        $ ls -F
        doc/ src/

5. 编译网页。（编译所需工具太繁杂，尚未整理）

        $ repo start whodo
        $ make -C src

6. 更新后的 HTML 文件在 [doc 版本库](https://github.com/gotgit/doc) 中提交。

        $ cd doc
        $ git add -A
        $ git commit

7. 推送至 GitHub 服务器。

        $ repo config repo.pushurl ssh://git@github.com/github/
        $ repo push

[repolink]: http://source.android.com/source/version-control.html "Version Control with Repo and Git"
