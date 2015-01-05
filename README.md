# Transitioning from Houm.io 1.0

Log in to your Houm.io bridge.

Upgrade your supervisord, let the installer overwrite your supervisor.conf:

    echo "deb http://http.debian.net/debian wheezy-backports main" | sudo tee -a /etc/apt/sources.list
    sudo apt-get update
    sudo apt-get -t wheezy-backports install "supervisor"

Replace your `/etc/supervisor/supervisord.conf` with [this](supervisord.conf).

Add [houmio.conf](houmio.conf) to `/home/pi`.

Replace `HOUMIO_SITEKEY` dummy value with your siteKey.

Install `houmio-bridge` and `houmio-driver-enocean`:

    npm install houmio/houmio-bridge
    npm install houmio/houmio-driver-enocean

Restart supervisor:

    sudo service supervisor restart
