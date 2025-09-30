# Bash

- `ctrl + r` Search previous commands
- `ctrl + a` Move cursor to front of command

## SSH

- `ssh -L <local-port>:<remote-port> remote.machine` SSH remote.machine with port forwarding
  - `ssh -L 3000:localhost:3000 mymachine.domain.etc` 

### SSH Config

```
# ~/.ssh/config

Host myMachine
    Host mymachine.domain.etc
    User myUsername
    LocalForward 3000 localhost:3000

Host myOtherMachine
    Host myothermachine.domain.etc
    User myUsername
    LocalForward 8000 localhost:8000
```
