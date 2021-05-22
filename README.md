https://github.com/anhpt0135/CNC/compare/master...develop


**pin map:**
To control each step motor, we just need two pin: step pin (also called en pin) and dir pin:

  #define STEP_PORT       PORTD
  #define X_STEP_BIT      2  // Uno Digital Pin 2
  #define Y_STEP_BIT      3  // Uno Digital Pin 3
  #define Z_STEP_BIT      4  // Uno Digital Pin 4

  #define DIRECTION_PORT    PORTD
  #define X_DIRECTION_BIT   5  // Uno Digital Pin 5
  #define Y_DIRECTION_BIT   6  // Uno Digital Pin 6
  #define Z_DIRECTION_BIT   7  // Uno Digital Pin 7
  

To control the extruder, we use PORTB:

#define SPINDLE_ENABLE_PORT   PORTB
#define SPINDLE_ENABLE_BIT    4  // Uno Digital Pin 12

#define SPINDLE_DIRECTION_PORT  PORTB
#define SPINDLE_DIRECTION_BIT   5  // Uno Digital Pin 13 (NOTE: D13 can't be pulled-high input due to LED.)

// Define stepper driver enable/disable output pin. (ACTIVE LOW TO ENABLE STEP DRIVER)
  #define STEPPERS_DISABLE_DDR    DDRB
  #define STEPPERS_DISABLE_PORT   PORTB
  #define STEPPERS_DISABLE_BIT    0  // Uno Digital Pin 8
  #define STEPPERS_DISABLE_MASK   (1<<STEPPERS_DISABLE_BIT)
  
  ISR1 --> Set Outbit
  ISR0 --> reset Outbit
  
 F: Feet rate  (mm/min)
 S: Spindle speed (rpm) --> gc_block.value.s --> gc_state.spindle_speed --> 
 Spindle state:
 
 M3: SPINDLE_ENABLE_CW  --> gc_state.modal.spindle --> _spindle_set_state(state); spindle_get_state().
 M4: SPINDLE_ENABLE_CCW
 M5: SPINDLE_DISABLE
 
 Calculate number of step/mm for extruder from sys.extruder_speed --> ISR1 and ISR0
 
 
 
 