# homebridge-setting
Setup Homebridge to Start on Bootup

 October 14, 2016  Tim  Home Automation, How To, Raspberry Pi
I’ve recently been playing with Homebridge on my Raspberry Pi. I’ve setup my Harmony Hub and my wireless power outlets to be controlled by Siri on my iPhone. Overall it has been pretty simple to setup but I did run into an issue trying to get Homebridge to start on bootup. Homebridge suggest 3 different methods. 

I decided to use systemd to start Homebridge on bootup. I prefered this method because it will restart if an error occurs. I followed the gist setup step by step but ran into some problems.

My main issues were:

The location of my homebridge binary. Step 2 <br>
Permissions were not correct and the service failed to load. Step 7 <br>
I needed the persist folder in /var/homebridge directory. Step 6 <br>
Here are the steps that worked for me:

sudo nano /etc/default/homebridge and paste this gist  <br>
sudo nano /etc/systemd/system/homebridge.service and paste this gist <br>
I had to remove local from:  ExecStart=/usr/local/bin/homebridge $HOMEBRIDGE_OPTS  because my homebridge installed in /usr/bin/  <br>
Create a user to run service: sudo useradd --system homebridge <br>
sudo mkdir /var/homebridge <br>
sudo cp ~/.homebridge/config.json /var/homebridge/ <br>
This copies your current user’s config. This assumes you have already added accessories etc. <br>
sudo cp -r ~/.homebridge/persist /var/homebridge <br>
sudo chmod -R 0777 /var/homebridge <br>
sudo systemctl daemon-reload <br>
sudo systemctl enable homebridge <br>
sudo systemctl start homebridge <br>
Type systemctl status homebridge to check the status of the service. <br>

Hopefully this helps anyone who is having trouble with Homebridge starting on boot on a Raspberry Pi. Please comment below if you have any questions.<br>
