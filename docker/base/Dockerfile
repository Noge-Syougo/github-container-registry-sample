ARG ROS_DISTRO=melodic
FROM osrf/ros:${ROS_DISTRO}-desktop-full

# GitHubPushテスト
# Dockerのビルドに必要なツールのインストール
#------------------------------------------------
RUN apt-get update -q && apt-get upgrade -yq && apt-get install -y --no-install-recommends \
        libglib2.0-dev-bin \
        dh-python \
        apt-utils \
        python-pip \
        lsb-release \
        tzdata \
    && rm -rf /var/lib/apt/lists/* \
    && pip install --upgrade pip

# 依存ツール/ライブラリのインストール
#------------------------------------------------
RUN apt-get update -q && apt-get install -y --no-install-recommends \
        ros-${ROS_DISTRO}-turtlebot3 \
        ros-${ROS_DISTRO}-turtlebot3-msgs \
        ros-${ROS_DISTRO}-turtlebot3-simulations \
        ros-${ROS_DISTRO}-aruco-ros \
    && rm -rf /var/lib/apt/lists/*

# 依存ツール/ライブラリのインストール
#------------------------------------------------
RUN apt-get update -q && apt-get install -y --no-install-recommends \
        gnome-terminal \
        dbus-x11 \
        at-spi2-core \
        python-tk \
        python-pil.imagetk \
    && rm -rf /var/lib/apt/lists/*

# 開発者ユーザーの追加
#------------------------------------------------
ARG USERNAME=developer
RUN useradd --create-home --home-dir /home/${USERNAME} --shell /bin/bash --user-group --groups adm,sudo,video,audio ${USERNAME} \
    && echo ${USERNAME}:${USERNAME} | chpasswd \
    && echo "${USERNAME} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER ${USERNAME}

# ROSの初期化
#------------------------------------------------
RUN test -f /etc/ros/rosdep/sources.list.d/20-default.list && \
    sudo rm /etc/ros/rosdep/sources.list.d/20-default.list
RUN sudo rosdep init && \
    rosdep update

# コンテナ初期化
# -----------------------------------------------
CMD [ "bash" ]


