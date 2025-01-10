# ROS 2 Humble Installation Guide

This guide covers the installation of ROS 2 Humble on Ubuntu 22.04 LTS (Jammy Jellyfish).

## System Requirements
- Ubuntu 22.04 LTS
- At least 2GB RAM
- At least 20GB free disk space
- Internet connection

## 1. Set Locale
```bash
locale  # Verify current locale settings
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

## 2. Setup Sources

### 2.1 Enable Ubuntu Universe Repository
```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```

### 2.2 Add ROS 2 GPG Key
```bash
sudo apt update && sudo apt install curl
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

### 2.3 Add ROS 2 Repository
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

## 3. Install ROS 2 Packages

### 3.1 Update Package Lists
```bash
sudo apt update
```

### 3.2 Install ROS 2 (Choose ONE of the following options)

#### Desktop Installation (Recommended)
```bash
sudo apt install ros-humble-desktop
```

#### Base Installation (Minimal)
```bash
sudo apt install ros-humble-ros-base
```

#### Development Tools
```bash
sudo apt install ros-dev-tools
```

## 4. Environment Setup

### 4.1 Add ROS 2 Setup to .bashrc
```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

## 5. Verify Installation

### 5.1 Test Publisher
Open a new terminal and run:
```bash
ros2 run demo_nodes_cpp talker
```

### 5.2 Test Subscriber
Open another terminal and run:
```bash
ros2 run demo_nodes_cpp listener
```

## 6. Install Additional Tools (Optional)

### 6.1 Install colcon build system
```bash
sudo apt install python3-colcon-common-extensions
```

### 6.2 Install rosdep
```bash
sudo apt install python3-rosdep
sudo rosdep init
rosdep update
```

## Troubleshooting

### Common Issues

1. **GPG Key Issues**
```bash
sudo apt-key del [key]
# Then repeat the GPG key installation steps
```

2. **Package Dependencies**
```bash
sudo apt install -f
```

3. **Permission Issues**
```bash
sudo chown -R $USER:$USER ~/ros2_ws
```

### Environment Variables
If ROS 2 commands aren't recognized, ensure environment is properly sourced:
```bash
printenv | grep -i ROS
```

## Additional Resources
- ROS 2 Documentation: https://docs.ros.org/en/humble/
- ROS 2 Tutorials: https://docs.ros.org/en/humble/Tutorials.html
- ROS 2 Community Support: https://discourse.ros.org/