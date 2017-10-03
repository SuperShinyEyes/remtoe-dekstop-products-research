```bash
ssh seyoung@130.233.195.77

loginctl unlock-sessions

# For a single TigerVNC session
ssh -L 5901:127.0.0.1:5901 -N -f -l seyoung 130.233.195.77

# For NoMachine free NX connection
ssh -L 4000:localhost:4000 -N -f -l seyoung 130.233.195.77
ps -ef | grep ssh

ssh git@admin.cs.hut.fi


```
