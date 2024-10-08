# su & sudo

## su

在Linux系统中，`su`命令是一个非常有用的命令，它允许用户切换到另一个用户的身份，默认情况下，如果没有指定用户，它会尝试切换到root用户。这个命令在需要执行需要更高权限的任务时非常有用。

### 基本用法

- **切换到root用户**：

如果你想要切换到root用户，可以简单地输入`su`然后输入root用户的密码（在某些配置中，你可能不需要输入自己的密码就能切换到root，但这通常不推荐出于安全考虑）。

```sh
su
```

或者更明确地指定root用户：

```sh
su - root
```

使用`-`选项会启动一个新的shell作为root用户，并且加载root用户的环境变量和配置文件（如`.bashrc`或`.bash_profile`）。

- **切换到其他用户**：

如果你想要切换到另一个非root用户，你可以在`su`命令后指定用户名。

```sh
su - 用户名
```

同样地，使用`-`选项会启动一个新的shell并加载该用户的环境。

### 注意事项

- **安全性**：使用`su`命令时，特别是切换到root用户，要非常小心，因为你可以执行任何命令，包括那些可能损坏系统或数据的命令。
- **密码**：当你尝试使用`su`切换到另一个用户时，系统会提示你输入目标用户的密码，而不是你自己的密码。
- **sudo**：在许多现代Linux发行版中，`sudo`命令被用作`su`的替代品，因为它提供了更细粒度的权限控制。使用`sudo`，你可以配置哪些用户或用户组可以执行哪些命令，而不需要知道root的密码。
- **环境变量**：<u>当你使用`su`切换到另一个用户时，你的环境变量（如`PATH`）可能不会改变，除非你使用了`-`选项。这可能会导致某些命令因为不在新的`PATH`中而无法找到。</u>

### 结论

`su`命令是Linux系统中一个强大的工具，允许用户切换到另一个用户的身份。然而，在使用时应该小心谨慎，特别是当切换到root用户时。在可能的情况下，考虑使用`sudo`来执行需要更高权限的命令，因为它提供了更好的安全性和灵活性。

## sudo

sudo 以`自己的身份`来执行其他用户的命令。 

Linux中的`sudo`命令是一个非常强大且常用的工具，它允许系统管理员授权某些用户（或用户组）以其他用户（通常是root用户）的身份来执行命令。以下是关于`sudo`命令的详细解释：

### 一、基本用法

- **执行命令**：在命令前加上`sudo`，然后输入用户密码（如果当前用户被授权使用sudo），**即可**以超级用户权限执行该命令。例如，`sudo apt-get update`会以root权限更新系统的软件包。
- **切换到其他用户**：使用`sudo -u 用户名 命令`的格式，可以以指定用户的身份执行命令。例如，`sudo -u john ls`会以john用户的身份执行`ls`命令。  sudo -u root  shutdown -c
- **切换到root用户**：直接输入`sudo su`或`sudo -i`（后者会启动一个root用户的交互式shell）即可切换到root用户身份。

`visudo` 设置需要使用sudo的用户（组）

### 二、特性与优势

- **安全性**：sudo减少了root用户的登录和管理时间，提高了系统的安全性。普通用户不需要知道root密码即可执行需要较高权限的命令，且sudo提供了详细的日志记录功能，可以追踪用户的操作。
- **灵活性**：sudo的配置文件`/etc/sudoers`允许系统管理员灵活地管理用户的使用权限和使用的主机。通过编辑这个文件，可以精确控制哪些用户可以执行哪些命令。
- **时间戳文件**：sudo使用时间戳文件来执行类似的“检票”系统。当用户调用sudo并输入密码时，用户获得了一张存活期为默认5分钟（可配置）的票，在此期间内再次使用sudo无需再次输入密码。

%wheel  用户组

### 四、常用选项

- `-l`：列出当前用户可以执行的命令和文件。

- `-u`：指定以哪个用户的身份执行命令。

- `-s`：以root用户的身份启动一个新的shell。

- `-i`：以root用户的身份启动一个新的交互式shell，类似于直接登录为root用户。

- `-k`：撤销sudo的密码缓存，下次使用sudo时需要重新输入密码。

  

### 五、注意事项

- 在使用sudo时，应确保只有可信任的用户才被授权使用，以避免安全风险。
- 修改sudo配置文件时应谨慎操作，以免破坏系统的安全性。
- 定期检查sudoers文件的配置，确保只有需要的用户和命令被授权使用sudo。

综上所述，`sudo`命令是Linux系统中不可或缺的一部分，它提供了强大的权限管理功能，使得系统管理更加灵活和安全。

```sh
visudo 

user3 ALL=/sbin/shutdown -c

##Same thing without password
%wheel ALL=(ALL)  NOPASSWD: ALL
#%wheel  用户组
#ALL 图形用户界面或Command模式都支持， 如果localhost， 表示只支持command模式
#(ALL) 所有的命令


:wq
```



:!which shutdown  在vi的模式下查看某个命令的位置

