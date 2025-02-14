# my-projfrom machine import Pin
from gpio_lcd import GpioLcd
import time

# Initialize LCD
lcd = GpioLcd(
    rs_pin=Pin(16),
    enable_pin=Pin(17),
    d4_pin=Pin(18),
    d5_pin=Pin(19),
    d6_pin=Pin(20),
    d7_pin=Pin(21),
    num_lines=2,
    num_columns=16 )

# Vote counters
j = 0  # BJP Votes
k = 0  # AAP Votes
p = 0  # CON Votes

button = Pin(0, Pin.IN, Pin.PULL_DOWN)
button_green = Pin(1, Pin.IN, Pin.PULL_DOWN)
button_blue = Pin(2, Pin.IN, Pin.PULL_DOWN)

lcd.putstr("BJP   AAP    CON")

time.sleep(1)  # Allow LCD to initialize properly
lcd.move_to(0, 1)
lcd.putstr("0     0      0")

while True:
    if button.value() == 1:  # BJP Vote
        j += 1
        lcd.move_to(0, 1)
        lcd.putstr("   ")  # Clear previous number
        lcd.move_to(0, 1)
        lcd.putstr(str(j))
        print(f"BJP Votes: {j}")
        time.sleep(0.2)  # Debounce delay

    if button_green.value() == 1:  # AAP Vote
        k += 1
        lcd.move_to(6, 1)
        lcd.putstr("   ")
        lcd.move_to(6, 1)
        lcd.putstr(str(k))
        print(f"AAP Votes: {k}")
        time.sleep(0.2)

    if button_blue.value() == 1:  # CON Vote
        p += 1
        lcd.move_to(13, 1)
        lcd.putstr("   ")
        lcd.move_to(13, 1)
        lcd.putstr(str(p))
        print(f"CON Votes: {p}")
        time.sleep(0.2)
