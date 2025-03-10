# JAIL

Jülich Advanced Imaging Toolbox

## Onboarding

### Install Required Software

To set up your development environment, install the following:

- **[VS Code](https://code.visualstudio.com/)** – Code editor with DevContainer support.
- **[Podman Desktop](https://podman-desktop.io/)** – GUI for managing Podman containers.

**Note:** After installing Podman Desktop, enable the **Docker compatibility** option in **Settings > Experimental**. Restart any open VS Code instances to apply the changes.

### Install the **Dev Containers** extension in VS Code:

1. Open VS Code.
2. Go to **Extensions** (`Ctrl+Shift+X`).
3. Search for **Dev Containers**.
4. Install the extension from **Microsoft** or [visit the repo](https://github.com/devcontainers).

### Configure VS Code for Podman

Set the VS Code setting for `Dev Containers > Containers: Docker Path` path to `podman`.
This can also be done in the user settings JSON by adding the following line:

```json
"dev.containers.dockerPath": "podman"
```

### Clone the Repository

Ensure you have Git installed, then clone the repository:

```sh
git clone git@github.com:inm-4/jail.git
cd jail
```

### Sharing Git Credentials with the Container

To authenticate with Git inside the container, install **Git** and **SSH** on your host machine:

```sh
git config --global user.name "Your Name"
git config --global user.email "your.email@address"
```

Ensure your SSH agent is running and your key is added:

```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

For persistent SSH authentication, consider adding this to your `~/.bashrc` or `~/.zshrc`:

```sh
if [ -z "$SSH_AUTH_SOCK" ]; then
    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_rsa
fi
```

More details: [Sharing Git Credentials with Containers](https://code.visualstudio.com/remote/advancedcontainers/sharing-git-credentials).

### Open the Project in a DevContainer

1. Open **VS Code**.
2. Press `Ctrl+Shift+P` and select **Dev Containers: Open Folder in Container…**.
3. Choose the cloned **QRAGE** project folder.
4. Wait for the container to build and start.

Once started, you're ready to code inside the containerized development environment.

### Autoformatting and Linting

The code uses Ruff for autoformatting and linting. Please install the git precommit hook

## Linting and Formatting

We use **Ruff** for linting and formatting. Make sure to install and use it correctly:

### Setting Up Pre-Commit Hooks

To ensure consistency, we use **pre-commit hooks** for automatic linting and formatting before committing changes.
Open a terminal inside VS Code. Make sure that the directory path is pointing to `/workspaces/jail` 

Set up the pre-commit hook:
```sh
pre-commit install
```

From now on, every time you commit code, `pre-commit` will automatically check and format files according to our rules.

For manual checks, you can run:
```sh
pre-commit run --all-files
```

To verify if the pre-commit hook is active, run:
```sh
ls -l .git/hooks/pre-commit
```

## Issues

### Files Showing as Modified in Git

After opening the repository in the DevContainer, all files may appear as modified due to file mode changes:

```
diff --git a/<filename> b/<filename>
old mode 100644
new mode 100755
```

To prevent this issue, we use the following setting in `devcontainer.json`:

```json
"postCreateCommand": "git config core.fileMode false"
```

For more details, see the related discussion: [VS Code Remote Issue #1134](https://github.com/microsoft/vscode-remote-release/issues/1134).

