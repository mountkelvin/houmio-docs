# Request a migration

First, set your site recovery email address by editing the name of your site. Then, from this email address, send an email to help@houm.io with the subject "Request for migration from 1.0 to 2.0".

You will receive a new siteKey.

# Reconfigure

SSH to your Houm.io bridge.

Upgrade your supervisord, let the installer overwrite your supervisor.conf:

    echo "deb http://http.debian.net/debian wheezy-backports main" | sudo tee -a /etc/apt/sources.list
    sudo apt-get update
    sudo apt-get -t wheezy-backports install "supervisor"

Replace your `/etc/supervisor/supervisord.conf` with this [supervisord.conf](supervisord.conf).

Add [houmio.conf](houmio.conf) to `/home/pi`.

Replace `HOUMIO_SITEKEY` dummy value with your siteKey.

Install `houmio-bridge` and `houmio-driver-enocean`:

    cd
    npm install houmio/houmio-bridge
    npm install houmio/houmio-driver-enocean

Restart supervisor:

    sudo service supervisor restart

Your site UI is at `https://houmio-ui.herokuapp.com/site/yoursecretsitekey`.

# Additional drivers

You might want to install additional drivers:

* [KNX driver](https://github.com/houmio/houmio-driver-knx)
* [Philips Hue driver](https://github.com/houmio/houmio-driver-philips-hue)
