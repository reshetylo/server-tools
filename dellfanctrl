#!/bin/bash

# This is Dell R510 FAN control script. Should be compatible with R710 and others with DRAC 6
# IMPI commands used:
# ipmitool raw 0x30 0x30 0x01 0x00 # Disable system FAN control
# ipmitool raw 0x30 0x30 0x02 0xff 0x08 # Set FAN speed in percents
# ipmitool raw 0x30 0x30 0x01 0x01 # Enable system FAN control
# tested on FreeBSD 11.1 (FreeNAS) using `root` user

echo "Dell R510 FAN control script v1.0"

usage_example() {
        echo "Example usage:"
        echo -e "Enable automatic FAN control:\t\t$0 auto"
        echo -e "Disable automatic FAN control:\t\t$0 manual"
        echo -e "Disable & set speed to N percents:\t$0 set 10"
}

runthis() {
        echo "Running: $1"
        $1
        EXIT_CODE=$?
        if [ $EXIT_CODE == 0 ]; then
                echo "Command executed successfully"
        else
                echo "Execution failed with status $EXIT_CODE"
        fi
}

if [ $# == 0 ]; then
        echo -e "There is not enough parameters for this script!\n"
        usage_example
else
        if [ $1 == "auto" ]; then
                runthis "ipmitool raw 0x30 0x30 0x01 0x01"
        elif [ $1 == "manual" ]; then
                runthis "ipmitool raw 0x30 0x30 0x01 0x00"
        elif [ $1 == "set" ]; then
                SET_SPEED=15
                if [ $2 -gt 0 ] && [ $2 -le 100 ]; then
                        SET_SPEED=`printf "%x\n" $2`
                else
                        echo "Entered number is not in the range [1..100]: $2"
                        exit
                fi
                if [ `echo $SET_SPEED | wc -c` -eq 2 ]; then
                        SET_SPEED=0$SET_SPEED
                fi
                echo "Setting FAN speed to $2%"
                runthis "ipmitool raw 0x30 0x30 0x02 0xff 0x$SET_SPEED"
        elif [ $1 == "status" ]; then
                echo "Current system status:"
                ipmitool sensor | grep -iE "fan|temp" | awk -F"|" '{if($2!~"na"){print $1$2}}'
        else
                echo "Unknown parameter!"
                usage_example
        fi
fi
