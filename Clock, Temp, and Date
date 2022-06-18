####################Import all the libraries#######################
from machine import I2C, Pin
from ds1302 import DS1302
from pico_i2c_lcd import I2cLcd
from neopixel import Neopixel
import time
###################################################################


################Setup LCD I2C and initialize#######################
I2C_ADDR     = 39
I2C_NUM_ROWS = 2
I2C_NUM_COLS = 16

i2c = I2C(0, sda=machine.Pin(0), scl=machine.Pin(1), freq=400000)
lcd = I2cLcd(i2c, I2C_ADDR, I2C_NUM_ROWS, I2C_NUM_COLS)
###################################################################


################Setup DS1302 and initialize###########################
ds = DS1302(Pin(18),Pin(17),Pin(16))

ds.date_time() # returns the current datetime.

#ds.date_time([2022,6, 16, 0, 10, 30, 40, 0]) # set datetime.

#ds.hour() # returns hour.
#print(ds.date_time())
###################################################################


#################Buttons#############################################
Button_pins = [6,7,8,9]

Button = []
# Loop to assign GPIO pins and setup input and outputs
for x in range(0,4):

    Button.append(Pin(Button_pins[x], Pin.IN, Pin.PULL_DOWN))
    Button[x].value(0)
######################################################################


######################### Time #################################
while True:
    (Y,M,D,day,hr,m,s)=ds.date_time()
    if s < 10:
        s = "0" + str(s)
    if m < 10:
        m = "0" + str(m)
    if hr < 10:
        hr = "0" + str(hr)
    if D < 10:
        D = "0" + str(D)
    if M < 10:
        M = "0" + str(M)
        
    lcd.move_to(0,0)
    lcd.putstr("Time:")
    lcd.move_to(6,0)
    lcd.putstr(str(hr) + ":" + str(m))
#################### button press to add date ###################################
    if Button[0].value() != 0:
     
        
        lcd.move_to(0,1)
        lcd.putstr("Date:")
        lcd.move_to(6,1)
        lcd.putstr(str(M) + "/" + str(D) + "/" + str(Y)+"  ")
        time.sleep(30)
        lcd.clear()
    
############### Temperature ########################################    
    sensor_temp = machine.ADC(4)
    conversion_factor = 3.3 / (65535)    
    reading = sensor_temp.read_u16() * conversion_factor
    temperature = ((27 - (reading - 0.706)/0.001721)*(9/5))+32
    
    rounded_temperature = round(temperature)
    print(rounded_temperature)
    lcd.move_to(0,1)
    lcd.putstr('Temp:')
    lcd.move_to(6,1)
    lcd.putstr(str(rounded_temperature))
    
    
    
    a=65
    b=70
    c=75
    
    lcd.move_to(9,1)
    if a>temperature:
        lcd.putstr("Chilly!")
    lcd.move_to(9,1)
    if a<=temperature<b:
        lcd.putstr("Nice :)")
    lcd.move_to(9,1)
    if b<=temperature<c:
        lcd.putstr("Okay :/")
    lcd.move_to(9,1)
    if c<=temperature:
        lcd.putstr("HOT!!! ")
    time.sleep(.5)
    
########################################################  
    
            
        
       

