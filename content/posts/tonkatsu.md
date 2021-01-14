---
title: "Tongatsu Recepie"
date: 2021-01-14
tags: ['blogs', 'data wrangling']
draft: true
---


# Ingredients

Below are all materials you will need to prepare the soup.

## Broth
| Ingredient   | Quantity |  Units |
|--------------|---|--------|
| Pig trotters | 3 | lbs    |
| Green onion  | 1 | bunch  |
| Yellow onion | 1 |        |
| Shallot      | 2 |        |
| Knob ginger  | 2 | inches |

## Chashu (Braised pork belly)

| Ingredient   | Quantity |  Units |
|--------------|-----|--------|
| Pork belly   | 2   | lbs    |
| Soy sauce    | 1/2 | cup    |
| Mirin        | 3/4 | cup    |
| Sake         | 1   | cup    |
| Ginger knob  | 2   | inches |
| Green onion  | 1   | bunch  |
| Glove garlic | 5   | cloves |

## Tare

| Ingredient   | Quantity |  Units |
|--------------------------|-----|--------|
| Bonito flakes            | 1/2 | Cup    |
| Kombu                    | 3   | Pieces |
| Soy sauce                | 3/4 | Cup    |
| Dried shiitake mushrooms | 1/4 | Cup    |
| Chashu braising liquid   | 1/4 | Cup    |



## Electronics (Optional)

| Ingredient   | Quantity |
|---------------------------------------|---|
| Raspberry Pi                          | 1 |
| DS18B20 Temperature Sensor Module Kit | 1 |

# Protocol

## Prepare electronics

https://www.circuitbasics.com/raspberry-pi-ds18b20-temperature-sensor-tutorial/
```
sudo nano /boot/config.txt
dtoverlay=w1-gpio
sudo reboot
sudo modprobe w1-gpio
sudo modprobe w1-therm
cd /sys/bus/w1/devices
ls  # assuming connected
cat w1_slave  # raw temp reading
```

reading the temperature

```
import os
import glob
import time
 
os.system('modprobe w1-gpio')
os.system('modprobe w1-therm')
 
base_dir = '/sys/bus/w1/devices/'
device_folder = glob.glob(base_dir + '28*')[0]
device_file = device_folder + '/w1_slave'
 
def read_temp_raw():
    f = open(device_file, 'r')
    lines = f.readlines()
    f.close()
    return lines
 
def read_temp():
    lines = read_temp_raw()
    while lines[0].strip()[-3:] != 'YES':
        time.sleep(0.2)
        lines = read_temp_raw()
    equals_pos = lines[1].find('t=')
    if equals_pos != -1:
        temp_string = lines[1][equals_pos+2:]
        temp_c = float(temp_string) / 1000.0
        temp_f = temp_c * 9.0 / 5.0 + 32.0
        return temp_c, temp_f
	
while True:
	print(read_temp())	
	time.sleep(1)
```

## Prepare broth

1. Add `3lbs trotters` to large pot. Cover with 2 inches of water and bring to a
rolling boil for 10 minutes. Remove any residue that floats to the top with a
spoon or mesh strainer.
2. Empty `3lbs trotters` and water into a strainer and rinse to clean.
3. Place trotters back into the large pot and cover with 3 inches of water.
4. Cut `1 bunch green onion` into fourths and add to large pot.
5. Cut `2 shallots` into fourths, leaving skins on, and add to pot.
6. Cut `1 yellow onion` into fourths and add to the pot.
7. Peel `2 2 inch knobs ginger`, slice and add to pot.
8. Peel `5 cloves garlic` and add to pot. 
9. Bring water in large part to a rolling boil. Minimize temperature while
still maintaining a low boil. This will be maintained for **12 hours**. 
Stir pot around once an hour. Additionally, add water to restore original
level whenever half of the water had been lost.

## Add electronics

Since it is critical the low boil is maintained it is widely accepted that
you should electronically monitor the temperature and water level of your
broth. 

## Prepare chashu





