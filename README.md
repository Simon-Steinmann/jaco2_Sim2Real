# jaco2_Sim2Real

#install Git
sudo apt update
sudo apt upgrade
sudo apt install git


#install Ros Melodic
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
sudo apt update
sudo apt install ros-melodic-desktop-full
sudo rosdep init
rosdep update
#install dependencies
sudo apt install python-rosinstall python-rosinstall-generator python-wstool build-essential
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
#installing controllers
sudo apt-get install ros-melodic-ros-controllers*


#install Moveit
sudo apt-get install ros-melodic-trac-ik


#set up catkin workstpace
source ~/.bashrc
cd ~
mkdir catkin_ws
cd catkin_ws
mkdir src
cd src
git clone https://github.com/christian-rauch/kinova-ros.git
rm -r ~/catkin_ws/src/kinova-ros/kinova_moveit/inverse_kinematics_plugins
rm -r ~/catkin_ws/src/kinova-ros/kinova_moveit/kinova_arm_moveit_demo
cd ~/catkin_ws/
catkin_make
rosdep install --from-paths src --ignore-src --rosdistro melodic -y
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc

#setting up vpn server
sudo apt-get update && sudo apt-get install openvpn easy-rsa
make-cadir certificates && cd certificates
#https://linuxconfig.org/openvpn-setup-on-ubuntu-18-04-bionic-beaver-linux
gedit vars
source vars
./clean-all && ./build-ca
./build-key-server server
./build-dh
openvpn --genkey --secret keys/ta.key
sudo cp keys/{server.crt,server.key,ca.crt,dh2048.pem,ta.key} /etc/openvpn



