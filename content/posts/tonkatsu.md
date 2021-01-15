---
title: "Tonkotsu Recipe"
date: 2021-01-14
tags: ['cooking']
draft: false
---

This recipe (aside from the electronics) is derived from Joshua Weissman's
video, [How to Make Real Tonkotsu Ramen](https://www.youtube.com/watch?v=uPqzY8rZLZM&t=312s).

# Ingredients

Below are all materials you will need to prepare the soup.

## Broth / soup
| Ingredient   | Quantity |  Units |
|--------------|---|--------|
| Pig trotters | 3 | lbs    |
| Green onion  | 1 | bunch  |
| Yellow onion | 1 |        |
| Shallot      | 2 |        |
| Knob ginger  | 2 | inches |
| Ramen noodles  | 1 | package |

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
| Bonito flakes            | 1/2 | cup    |
| Kombu                    | 3   | pieces |
| Soy sauce                | 3/4 | cup    |
| Dried shiitake mushrooms | 1/4 | cup    |
| Chashu braising liquid   | 1/4 | cup    |



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

## Add electronics

Since it is critical the low boil is maintained it is widely accepted that
you should electronically monitor the temperature and water level of your
broth.

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

## Prepare chashu

1. Cut `1 bunch` green onion into 2 inch sections.
2. Peel `2 inch knob ginger` and slice.
3. Add `1 cup sake`, the green onion, the ginger, `3/4 cup mirin`, `1/2 cup + 2 Tablespoons soy sauce`,
four cloves of whole garlic, and `1/3` cup water to a large oven-safe pot.
4. Roll the pork belly length wise and tie with kitchen twine into three
separate segments. Place into the pot with other ingredients.
5. Bring chashu to a boil, then low boil and then cover with a lid and place
into a 300 degree oven for 3-3.5 hours. Baste every 30 mins.

## Prepare the tare

1. Add `three 2 inch peices of kombu` to a small pot. 
2. Add `3/4 cup water` to the pot.
3. Boil the water and then let kombu seep for 10 minutes. 
4. Add `1/2 cup bonito flakes` to pot and let steep for 5 minutes.
5. After the 5 minutes poor solution through a fine mesh sieve into a medium bowl.
6. Add `3/4 cup soy sauce`, `1/4 cup + 2 tablespoons mirin`, `1/4 cup chashu braising liquid` 
and `1/4 cup rehydrating liquid` used for mushrooms to medium bowl. Stir and
lightly salt. 

## Prepare toppings

This should be done within a half-hour of time to serve.

1. Finely chop the green part of a green onion.
2. Dehydrate shiitake mushrooms according to package directions.
3. Prepare ice water bath.
4. Bring small pot of water to boil. Add eggs and reduce heat to gentile bowl.
Boil eggs for 6-7 minutes then place into ice bath.

## Assembling the soup

1. Boil ramen noodles according to package directions.
2. Slice chashu into into 1/2 inch slices. If cold reheat in pan.
3. Add tare to bowl to taste.
4. Strain broth and add to bowl.
5. Add soft boiled eggs, chashu, mushrooms and sliced green onion to broth. 

Done!

# Enjoy

# Plot temperature data with R







