
--------------------------------------------------------------------------------------------------------------------------------------
fdisk -l
sudo mount  /dev/nvme0n1p4 /mnt/d
mkdir /mnt/d
export DESTDIR="$HOME/Software/LocalInstall" && make -j4 install

ffmpeg -i input.mp4 -vcodec mjpeg output.mjpeg
ffmpeg -i output.mjpeg -vcodec mjpeg output.avi

ffmpeg -i output.avi -qscale 0 -ss 00:00:05.0 -t 00:00:10.0 cut.avi

ffmpeg -i  bridal_shower.mp4 -ss 00:03:02 -to 00:03:10 -acodec copy -vcodec copy  cut.mp4
wget -O deleteMeLater.tmp https://www.youtube.com/watch?v=wQcchdeS4QY
cat deleteMeLater.tmp | grep fullscreenUrl
wget -O rickroll.flv 'http://www.youtube.com/get_video?video_id=eBGIQ7ZuuiU&l=210&sk=QHSGy-6-eiJ6h5qtrj1kR2OJanvL6tLlC&fmt_map=&t=OEgsToPDskIjlCX_1shTRBRDv2UQzVb-&hl=en&plid=AAROOIUyvpMFnjvzAAAAoARsYAg&tk=6J3d54cPnMJP7mUN2BtMkd2OmbgxTvB_GPcrV3ckGUbzd7KVMiH1kA%3D%3D&title=Rick Roll'

ffmpeg  Nirvana2.mp4 -ss 00:09:10 -t 00:10:10 nirvana/nirvana_%d.png
ffmpeg -i This_is_Happy.mp4 Happy/This_is_Happy_%d.png
 git stash save -p "my commit message"

find /path/to/files -type f -exec sed -i 's/oldstring/new string/g' {} \;
(frame|ipuProcess.cpp:752)

git revert --strategy resolve <commit>
adb shell pidof com.huawei.videoanalysisengine


// show processes
pstree
ps -Ae

//remote port forwarding
ssh -NfL 6006:localhost:6006 username@remote_server_address


dpkg-query --list 'pattern*' lists all packages that have not been purged
dpkg-query --search 'pattern*' searches for individual files installed
sudo dpkg -S wine
sudo dpkg -r --force-depends libwine-development:i386
sudo apt-get --purge remove wine-mono0.0.8
sudo dpkg -r --force-depends  wine64-development


sudo apt-get update
sudo apt-get autoclean
sudo apt-get clean
sudo apt-get autoremove //apt-get -s autoremove to do a simulated dry
---------------------------shared_library----------------------------
readelf -d $executable | grep 'NEEDED'
readelf -d /lib/libOpenCL.so | grep 'NEEDED'
ldd /path/executable

----------------------------Windows-----------------------------
 netstat -ano|grep 8888
 taskkill /f /im 24536
reptyr pid


lsb_release -a 


 pip3 install tensorflow-gpu==2.0.0-beta1 --index-url=http://pypi.python.org/simple/ --trusted-host pypi.python.org
 
 "taskset -c 0 python my_program.py" will limit my_program.py to CPU:0.



------------------------.ssh file permision--------------------------
stat -c "%a" .ssh
700 for .ssh
644 for .pub
600 for id_rsa
600 authorized_keys // copy local .pub file into authorized_keys
755 for config
git multiple keys
https://docs.gitlab.com/ee/ssh/

###########---apt-key #####################

# Remove it from sources.list.

# If it was added by add-apt-repository then you will find it in its own file in /etc/apt/sources.list.d, not in the main sources.list.

sudo rm /etc/apt/sources.list.d/nemh-systemback-precise.list
Optional: Stop trusting the key

# Use apt-key list to list trusted keys. Look for an entry like "Launchpad PPA for Kendek" in this case. Then use apt-key del to delete it:

sudo apt-key del 73C62A1B