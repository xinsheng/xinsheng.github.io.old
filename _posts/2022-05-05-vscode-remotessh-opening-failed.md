---
layout: post
title: "vscode remotessh opening failed"
category: kb
---

By using vscode, connect to a remote CentOS server, error happens on long time connecting

```bash
Failed to connect to the remote extension host server (Error: WebSocket close with status code 1006)
```

Check the vscode log, it says:

```bash
[13:53:58.386] Failed to set up socket for dynamic port forward to remote port 39105: Socket closed. Is the remote port correct?
[13:53:58.462] [Forwarding server 64026] Got connection 1
[13:53:58.465] Failed to set up socket for dynamic port forward to remote port 39105: Socket closed. Is the remote port correct?
[13:53:58.469] > channel 3: open failed: administratively prohibited: open failed
[13:53:58.480] > channel 3: open failed: administratively prohibited: open failed
```

It means the ssh server side disabled tcp forwarding, so we could change the sshd config file `/etc/ssh/sshd_config`, remote the `#` from `#AllowTcpForwarding yes`,
save it and then restart sshd `systemctl restart sshd`

Reconnect it from vscode, it works.
