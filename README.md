# Cse-project
from gpiozero import Robot, LineSensor
from time import sleep

prototype = Robot(left=(7, 8), right=(9, 10))
left_sensor1 = LineSensor(17)
right_sensor1= LineSensor(27)

velocity = 0.65

def motor_speed():
    while True:
        left_detector  = int(left_sensor1.value)
        right_detector = int(right_sensor1.value)
        ## Stage 1 begins
        if left_detector == 0 and right_detector == 0:
            left_motor = 1
            right_motor = 1
        ## Stage 2 begins
        if left_detector == 0 and right_detector == 1:
            left_motor = -1
        if left_detector == 1 and right_detector == 0:
            right_motor = -1
        #PRINT(r, l)
        yield (right_motor * velocity, left_motor * velocity)

prototype.source = motor_speed()

sleep(60)
prototype.stop()
prototype.source = None
prototype.close()
left_sensor.close()
right_sensor.close()
