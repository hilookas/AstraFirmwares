夹爪零位设置:
夹爪开合0-120mm
合并夹爪
设置中点
(0.06/0.027)/2/pi*4096=1448
2048-1448=600
移动到600位置
设置中点
合并夹爪，此时
应该位置为3496

设0命令：
回到0点（多发几次） 5A 02 08 00 08 00 08 00 08 00 08 00 08 00 00 00 00 00
设置0点 5A 04 80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

odrive_config:
```python
# Ref: https://blog.csdn.net/gjy_skyblue/article/details/115412902
# Ref: https://docs.odriverobotics.com/v/0.5.4/hoverboard.html#hoverboard-doc
# Ref: https://docs.odriverobotics.com/v/0.5.6/encoders.html
# Ref: https://blog.csdn.net/gjy_skyblue/article/details/118159153
# Ref: https://docs.odriverobotics.com/v/0.5.6/getting-started.html
# Ref: https://docs.odriverobotics.com/v/0.5.6/control.html
# Ref: https://things-in-motion.blogspot.com/2018/12/how-to-select-right-power-source-for.html

odrv0.erase_configuration() # with reboot

# 放宽保护条件
odrv0.config.dc_max_negative_current = -5.0 # 反向电流
odrv0.axis0.motor.config.current_lim = 20

# 设置电机极对数和霍尔编码器
odrv0.axis0.motor.config.pole_pairs = 10 # 电机极对数
odrv0.axis0.encoder.config.mode = ENCODER_MODE_HALL # 使用ABC(UVW)霍尔模式
odrv0.axis0.encoder.config.cpr = 60 # 电机一圈脉冲数（6 * 极对数）
odrv0.axis0.encoder.config.bandwidth = 100

odrv0.axis0.motor.config.resistance_calib_max_voltage = 5 # 电机校准时的电压
odrv0.axis0.encoder.config.calib_range = 0.1 # 放宽编码器标定范围
odrv0.axis0.encoder.config.calib_scan_distance = 150
odrv0.axis0.motor.config.current_control_bandwidth = 100

# ignore illegal_hall_state error
odrv0.axis0.encoder.config.ignore_illegal_hall_state = True

# 放宽保护条件
odrv0.axis1.motor.config.current_lim = 20

# 设置电机极对数和霍尔编码器
odrv0.axis1.motor.config.pole_pairs = 10 # 电机极对数
odrv0.axis1.encoder.config.mode = ENCODER_MODE_HALL # 使用ABC(UVW)霍尔模式
odrv0.axis1.encoder.config.cpr = 60 # 电机一圈脉冲数（6 * 极对数）
odrv0.axis1.encoder.config.bandwidth = 100

odrv0.axis1.motor.config.resistance_calib_max_voltage = 5 # 电机校准时的电压
odrv0.axis1.encoder.config.calib_range = 0.1 # 放宽编码器标定范围
odrv0.axis1.encoder.config.calib_scan_distance = 150
odrv0.axis1.motor.config.current_control_bandwidth = 100

# ignore illegal_hall_state error
odrv0.axis1.encoder.config.ignore_illegal_hall_state = True

# sleep(1)

odrv0.save_configuration()
odrv0.reboot()








# 编码器标定
odrv0.axis0.requested_state = AXIS_STATE_FULL_CALIBRATION_SEQUENCE # 开始标定

# wait until motor stop

odrv0.axis0.encoder.config.pre_calibrated = True
odrv0.axis0.motor.config.pre_calibrated = True

# sleep(1)

odrv0.save_configuration()
odrv0.reboot()



# 编码器标定
odrv0.axis1.requested_state = AXIS_STATE_FULL_CALIBRATION_SEQUENCE # 开始标定

# wait until motor stop

odrv0.axis1.encoder.config.pre_calibrated = True
odrv0.axis1.motor.config.pre_calibrated = True

# sleep(1)

odrv0.save_configuration()
odrv0.reboot()

















# 位置模式 + 调参
odrv0.axis0.controller.config.control_mode = CONTROL_MODE_POSITION_CONTROL
odrv0.axis0.controller.config.pos_gain = 20
odrv0.axis0.controller.config.vel_gain = 0.10
odrv0.axis0.controller.config.vel_integrator_gain = 0

# 位置模式 + 调参
odrv0.axis1.controller.config.control_mode = CONTROL_MODE_POSITION_CONTROL
odrv0.axis1.controller.config.pos_gain = 20
odrv0.axis1.controller.config.vel_gain = 0.10
odrv0.axis1.controller.config.vel_integrator_gain = 0

# 梯形加减速
odrv0.axis0.controller.config.input_mode = INPUT_MODE_TRAP_TRAJ
odrv0.axis0.controller.config.vel_limit = 20
odrv0.axis0.trap_traj.config.vel_limit = 20
odrv0.axis0.trap_traj.config.accel_limit = 1
odrv0.axis0.trap_traj.config.decel_limit = 1

# 梯形加减速
odrv0.axis1.controller.config.input_mode = INPUT_MODE_TRAP_TRAJ
odrv0.axis1.controller.config.vel_limit = 20
odrv0.axis1.trap_traj.config.vel_limit = 20
odrv0.axis1.trap_traj.config.accel_limit = 1
odrv0.axis1.trap_traj.config.decel_limit = 1

# # 开启闭环控制
# odrv0.axis0.requested_state = AXIS_STATE_CLOSED_LOOP_CONTROL
# odrv0.axis0.config.startup_closed_loop_control = True

# # 测试
# odrv0.axis0.controller.input_pos = 5

# # 开启闭环控制
# odrv0.axis1.requested_state = AXIS_STATE_CLOSED_LOOP_CONTROL
# odrv0.axis1.config.startup_closed_loop_control = True

# # 测试
# odrv0.axis1.controller.input_pos = 0

# sleep(1)

odrv0.save_configuration()
odrv0.reboot()











# for any errors
dump_errors(odrv0)
odrv0.clear_errors()

```