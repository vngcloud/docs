# Instructions for installing and configuring the kubectl in Kubenetes

## Necessary conditions <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-truockhibatdau" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-truockhibatdau"></a>

You need to use a kubectl version that is no more than one version different from the cluster version. For example, a client v1.2 should work with master v1.1, v1.2 and v1.3. Using the latest version of kubectl helps avoid unforeseen problems.

***

## **Install kubectl on Linux** <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectltrenlinux" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectltrenlinux"></a>

### Install kubectl binary with curl on Linux <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectlbinaryvoicurltrenlinux" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectlbinaryvoicurltrenlinux"></a>

**Step 1:** Download the latest version with the command:

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```

To download a specific version, replace the section in the command with a specific version.`$(curl -s https://`[`storage`](https://www.thegioimaychu.vn/storage/)`.`[`googleapis.com/kubernetes-release/release/stable.txt`](http://googleapis.com/kubernetes-release/release/stable.txt)`)`

For example, to download version v1.17.0 on Linux, run the command:

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/linux/amd64/kubectl
```

**Step 2:** Create kubectl binary executable via command:

```
chmod +x ./kubectl
```

**Step 3:** Put the binary into your PATH environment variable via the command:

```
sudo mv ./kubectl /usr/local/bin/kubectl
```

**Step 4:** Check to make sure that the version you installed is the latest via command:

```
kubectl version
```

### Install kubectl using the package manager <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectlsudungtrinhquanlygoi" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectlsudungtrinhquanlygoi"></a>

* With CentOS, RHEL or Fedora operating systems, you can run the command:

```
sudo apt-get update && sudo apt-get install -y apt-transport-httpscurl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -echo "deb 
https://apt.kubernetes.io/
 kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.listsudo apt-get updatesudo apt-get install -y kubectl
```

### Install kubectl with snap <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatvoisnap" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatvoisnap"></a>

[If you are using Ubuntu or another Linux distro that supports the snap](https://snapcraft.io/docs/core/install) package manager , kubectl is already available in [snap](https://snapcraft.io/) .

**Step 1:** Switch to user snap and execute the installation command:

```
sudo snap install kubectl --classic
```

**Step 2:** Check the version you just installed is the latest:

```
kubectl version
```

***

## **Install kubectl on macOS** <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectltrenmacos" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectltrenmacos"></a>

### Install kubectl binary with curl on macOS <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectlbinaryvoicurltrenmacos" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectlbinaryvoicurltrenmacos"></a>

**Step 1:** Download the latest version:

```
kubectl versioncurl -LO "
https://storage.googleapis.com/kubernetes-release/release/$(curl
 -s 
https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl
"
```

To download a specific version, replace the section in the command with the specific version. For example, to download v1.17.0 on macOS, run the command:`$(curl -s` [`https://storage.googleapis.com/kubernetes-release/release/stable.txt`](https://storage.googleapis.com/kubernetes-release/release/stable.txt)`)`

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/darwin/amd64/kubectl
```

**Step 2:** Create kubectl binary executable via command:

```
chmod +x ./kubectl
```

**Step 3:** Put the binary into your PATH environment variable via the command:

```
sudo mv ./kubectl /usr/local/bin/kubectl
```

**Step 4:** Check to make sure that the version you installed is the latest via command:

```
kubectl version
```

### Install with Homebrew on macOS <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatvoihomebrewtrenmacos" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatvoihomebrewtrenmacos"></a>

[If you are on macOS and using the Homebrew](https://brew.sh/) package manager , you can install kubectl with Homebrew.

**Step 1:** Run the installation command:

```
brew install kubernetes-cli
```

or command:

```
brew install kubectl
```

**Step 2:** Check to make sure the version you installed is the latest:

```
kubectl version
```

### Install with Macports on macOS <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatvoimacportstrenmacos" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatvoimacportstrenmacos"></a>

[If you are on macOS and using the Macports](https://macports.org/) package manager , you can install kubectl with Macports.

**Step 1:** Run the installation command:

```
sudo port selfupdatesudo port install kubectl
```

**Step 2:** Check to make sure the version you installed is the latest:

```
sudo port selfupdatesudo port install kubectl
```

***

## **Install kubectl on Windows** <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectltrenwindows" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectltrenwindows"></a>

### Install kubectl binary with curl on Windows <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectlbinaryvoicurltrenwindows" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatkubectlbinaryvoicurltrenwindows"></a>

**Step 1:** Download the latest version v1.17.0 from [this link](https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/windows/amd64/kubectl.exe) . Or if you have already installed it `curl`, use the following command:

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/windows/amd64/kubectl.exe
```

To find out the latest stable version, see [https://storage.googleapis.com/kubernetes-release/release/stable.txt](https://storage.googleapis.com/kubernetes-release/release/stable.txt) .

**Step 2:** Include the binary in your PATH environment variable.

**Step 3:** Check to make sure the version `kubectl`is the same as the downloaded version:

```
kubectl version
```

> **Note:** [Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/#kubernetes)`kubectl` adds its own version to the PATH. If you have previously installed Docker Desktop, you may need to set your PATH before the Docker Desktop installation adds a PATH to or removes `kubectl`Docker Desktop's.

### Install with Powershell from PSGallery <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatvoipowershelltupsgallery" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidatvoipowershelltupsgallery"></a>

[If you are on Windows and using the Powershell Gallery](https://www.powershellgallery.com/) package manager , you can install and update kubectl with Powershell.

**Step 1:** Execute the following installation commands (make sure you define your own `DownloadLocation`):

```
Install-Script -Name install-kubectl -Scope CurrentUser -Forceinstall-kubectl.ps1 [-DownloadLocation <path>]
```

> **Note:** If you do not define it `DownloadLocation`, `kubectl`it will be installed in the user's temp directory.

The installation will generate `$HOME/.kube`and instruct you to create a configuration file

**Step 1:** Check to make sure the version you installed is the latest:

```
kubectl version
```

> **Note:** Installation updates will be performed when re-running the commands from step 1.

### Install on Windows using Chocolatey or Scoop <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidattrenwindowssudungchocolateyhoacscoop" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-caidattrenwindowssudungchocolateyhoacscoop"></a>

**Step 1: To install kubectl on Windows you can use the** [Chocolatey](https://chocolatey.org/) package manager or the [Scoop](https://scoop.sh/) command installer .

* If you use Choco

```
choco install kubernetes-cli
```

* If you use Scoop

```
scoop install kubectl
```

**Step 2:** Check to make sure the version you installed is the latest:

```
kubectl version
```

**Step 3:** Move to your home directory:

```
cd %USERPROFILE%
```

**Step 4:** Create folder `.kube`:

```
mkdir .kube
```

**Step 5:** Move to the folder `.kube`you just created:

```
cd .kube
```

**Step 6:** Configure kubectl to use a remote Kubernetes cluster:

```
New-Item config -type file
```

> **Note:** Edit the configuration file with a text editor, such as Notepad.

***

## **Download from part of the Google Cloud SDK** <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-taixuongtumotphancuagooglecloudsdk" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-taixuongtumotphancuagooglecloudsdk"></a>

You can install kubectl from part of the Google Cloud SDK.

**Step 1:** Install [Google Cloud SDK](https://cloud.google.com/sdk/) .

**Step 2:** Execute the installation command `kubectl`:

```
gcloud components install kubectl
```

**Step 3:** Check to make sure the version you installed is the latest:

```
kubectl version
```

***

## **Verify kubectl configuration** <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-xacminhcauhinhkubectl" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-xacminhcauhinhkubectl"></a>

1. For kubectl to search and access your Kubernetes cluster, it needs a kubeconfig file, which is automatically created when you create a new cluster using [kube-up.sh](https://github.com/kubernetes/kubernetes/blob/master/cluster/kube-up.sh) or successfully deploy a Minikube cluster. By default, kubectl's configuration is defined at `~/.kube/config`.
2. Check kubectl is configured correctly by viewing the cluster status: kubectl cluster-info

```
kubectl cluster-info
```

1. If you see a response URL, kubectl is properly configured to access your cluster.
2. If you see a message similar to the one below, kuberctl is not configured correctly or cannot connect to the Kubernetes cluster. `The connection to the server <server-name:port> was refused - did you specify the right host or port?` For example, if you are planning to run a Kubernetes cluster on your laptop (locally), you will need a tool like Minikube installed previously and run the commands above again. If kubectl cluster-info returns the url but you cannot access your cluster, then check if it is configured correctly, by:

```
kubectl cluster-info dump
```

***

## **kubectl configuration options** <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-cacluachoncauhinhkubectl" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-cacluachoncauhinhkubectl"></a>

### Enable shell autocompletion <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-kichhoatshellautocompletion" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-kichhoatshellautocompletion"></a>

* kubectl provides autocompletion support for Bash and Zsh, helping you reduce the need to type many commands.
* Below are the steps to set up autocompletion for Bash (including the differences between Linux and macOS) and Zsh.

***

### **Bash on Linux** <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-bashtrenlinux" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-bashtrenlinux"></a>

#### **Introduce**

* Kubelet completion script for Bash is generated with the command . After the script is created, you need to source (execute) the script to enable the autocompletion feature. **`kubectl completion bash`**
* However, the completion script depends on [**bash-completion**](https://github.com/scop/bash-completion) , so you must install bash-completion beforehand (check bash-completion exists with the command `type _init_completion`).

#### **Install bash-completion**

1. bash-completion is provided by many package managers (see here [)](https://github.com/scop/bash-completion#installation) . You can install with command `apt-get install bash-completion`or `yum install bash-completion`.
2. The above commands generate `/usr/share/bash-completion/bash_completion`, which is the main script of bash-completion. Depending on your package manager, you may have to source this file in a `~/.bashrc`.
3. To find this file, reload your current shell and run the `type _init_completion`. If successful, you are done setting up, otherwise add the following to `~/.bashrc`your file:

```
source /usr/share/bash-completion/bash_completion
```

1. Reload your shell and confirm that bash-completion is installed correctly with the command `type _init_completion`.

#### **Enable kubectl autocompletion**

Now you need to ensure that the kubectl completion script is sourced across all shell sessions. There are 2 ways to do this:

* Source script in file `~/.bashrc`:

```
echo 'source <(kubectl completion bash)' >>~/.bashrc
```

* Add script to folder `/etc/bash_completion.d`:

```
kubectl completion bash >/etc/bash_completion.d/kubectl
```

*   If you have an alias for kubectl, you can add another shell completion to that alias:

    Copy

    ```
    echo 'alias k=kubectl' >>~/.bashrcecho 'complete -F __start_kubectl k' >>~/.bashrc
    ```

> **Note:** bash-completion sources all completion scripts in `/etc/bash_completion.d`.

The above methods are equally effective. After reloading the shell, kubectl autocompletion will work.

***

### **Bash on macOS** <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-bashtrenmacos" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-bashtrenmacos"></a>

#### **Introduce**

Kubectl completion script on Bash is generated by `kubectl completion bash`. This source script will enable the kubectl completion feature.

However, the kubectl completion script depends on [**the bash-completion**](https://github.com/scop/bash-completion) you installed earlier.

> **Warning:** There are two versions of bash-completion, v1 and v2. V1 is for Bash 3.2 (default Bash on macOS), and v2 is for Bash 4.1+. Kubectl completion script **does not work** properly with bash-completion v1 and Bash 3.2. It is compatible with **bash-completion v2** and **Bash 4.1+** . Therefore, to use kubectl completion correctly on macOS, you must install Bash 4.1+ ( [_instructions_](https://itnext.io/upgrading-bash-on-macos-7138bd1066ba) ). The instructions that follow assume that you are using Bash 4.1+ (that is, any Bash version 4.1 or later).

#### **Install bash-completion**

> **Note:** As mentioned, these instructions assume you are using Bash 4.1+, which means that you will be installing bash-completion v2 (as opposed to Bash 3.2 and bash-completion v1, in which case, kubectl completion will not work).

1. You can check if bash-completion v2 was previously installed with the command **`type _init_completion`**. If not, you can install it with Homebrew:

```
brew install bash-completion@2
```

1. From the output of this command, add the following to **`~/.bashrc`**your file: export BASH\_COMPLETION\_COMPAT\_DIR="/usr/local/etc/bash\_completion.d"

```
export BASH_COMPLETION_COMPAT_DIR="/usr/local/etc/bash_completion.d"[[ -r "/usr/local/etc/profile.d/bash_completion.sh" ]] && . "/usr/local/etc/profile.d/bash_completion.sh"
```

Reload your shell and verify that bash-completion v2 is installed correctly using the **`type _init_completion`**.

#### **Enable kubectl autocompletion**

Now you must ensure that the kubectl completion script has been sourced in all your shell sessions. There are many ways to achieve this:

* Source completion script in file `~/.bashrc`:

```
echo 'source <(kubectl completion bash)' >>~/.bashrc
```

* Add completion script to the folder `/usr/local/etc/bash_completion.d`:

```
kubectl completion bash >/usr/local/etc/bash_completion.d/kubectl
```

*   If you have an alias for kubectl, you can extend the completion shell to work with that alias:

    Copy

    ```
    echo 'alias k=kubectl' >>~/.bashrcecho 'complete -F __start_kubectl k' >>~/.bashrc
    ```
* If you have installed kubectl with Homebrew (as introduced [above](https://kubernetes.io/vi/docs/tasks/tools/#install-with-homebrew-on-macos) ) then the kubectl completion script will be included in the **`/usr/local/etc/bash_completion.d/kubectl`**. In this case, you don't need to do anything.

> **Note:** Installing the Homebrew way already sources all the files in the `BASH_COMPLETION_COMPAT_DIR`, which is why the following two methods work.

In any case, after reloading your shell, kubectl completion should work.

***

### **Zsh** <a href="#buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-zsh" id="buoc1-huongdancaidatvacauhinhcongcukubectltrongkubernetes-zsh"></a>

1. Kubectl completion script for Zsh is generated with the command `kubectl completion zsh`. Source completion script in your shell will enable kubectl autocompletion. To make it work for all shells, add the following line to the file `~/.zshrc`:

```
source <(kubectl completion zsh)
```

1. If you have an alias for kubectl, you can extend the completion shell to work with that alias:

```
echo 'alias k=kubectl' >>~/.zshrcecho 'complete -F __start_kubectl k' >>~/.zshrc
```

After reloading the shell, kubectl autocompletion should work.

1. If you get the error complete:13: command not found: compdef, add the following line at the beginning of the file `~/.zshrc`:

```
autoload -Uz compinitcompinit
```

_For more details, see_ [kubernetes.io](http://kubernetes.io/)
