## [3. 如何进行本地测试](https://edu.n2sys.cn/#/tut_lab/lv1/1.myftp?id=_3-%e5%a6%82%e4%bd%95%e8%bf%9b%e8%a1%8c%e6%9c%ac%e5%9c%b0%e6%b5%8b%e8%af%95)

我们已经提供了自动评测的程序，在接受 Github Classroom 邀请后每位同学有独立的 Github 仓库。
如果无法进行正常测试，请和助教联系。

### [3.1 获取仓库](https://edu.n2sys.cn/#/tut_lab/lv1/1.myftp?id=_31-%e8%8e%b7%e5%8f%96%e4%bb%93%e5%ba%93)

1. 从远程仓库 clone
2. 在根目录中执行 `git submodule update --init`
3. 在根目录中执行 `git submodule update --remote`
4. 建议 clone 和 push 仓库的操作都在容器外进行，避免容器内的用户配置、代理等等问题；将仓库放在挂载入容器的目录下（默认为 `netlab-lab0`），仅在容器内进行编译和测试

### [3.2 编译 myFTP 程序](https://edu.n2sys.cn/#/tut_lab/lv1/1.myftp?id=_32-%e7%bc%96%e8%af%91-myftp-%e7%a8%8b%e5%ba%8f)

在根目录中执行 `mkdir build && cd build && cmake .. && make -j`
我们期望此时在 `build` 目录下应该有两个可执行文件 `ftp_server` 和 `ftp_client` 分别是你编写的 Server 和 Client 程序。

### [3.3 编译测试程序](https://edu.n2sys.cn/#/tut_lab/lv1/1.myftp?id=_33-%e7%bc%96%e8%af%91%e6%b5%8b%e8%af%95%e7%a8%8b%e5%ba%8f)

我们提供了本地化的测试程序，如果需要在本地进行测试，请参考下述步骤。

1. 如果你在上面的获取仓库一节成功执行了 `git submodule update --remote` 命令，此时你的项目根目录下应该有文件夹 `test_local`。
2. 进入该文件夹内，你应该能看到 `ftp_client_std` 和 `ftp_server_std` 两个程序分别是标准的 Server 和 Client 程序。
3. 在 `test_local` 文件内执行 `mkdir build && cd build && cmake .. && make -j`，开始编译自动测试程序。
4. 编译完成后，你应该能在 `test_local/build` 目录下看到可执行文件 `ftp_test`。
5. 将 `test_local/ftp_client_std`, `test_local/ftp_server_std` 和 `test_local/build/ftp_test` 三个程序拷贝到你在上一节编译 `myFTP` 得到 `ftp_client` 和 `ftp_server` 两个可执行文件的 `build` 目录下。

将上述步骤均完成后，一个供参考的文件目录示意图如下：

```plain
CMakeLists.txt
ftp_server.cpp
ftp_client.cpp
build/
      ftp_server
      ftp_client
      ftp_server_std
      ftp_client_std
      ftp_test
      （其它文件）
test_local/
          CMakeLists.txt
          ftp_server_std
          ftp_client_std
          test.cpp
          build/
                ftp_test
                （其他文件）
          （其它文件）
（其它文件）
```

注意若自动测试程序发生更新则需要执行如下指令获取最新的测试程序（我们会在教学网和微信群进行通知）:
在根目录中执行 `git submodule update --remote`，并重新执行上述步骤 3, 4, 5 即可
