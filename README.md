# unRAID-Tools
A collection of tools for unRAID - Modified to work with the QNAP TS-EC2480U


# Needed Plugins: 
 - Dynamix System Temperature
 - User Scripts

## Configure System Temperature
Enter ```nct7802``` in the Available drivers: box and Click Load Drivers 

In the sensors section, you can select...

Processor temperature: ```nct7802 - CPU Temp```
Mainboard temperature: ```nct7802 - MB Temp```
Array fan speed: 2 instances of ```nct7802 - Array Fan```


## Configure User Scripts plugin
Open the User Scripts plugin and **Add New Script** called *fan_control* 
Edit the new script and paste in the contents of ```unraid_array_fan.sh```  
Change the Schedule to **Custom** and enter ```*/5 * * * *``` to run the script every 5 minutes


# Manual testing of fan control

If you have more than 1 sensor module loaded, you may need to switch ```hwmon2``` to ```hwmon3```.
Be sure to update the ```ARRAY_FAN``` in the script.

#### Read fan speed value
```cat /sys/devices/pci0000\:00//0000\:00\:1f.3/i2c-0/0-002b/hwmon/hwmon2/pwm3```

#### Change fan speed value
```echo 10 > /sys/devices/pci0000\:00//0000\:00\:1f.3/i2c-0/0-002b/hwmon/hwmon2/pwm3```

If you are unable to change the fan speed, in the BIOS, **Auto fan control** needs to be disabled
