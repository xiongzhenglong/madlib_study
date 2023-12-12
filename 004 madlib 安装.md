sudo apt-get update
sudo apt-get install -y cmake g++ m4 python3-pip python3-dev libboost-dev libboost-system-dev libboost-thread-dev git postgresql-server-dev-15 build-essential postgresql-plpython3-15
cd ~
git clone https://github.com/apache/madlib.git
cd madlib
 git checkout madlib2-master # 或选择一个特定版本  非常关键
./configure
sudo make
sudo make install
psql -U postgres
CREATE DATABASE madlib_db;
\q



export PATH=$PATH:~/madlib/build/src/bin

既然您已经找到了`pg_ctl`的位置（`/usr/lib/postgresql/15/bin/pg_ctl`），接下来需要确保这个路径被包含在您的系统的PATH环境变量中。这样，当运行需要`pg_ctl`的命令时，系统能够找到它。请按照以下步骤操作：

1. **编辑环境变量配置文件**：您需要编辑您的shell配置文件（通常是`~/.bashrc`或`~/.bash_profile`，具体取决于您使用的shell和操作系统）。使用文本编辑器打开这个文件，例如使用命令`nano ~/.bashrc`。

2. **添加pg_ctl到PATH**：在打开的配置文件中，添加以下行：

   ```bash
   export PATH=$PATH:/usr/lib/postgresql/15/bin
   ```

   这行命令将`pg_ctl`所在的目录添加到PATH环境变量中。

3. **保存并关闭文件**：保存对配置文件的更改，并关闭编辑器。

4. **重新加载配置**：为使更改生效，您需要重新加载配置文件。可以通过运行以下命令来实现：

   ```bash
   source ~/.bashrc
   ```

   或者，如果您编辑的是`~/.bash_profile`，则运行：

   ```bash
   source ~/.bash_profile
   ```

5. **验证更改**：为了验证`pg_ctl`是否现在可以被系统找到，您可以在终端中运行`which pg_ctl`。如果一切正常，它应该返回`pg_ctl`的路径。

6. **重试MADlib安装**：完成这些步骤后，您应该可以重新尝试安装MADlib，这次应该不会遇到关于`pg_ctl`的错误了。

如果在这个过程中遇到任何问题，建议参考PostgreSQL和您所使用操作系统的相关文档。

当您尝试使用 `sudo` 运行 `madpack` 命令时遇到 “command not found” 错误，这可能是因为 `madpack` 命令的位置没有包含在 `root` 用户的 `PATH` 环境变量中。这通常发生在使用 `sudo` 时，因为 `sudo` 默认不使用当前用户的 `PATH` 环境变量。

要解决这个问题，您有几个选择：

1. **使用完整路径执行命令**：找到 `madpack` 命令的完整路径，然后使用这个路径来运行命令。例如：

   ```bash
   sudo /full/path/to/madpack install -s madlib -p postgres -c postgres@localhost/madlib_db
   ```

   您可以通过在普通用户模式下运行 `which madpack` 来找到 `madpack` 的完整路径。

2. **临时修改 `sudo` 的 `PATH`**：在 `sudo` 命令中临时修改 `PATH`。例如：

   ```bash
   sudo PATH=$PATH madpack install -s madlib -p postgres -c postgres@localhost/madlib_db
   ```

   这会将当前用户的 `PATH` 环境变量传递给 `sudo`。

3. **以 `postgres` 用户运行命令**：尝试以 `postgres` 用户身份运行命令，因为 `postgres` 用户可能有正确配置的环境变量。首先切换到 `postgres` 用户：

   ```bash
   sudo -i -u postgres
   ```

   然后运行 `madpack` 命令。

4. **永久修改 `root` 用户的 `PATH`**：编辑 `root` 用户的 `bash` 配置文件（如 `/root/.bashrc`），加入 `madpack` 命令所在的路径到 `PATH` 环境变量中。

5. **检查 `madpack` 的安装**：确保 `madpack` 已经正确安装在系统中，并且其可执行文件位于某个被 `PATH` 环境变量包含的目录中。

如果这些步骤仍然无法解决问题，您可能需要重新检查 `madpack` 的安装步骤，确保它已正确安装在您的系统上。

sudo PATH=$PATH madpack install -s madlib -p postgres -c postgres@localhost/madlib_db

sudo madpack install -s madlib -p postgres -c postgres@localhost/madlib_db

psql -U postgres -d madlib_db -c "SELECT madlib.version();"


find  -name madpack
