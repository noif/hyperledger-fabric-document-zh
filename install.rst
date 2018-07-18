Install Samples, Binaries and Docker Images
===========================================

在我们在Hyperledger Fabric上开发真正的应用程序时，我们提供了一个脚本，
该脚本可以下载并安装 一些例子和 二进制文件 到您的系统。我们认为您会发现安装的示例应用程序对于
了解更多信息有关Hyperledger Fabric的功能和操作方面非常有用。

.. 注意:: If you are running on **Windows** you will want to make use of the
	  Docker Quickstart Terminal for the upcoming terminal commands.
          Please visit the :doc:`prereqs` if you haven't previously installed
          it.

          If you are using Docker Toolbox on Windows 7 or macOS, you
          will need to use a location under ``C:\Users`` (Windows 7) or
          ``/Users`` (macOS) when installing and running the samples.

          If you are using Docker for Mac, you will need to use a location
          under ``/Users``, ``/Volumes``, ``/private``, or ``/tmp``.  To use a different
          location, please consult the Docker documentation for
          `file sharing <https://docs.docker.com/docker-for-mac/#file-sharing>`__.

          If you are using Docker for Windows, please consult the Docker
          documentation for `shared drives <https://docs.docker.com/docker-for-windows/#shared-drives>`__
          and use a location under one of the shared drives.

确定一个你机子上要放置fabric-samples 源代码的文件夹，并在终端窗口中定位到该目录。下面的的命令将执行以下步骤：

#. If needed, clone the `hyperledger/fabric-samples` repository
#. Checkout the appropriate version tag
#. Install the Hyperledger Fabric platform-specific binaries and config files
   for the version specified into the root of the fabric-samples repository
#. Download the Hyperledger Fabric docker images for the version specified

准备好后，在下载有Fabric Samples源代码的目录中，继续执行以下命令：

.. code:: bash

  curl -sSL http://bit.ly/2ysbOFE | bash -s 1.2.0

.. 注意:: 如果要下载Fabric，Fabric-ca和第三方Docker镜像，则必须提供版本标识符

.. code:: bash

  curl -sSL http://bit.ly/2ysbOFE | bash -s <fabric> <fabric-ca> <thirdparty>
  curl -sSL http://bit.ly/2ysbOFE | bash -s 1.2.0 1.2.0 0.4.10

.. note:: 如果运行上述curl命令时出错，则可能使用了不能处理重定向或不受支持的环境的旧版本curl

    请访问 :doc:`prereqs` 页面，了解有关在何处查找最新版本curl并获取正确环境的其他信息。或者，
    您可以替换成长URL：https://github.com/hyperledger/fabric/blob/master/scripts/bootstrap.sh

.. note:: 您可以对任何已发布的Hyperledger Fabric版本使用上述命令。只需将1.2.0替换为您要安装的版本的版本标识符即可。

上面的命令下载并执行一个bash脚本，该脚本将下载并提取设置网络所需的所有特定于平台的二进制文件，
并将它们放入您在上面创建的文件夹中。它会生成特定于平台的二进制文件：

  * ``cryptogen``,
  * ``configtxgen``,
  * ``configtxlator``,
  * ``peer``,
  * ``orderer``,
  * ``idemixgen``, and
  * ``fabric-ca-client``

并将它们放在bin当前工作目录的子目录中。

您可能希望将其添加到PATH环境变量中，以便在不完全限定每个二进制文件的路径的情况下使用这些可执行命令。例如：

.. code:: bash

  export PATH=<path to download location>/bin:$PATH

最后，该脚本会将`Docker Hub <https://hub.docker.com/u/hyperledger/>`__ 中的Hyperledger Fabric docker images下载 
到本地Docker images库中，并将其标记为“latest”。

该脚本在结束时会列出了安装的Docker镜像。

查看每个图像的名称; 这些组件最终将构成我们的Hyperledger Fabric网络。 您还会注意到，您有两个具有相同图像ID的实例
 - 一个标记为“amd64-1.x.x”，另一个标记为“latest”。 在1.2.0之前，下载的图像由 ``uname -m``  确定，并显示为“x86_64-1.x.x”。

.. note:: On different architectures, the x86_64/amd64 would be replaced
          with the string identifying your architecture.

.. note:: If you have questions not addressed by this documentation, or run into
          issues with any of the tutorials, please visit the :doc:`questions`
          page for some tips on where to find additional help.

.. Licensed under Creative Commons Attribution 4.0 International License
   https://creativecommons.org/licenses/by/4.0/
