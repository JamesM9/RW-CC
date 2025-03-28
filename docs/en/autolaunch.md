Software autorun
===

> **Note** In the image version **0.20** `droid` package and service was renamed to `droid`. See [previous version of the article](https://github.com/CopterExpress/droid/blob/v0.19/docs/en/autolaunch.md) for older images.

systemd
---

Main documentation: https://wiki.archlinux.org/title/Systemd.

All automatically started droid software is launched as a `droid.service` systemd service.

The service may be restarted by the `systemctl` command:

```(bash)
sudo systemctl restart droid
```

Text output of the software can be viewed using the `journalctl` command:

```(bash)
journalctl -u droid
```

To run droid software directly in the current console session, you can use the `roslaunch` command:

```(bash)
sudo systemctl restart droid
roslaunch droid droid.launch
```

You can disable droid software autolaunch using the `disable` command:

```(bash)
sudo systemctl disable droid
```

roslaunch
---

Main documentation: http://wiki.ros.org/roslaunch.

The list of nodes / programs declared for running is specified in file `/home/pi/catkin_ws/src/droid/droid/launch/droid.launch`.

You can add your own node to the list of automatically launched ones. To do this, place your executable file (e.g. `my_program.py`) into folder `/home/pi/catkin_ws/src/droid/droid`. Then add the start of your node to `droid.launch`, for example:

```xml
<node name="my_program" pkg="droid" type="my_program.py" output="screen"/>
```

The started file must have *permission* to run:

```bash
chmod +x my_program.py
```

When scripting languages are used, a <a href="https://en.wikipedia.org/wiki/Shebang_(Unix)">shebang</a> should be placed at the beginning of the file, for example:

```bash
#!/usr/bin/env python3
```
