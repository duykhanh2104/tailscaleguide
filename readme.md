#### download
curl -fsSL https://tailscale.com/install.sh | sh

### start service
sudo tailscale up

### authen 
To authenticate, visit:

        https://login.tailscale.com/a/xxxxxx

### check status
tailscale status

### install python
sudo dnf install -y git python3-pip

### install websockify
pip3 install websockify

### clone novnc
git clone https://github.com/novnc/noVNC.git ~/noVNC

### set ip target pc that need to remote:
websockify --web=$HOME/noVNC 6080 100.x.x.x:5900 


### for more secure:
#### create key under noVNC folder:
openssl req -x509 -nodes -newkey rsa:2048 \
  -keyout ~/novnc.key \
  -out ./novnc.crt \
  -days 365 \
  -subj "/CN=novnc"

#### run noVNC web:
websockify --web=$HOME/noVNC   --cert=$HOME/noVNC/novnc.crt   --key=$HOME/noVNC/novnc.key   6080 100.x.x.x:5900
