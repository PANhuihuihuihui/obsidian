
### 配置
本文通过systemctl来管理Clash的进程，对应`clash.service`文件，通过两个脚本`start-clash.sh`和`stop-clash.sh`来管理Clash的启停，具体配置如下。
```bash
# edit and save this file to /usr/lib/systemd/system/clash.service
[Unit]

Description=clash

After=network.target

[Service]

WorkingDirectory="your home directory"/.config/clash

ExecStart="your home directory"/.config/clash/start-clash.sh

ExecStop="your home directory"/.config/clash/stop-clash.sh

Environment="HOME=your home directory"

Environment="CLASH_URL=your subscribe address"

[Install]

WantedBy=multi-user.target
```

----
```bash
#!/bin/bash

# save this file to ${HOME}/.config/clash/start-clash.sh

# save pid file

echo $$ > ${HOME}/.config/clash/clash.pid

diff ${HOME}/.config/clash/config.yaml <(curl -s ${CLASH_URL})

if [ "$?" == 0 ]

then

/usr/bin/clash

else

TIME=`date '+%Y-%m-%d %H:%M:%S'`

cp ${HOME}/.config/clash/config.yaml "${HOME}/.config/clash/config.yaml.bak${TIME}"

curl -L -o ${HOME}/.config/clash/config.yaml ${CLASH_URL}

/usr/bin/clash

fi
```

----
```bash
#!/bin/bash

# save this file to ${HOME}/.config/clash/stop-clash.sh

# read pid file

PID=`cat ${HOME}/.config/clash/clash.pid`

kill -9 ${PID}

rm ${HOME}/.config/clash/clash.pid
```

----
配置添加完成后，执行以下代码就可以启动Clash并设置为开机自启动。
```bash
systemctl enable clash
systemctl start clash
```
