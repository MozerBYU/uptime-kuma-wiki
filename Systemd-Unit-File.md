Aside from the provided pm2 instructions. You can also use systemd to enable and run Uptime-Kuma at system startup more easily.

Place the following file in /etc/systemd/system/, or under whatever service your prefer and name it uptime.service.

```ini
[Unit]
Description=Uptime-Kuma - A free and open source uptime monitoring solution
Documentation=https://github.com/louislam/uptime-kuma
After=network.target

[Service]
Type=simple

WorkingDirectory=/opt/uptime-kuma

ReadWriteDirectories=/opt/uptime-kuma /var/log

ExecStart=/usr/bin/npm run start-server
ExecStop=/usr/bin/npm run stop-server

Restart=on-failure
. 
[Install]
WantedBy=multi-user.target
```

Note: This unit file assumes that you are running the software under root privileges. These are necessary in order to use the socket capabilities of the linux kernel. 

If you have node/npm installed in a different path, you will need to alter the ExecStart line to match this.

Once installed, issue the following commands to reload systemd unit files, enable it to start on boot, and start it immediately:

```sh
systemctl daemon-reload
systemctl start uptime
systemctl enable uptime
```
