# Hayunje_tutoria 
(1)ROS Melodic install

http://wiki.ros.org/melodic/Installation/Ubuntu 에 들어가 Ubunt 18.04 version에 맞는 ROS Melodic을 설치하였습니다.
sources.list 설정하기 위해 다음과 같은 코드를 Terminal에 입력해줍니다.

```sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $ (lsb_release -sc) main"> /etc/apt/sources.list.d/ros-latest.list' ```

키 설정을 해줍니다.

```sudo apt-key adv --keyserver 'hkp : //keyserver.ubuntu.com : 80'--recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654```

Debian pakage index가 최신 버전인지 확인해줍니다.

``` sudo apt update ```

ROS에는 다양한패키지가 있습니다.
그중에서도 Desktop-Full 을 설치합니다. (ROS, rqt, rviz, robot-generic libraries, 2D/3D simulators and 2D/3D perception)

```sudo apt install ros-melodic-desktop-full```

새로운 셀이 시작될 때마다 ROS 환경 Valiables이 bash에 자동으로 추가되도록해줍니다. 

```echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc```  
```source ~/.bashrc```

현재 쉘의 환경을 변경하려면 위의 대신 다음을 입력 할 수 있습니다.

ROS 패키지 빌드를 위한 기타 Dependencies을 설치합니다.

```sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential```

ROS dep을 설치합니다.

```sudo apt install python-rosdep```

다음과 같이 rosdep을 초기화합니다.

```sudo rosdep init```
```rosdep update```

(2) Universial Robot _tutorial

패키지설치를 합니다.
catkin의 workspace를 생성합니다.

```mkdir -p catkin_ws/src && cd catkin_ws```

Driver를 clone.

```git clone https://github.com/UniversalRobots/Universal_Robots_ROS_Driver.git src/Universal_Robots_ROS_Driver```

```git clone -b calibration_devel https://github.com/fmauch/universal_robot.git src/fmauch_universal_robot```

dependencies를 설치합니다.

 ```sudo apt update -qq```
 ```rosdep update```
 
 위를 실행하던 중 
![스크린샷, 2021-05-29 22-41-53](https://user-images.githubusercontent.com/84005711/120072501-32eba780-c0cf-11eb-9194-5b6afac330b8.png)

위와 같은 오류가 계속적으로 발생하여 원인을 찾아보려하였지만 파일이 겹쳐 충돌되어 update가 진행이 안된다고 판단하여 우분투 환경을 재설치하였습니다.
그 후, 다시 진행하였습니다.

dependencies을 설치합니다.

 ```sudo apt update -qq```
 ```rosdep update```
```rosdep install --from-paths src --ignore-src -y```


workspace를 만들어줍니다.

 ``` catkin_make```

 만든 workspace를 활성화시킵니다.
 
 ```source devel/setup.bash```
 
![스크린샷, 2021-05-29 22-48-22](https://user-images.githubusercontent.com/84005711/120072682-071cf180-c0d0-11eb-89dc-c74c870d6af0.png)
![스크린샷, 2021-05-29 22-48-36](https://user-images.githubusercontent.com/84005711/120072685-084e1e80-c0d0-11eb-9907-d1c7cb1f036f.png)

(3) gazebo example

Usage with Gazebo Simulation

```roslaunch ur_gazebo ur5.launch```

새로운 terminal 실행후,
MoveIt! with a simulated robot

```roslaunch ur5_moveit_config ur5_moveit_planning_execution.launch sim:=true```

또 다른 terminal 실행 후,
For starting up RViz with a configuration including the MoveIt! Motion Planning plugin run:

```roslaunch ur5_moveit_config moveit_rviz.launch config:=true```

위를 실행하게 되면
![스크린샷, 2021-05-29 23-01-55](https://user-images.githubusercontent.com/84005711/120073453-57498300-c0d3-11eb-932f-87e94bf8771c.png)
![스크린샷, 2021-05-29 23-01-48](https://user-images.githubusercontent.com/84005711/120073488-7516e800-c0d3-11eb-8f3b-c4810ada359b.png)
*gazebo & RViz실행화면 

![스크린샷, 2021-05-20 21-46-44](https://user-images.githubusercontent.com/84005711/120073506-88c24e80-c0d3-11eb-9e36-21db8f6989a8.png)
 ![스크린샷, 2021-05-20 21-47-08](https://user-images.githubusercontent.com/84005711/120073507-8c55d580-c0d3-11eb-886a-9bca9f057050.png)
![스크린샷, 2021-05-20 21-47-16](https://user-images.githubusercontent.com/84005711/120073510-8e1f9900-c0d3-11eb-814a-3dcc3c0486fb.png)
![스크린샷, 2021-05-20 21-47-25](https://user-images.githubusercontent.com/84005711/120073511-8fe95c80-c0d3-11eb-8d3a-f8fb45cb1bd2.png)

위와 같은 ERROR가 발생합니다.



(4) rrbot_pushing_object

이 과제는 RRbot이 물체를 밀어내는 간단한 작업이다.
```cd  ~ / catkin_ws```
```catkin_make ``` 
ROS 작업공간을 만들어줍니다.

패키지가 내장되어, ```rrbot_pushing_object```를 사용하여 시뮬레이션 환경을 시작할 수 있습니다.
```cd  ~ / catkin_ws / src / rrbot_pushing_object / rrbot_pushing_object_basic```
```bash rrbotsimstart.sh```

기본 스크립트 ```rrbotsimstart.sh``` 는 별도의 터미널에서 4 개의 다른 스크립트를 실행합니다.
```rrbot_gazebo_launch.sh``` 파일에 나열된 객체 모델 이있는 Gazebo 시작
```rrbot_ros_control.sh```  
```rrbot_pushing_object.sh``` 
```rrbot_camera_view.sh``` RR bot 팔, 테이블 및 판지 상자와 같은 고정 된 객체, 카메라,Bot 팔 컨트롤러 (ROS 관절 위치 컨트롤러)를 로드하기

![스크린샷, 2021-06-03 15-53-55](https://user-images.githubusercontent.com/84005711/120608673-6beb9980-c48c-11eb-8ad8-6b237b1a2863.png)
위와 같은 오류가 발생하여  rrbotsimstart.sh파일을 열어 -x부분을 모두 --로 수정하였습니다.
![스크린샷, 2021-06-03 15-54-11](https://user-images.githubusercontent.com/84005711/120608722-786ff200-c48c-11eb-99a3-eab44b432dcb.png)

그후 다시 실행시 
![스크린샷, 2021-06-03 16-37-15](https://user-images.githubusercontent.com/84005711/120608986-b9680680-c48c-11eb-884a-44d965162015.png)
![스크린샷, 2021-06-03 16-40-18](https://user-images.githubusercontent.com/84005711/120608991-ba993380-c48c-11eb-8f11-449d914601a9.png)
![스크린샷, 2021-06-08 15-03-35](https://user-images.githubusercontent.com/84005711/121131444-ca3cc180-c86a-11eb-98cd-0f747519052d.png)

실행시간이 오래걸리고, object에 table이 없습니다.

 
