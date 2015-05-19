### Remove Unity Multitouch Gestures

Using Unity in Ubuntu 15.04 on a MacBookPro Mid 2010 will send you over the edge when the multitouch gestures trigger at unexpected times. This patch, based on this[1] answer, disables this functionality.

This has only been tested on my local machine (Macbook 6,2 running Ubuntu 15.04 and unity-7.3.2+15.04.20150420). Your mileage may vary.

    sudo apt-get build-dep unity
    mkdir -p /tmp/unity
    cd /tmp/unity
    apt-get source unity
    cd unity-7.3.2+15.04.20150420/plugins/unityshell/src/
    git clone https://github.com/gavinlaking/disable_unity_multitouch_macbook.git
    cd /tmp/unity/unity-7.3.2+15.04.20150420/
    dpkg-buildpackage -us -uc -nc
    cd ..
    sudo dpkg -i *deb
    sudo apt-get -f install
    sudo apt-get autoremove

Optionally, you can prevent unity from updating in future (may be harmful), see here[2].

    echo "unity hold" | sudo dpkg --set-selections


[1] http://askubuntu.com/questions/57586/how-can-i-disable-arbitrary-default-multitouch-gestures-in-unity

[2] http://ineed.coffee/1068/os-x-like-multitouch-gestures-for-macbook-pro-running-ubuntu-12-10/


### Notes

The build-dependencies for unity were around 250MiB of installation. Editing the correct file took moments, whilst compilation was around 20-25 minutes.

This Github repository is in no way affiliated with Canonical, or the developers of the `unity` package and is intended only to alleviate frustration caused by software developers who hard-code settings in their software which should quite clearly be configurable. This repository is not suitable for pets or small children. It will not cause scurvy, but any other side-effects are completely unpredictable. May lead to future OSS contributions.

