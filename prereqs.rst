Prerequisites
=============

在我们开始之前，如果您还没有这样做，您可能希望检查您是否已在将要开发区块链应用程序或运行Hyperledger Fabric的平台上
安装了所有前置条件

Install cURL
------------

Download the latest version of the `cURL
<https://curl.haxx.se/download.html>`__ tool if it is not already
installed or if you get errors running the curl commands from the
documentation.

如果尚未安装过cURL请下载最新版的 `cURL
<https://curl.haxx.se/download.html>`__ ，如果运行cURL命令有误也可以查看该文档。

.. 注意:: 如果你是windows系统的话请查看下面`Windows
   extras`_ 注意事项

Docker and Docker Compose
-------------------------

如果你想基于Hyperledger Fabric开发程序或者改进开发Fabric源程序，那么你需要遵循以下步骤：

  - MacOSX, \*nix, or Windows 10: `Docker <https://www.docker.com/get-docker>`__
    Docker version 17.06.2-ce or greater is required.
  - Older versions of Windows: `Docker
    Toolbox <https://docs.docker.com/toolbox/toolbox_install_windows/>`__ -
    again, Docker version Docker 17.06.2-ce or greater is required.

你可以在terminal运行以下命令来查看Docker版本信息：

.. code:: bash

  docker --version

.. 注意:: 安装Docker for Mac或Windows，或Docker Toolbox也将安装Docker Compose。
          如果您已安装Docker，则应检查是否已安装Docker Compose版本1.14.0或更高版本。
          如果没有，我们建议您安装更新版本的Docker。

你可以在terminal运行以下命令来查看Docker版本信息：

.. code:: bash

  docker-compose --version

.. _Golang:

Go Programming Language
-----------------------

Hyperledger Fabric的大部分组件都是使用go编程语言来开发的。

  - `Go <https://golang.org/dl/>`__ version 1.10.x is required.

鉴于我们将在Go中编写chaincode程序，您需要正确设置两个环境变量; 您可以将这些设置永久保存在适当的启动文件中，
例如您在Linux下使用的是 ``bash`` shell时那么可以在 ``~/.bashrc``写入。

First, you must set the environment variable ``GOPATH`` to point at the
Go workspace containing the downloaded Fabric code base, with something like:
首先，您必须将环境变量设置 ``GOPATH`` 为指向包含下载的Fabric代码库的Go工作区，具体如下：
.. code:: bash

  export GOPATH=$HOME/go

.. note:: 你 **必须** 设置 GOPATH 

  在Linux中Go的 ``GOPATH`` 变量可以是以冒号分隔的目录列表，并且如果没有设置的话将使用默认值 ``$HOME/go`，
  即使这样，当前的Fabric构建框架仍然需要您设置和导出该变量，并且它 **必须** 仅包含Go工作区的单个目录名称。
  （此限制可能会在将来的版本中删除。）

Second, you should (again, in the appropriate startup file) extend your
command search path to include the Go ``bin`` directory, such as the following
example for ``bash`` under Linux:
其次，您应该（再次，在适当的启动文件中）添加包含Go ``bin`` 目录的命令搜索路径，例如Linux下的``bash``示例：

.. code:: bash

  export PATH=$PATH:$GOPATH/bin

While this directory may not exist in a new Go workspace installation, it is
populated later by the Fabric build system with a small number of Go executables
used by other parts of the build system. So even if you currently have no such
directory yet, extend your shell search path as above.
虽然此目录可能不存在于新的Go workspace中，但稍后由在其他部分使用少量Go可执行文件的Fabric构建系统来填充。
因此，即使您目前还没有此类目录，也可以像上面那样扩展 shell 搜索路径。

Node.js Runtime and NPM
-----------------------

If you will be developing applications for Hyperledger Fabric leveraging the
Hyperledger Fabric SDK for Node.js, you will need to have version 8.9.x of Node.js
installed.
如果您将使用Node.js 版本的SDK来开发Hyperledger Fabric的应用程序，
那么需要安装版本为8.9.x的Node.js.

.. 注意:: Node.js 不支持 9.x 的版本.

  - `Node.js <https://nodejs.org/en/download/>`__ - version 8.9.x or greater

.. 注意:: 安装Node.js也会安装NPM，但建议您确认下已安装的NPM版本。您可以npm使用以下命令升级该工具：

.. code:: bash

  npm install npm@5.6.0 -g

Python
^^^^^^

.. 注意:: 以下内容仅适用于Ubuntu 16.04用户。

By default Ubuntu 16.04 comes with Python 3.5.1 installed as the ``python3`` binary.
The Fabric Node.js SDK requires an iteration of Python 2.7 in order for ``npm install``
operations to complete successfully.  Retrieve the 2.7 version with the following command:

默认情况下，Ubuntu 16.04安装了Python 3.5.1作为 ``python3`` 二进制文件。Fabric Node.js SDK需要Python 2.7才能
成功完成``npm install``操作。使用以下命令检索2.7版本：

.. code:: bash

  sudo apt-get install python

Check your version(s):

.. code:: bash

  python --version

.. _windows-extras:

（以下不翻译，为了少出现错误，请尽量在linux或者mac上做开发）
Windows extras
--------------

If you are developing on Windows 7, you will want to work within the
Docker Quickstart Terminal which uses `Git Bash
<https://git-scm.com/downloads>`__ and provides a better alternative
to the built-in Windows shell.

However experience has shown this to be a poor development environment
with limited functionality. It is suitable to run Docker based
scenarios, such as :doc:`getting_started`, but you may have
difficulties with operations involving the ``make`` and ``docker``
commands.

On Windows 10 you should use the native Docker distribution and you
may use the Windows PowerShell. However, for the ``binaries``
command to succeed you will still need to have the ``uname`` command
available. You can get it as part of Git but beware that only the
64bit version is supported.

Before running any ``git clone`` commands, run the following commands:

::

    git config --global core.autocrlf false
    git config --global core.longpaths true

You can check the setting of these parameters with the following commands:

::

    git config --get core.autocrlf
    git config --get core.longpaths

These need to be ``false`` and ``true`` respectively.

The ``curl`` command that comes with Git and Docker Toolbox is old and
does not handle properly the redirect used in
:doc:`getting_started`. Make sure you install and use a newer version
from the `cURL downloads page <https://curl.haxx.se/download.html>`__

For Node.js you also need the necessary Visual Studio C++ Build Tools
which are freely available and can be installed with the following
command:

.. code:: bash

	  npm install --global windows-build-tools

See the `NPM windows-build-tools page
<https://www.npmjs.com/package/windows-build-tools>`__ for more
details.

Once this is done, you should also install the NPM GRPC module with the
following command:

.. code:: bash

	  npm install --global grpc

Your environment should now be ready to go through the
:doc:`getting_started` samples and tutorials.

.. note:: If you have questions not addressed by this documentation, or run into
          issues with any of the tutorials, please visit the :doc:`questions`
          page for some tips on where to find additional help.

.. Licensed under Creative Commons Attribution 4.0 International License
   https://creativecommons.org/licenses/by/4.0/
