FROM mcr.microsoft.com/devcontainers/base:ubuntu

RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y dist-upgrade \
    && apt-get -y install --no-install-recommends htop vim curl git build-essential \
    libffi-dev libssl-dev libxml2-dev libxslt1-dev libjpeg8-dev libbz2-dev \
    zlib1g-dev unixodbc unixodbc-dev libsecret-1-0 libsecret-1-dev libsqlite3-dev \
    jq apt-transport-https ca-certificates gnupg-agent software-properties-common \
    bash-completion make libbz2-dev libreadline-dev libsqlite3-dev \
    wget llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev liblzma-dev faketime libyaml-dev

USER vscode

# Install ASDF
RUN git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.14.1; \
    echo '. $HOME/.asdf/asdf.sh' >> ~/.bashrc; \
    echo '. $HOME/.asdf/completions/asdf.bash' >> ~/.bashrc; \
    echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc; \
    echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc; \
    echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc;

ENV PATH="$PATH:/home/vscode/.asdf/bin/"

# Install ASDF plugins
RUN asdf plugin add ruby https://github.com/asdf-vm/asdf-ruby.git

WORKDIR /workspaces/eps-storage-terraform
ADD .tool-versions /workspaces/eps-storage-terraform/.tool-versions
ADD .tool-versions /home/vscode/.tool-versions

RUN asdf install
