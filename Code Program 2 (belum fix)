from controller import Robot
robot = Robot()
timestep = int(robot.getBasicTimeStep())

phase = 2

count = 2

def run_robot(robot):
    time_step = 16
    max_speed = 5

leftmotor = robot.getDevice('motor_1')
rightmotor = robot.getDevice('motor_2')
leftmotor.setPosition(float('inf'))
rightmotor.setPosition(float('inf'))

dsleft= robot.getDevice('ds_left')
dsright = robot.getDevice('ds_right')
dsfront = robot.getDevice('ds_front')
irl2 = robot.getDevice('IRL2')
irl1 = robot.getDevice('IRL1')
ircl = robot.getDevice('IRCL')
ircr = robot.getDevice('IRCR')
irr1 = robot.getDevice('IRR1')
irr2 = robot.getDevice('IRR2')

irl2.enable(timestep)
irl1.enable(timestep)
ircl.enable(timestep)
ircr.enable(timestep)
irr1.enable(timestep)
irr2.enable(timestep)
dsleft.enable(timestep)
dsright.enable(timestep)
dsfront.enable(timestep)
   
def forward():
    rightmotor.setVelocity(4.5)
    leftmotor.setVelocity(4.5)
def turn_left():
    rightmotor.setVelocity(4)
    leftmotor.setVelocity(-4)
def turn_right():
    rightmotor.setVelocity(-4)
    leftmotor.setVelocity(4)
def stop():
    rightmotor.setVelocity(0)
    leftmotor.setVelocity(0)

def start_phase(): #sebelum tembok
    if ir_right > 1400 and ir_left <1400:
        turn_left()
    elif liner < 1200:
        forward()
    elif ir_right < 1400 and ir_left > 1400:
        turn_right()
    elif line_left < 500:
        stop()
        turn_left()

def wall():
    if(ir_right > 600 and ir_left >600 and ds_right < 840) or (ir_right > 600 and ir_left >600 and ds_left < 1000):
       #tembok
       forward()

def afterwall_phase():
    if ir_right > 1400 and ir_left <1400:
        turn_left()
    #elif garis < 1200:
        #maju()
    elif ir_right < 1400 and ir_left > 1400:
        turn_right()
    elif line_right < 500:
        turn_right()
    elif ds_front > 200:
        forward()
    elif ds_front < 200:
        stop()
    else:
        forward()

def gate():
    if line_right < 500 and line_right > 600: ###s s
        turn_right()
    elif line_right < 500 and line_right > 350 and mid_line > 600 and line_left <600:
        forward()
    elif ds_front < 200:
        stop()
    #elif line_kanan < 350 and line_kiri < 350:
        #if ds_depan < 200:
            #berhenti()
        #else: 
            #maju()

while robot.step(timestep) != -1:  
    rightmotor.setVelocity(5)
    leftmotor.setVelocity(5)

    irl2_val = irl2.getValue()
    irl1_val = irl1.getValue()
    ircl_val = ircl.getValue()
    ircr_val = ircr.getValue()
    irr1_val = irr1.getValue()
    irr2_val = irr2.getValue()
    ds_left = dsleft.getValue()
    ds_right = dsright.getValue()
    ds_front = dsfront.getValue()
    
    line_right = irr1_val + irr2_val #nn
    line_left = irl1_val + irl2_val
    ir_right = ircr_val + irr1_val + irr2_val # irkanan n
    ir_left = ircl_val + irl1_val + irl2_val
    mid_line = ircr_val + ircl_val #gt
    liner = ir_right + ir_left #g
    
    
    print('dsR:{:.2f},||lineL:{:.2f},||irR: {:.2f},||irL:{:.2f},||g_t: {:.2f},|| garis:{:.2f} '.format(ds_right, line_left, ir_right, ir_left, mid_line, liner))
    
    if phase == 2:
        start_phase()
        wall()
        if liner < 3000 and ds_left <1000:
            phase =3
    elif phase == 3:
        afterwall_phase()
        if ds_right <900:
            phase = 4 #++
    elif phase == 4:
        gate()
        if count > 1 and line_right <280 and line_left <280:
            forward()
            count =+1
            if count == 5:
                stop()
                break
