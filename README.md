# gnss_launch

## 実機でのGNSSの使用方法
### パッケージのクローン・ビルド
```
mkdir -p ~/gnss_ws/src
cd ~/gnss_ws/src
git clone git@github.com:makotoyoshigoe/gnss_launch.git
cd ../ && colcon build --symlink-install
source install/setup.bash
```
### ubloxパッケージのインストール
```
sudo apt update
sudo apt install -y ros-$ROS_DISTRO-ublox
```
### launchファイルの起動
```
sudo chmod 666 /dev/ttyACM0
ros2 launch gnss_launch ublox_gps_node-zed_f9r.launch.py
```

## RTK測位の方法
### RTKLIBのインストール
```
sudo apt update
sudo apt install -y rtklib
```
### 基準局の決定
[こちらのサイト](https://rtk.silentsystem.jp/)を参考に決定（例として千葉県山武郡横芝光町のものを使用）\
例：千葉県山武郡横芝光町
| サーバアドレス | ポート番号 | MountPoint | ID | Passward | 
| -- | -- | -- | -- | -- |
| ntrip1.bizstation.jp | 2101 | 0C06E596 | なし | なし |

### WiFiへの接続
GNSSと接続している機器をWiFiに接続してください。

### RTK測位の実行
コマンドラインで
```str2str -in ntrip://ID:Passward@サーバアドレス:ポート番号/MountPoint#rtcm3 -out serial://ttyACM0:115200```
を実行

上の例で実行する場合
```
str2str -in ntrip://:@ntrip1.bizstation.jp:2101/0C06E596#rtcm3 -out serial://ttyACM0:115200
```