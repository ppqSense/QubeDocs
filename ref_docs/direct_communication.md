Direct Communication {#commands_table_chapter}
====================

#### 

The Qubes operates on the basis of a series of commands received by a
computer through the USB Serial Port. Each command is codified with a
string, to be as friendly for a user as possible, being easily readable.

#### 

The commands share the same structure, each one being composed by a
identifier and a value, separated by a colon character.

**\[identifier\]:\[value\]**

#### 

The *identifier* allows to differentiate all the available commands,
each one acting on a specific functionality of the connected Qube. The
*value* is used in association with the *identifier* to define the
operation to be carried out by the Qube (for example *activate* or
*deactivate* the modulations) or to pass numerical value to be used by
the firmware of the device for its operations (for example laser
temperature and bias current *setpoints*). The *value* parameter also
differentiates the **write** commands and the **queries**.

-   **Query:** It is possible to send queries to the Qube in order to
    receive information about its current status, read digital monitors
    and request informations about the driver. Not all the available
    **identifiers** have an associated query. In order to send queries
    to the Qube, the **value** of the command must be replaced by the
    **?** character, for example:

    **iset:?**

-   **Write commands:** Allow to send the Qube numerical values or
    commands to enable/disable some of its functionalities, for example:

    **iset:150**

Serial Port Specifications
--------------------------

#### 

The ppqSense Control Software communicates with the Qubes by the mean of
a Serial Connection. The same port can also be used by a third party
software to interact with the driver. The baud rate of the Qubes Serial
Port is 115200 bps, which has to be set on the third party software in
order for it to work with the driver. The connection of a third-party
software is only possible if the Qube Control Software is not running,
otherwise the Serial Port resources is kept busy and it is not
accessible from the third party software.

Serial Commands Specifications
------------------------------

#### 

User can find all the available commands listed in the subsequent
tables. Those commands are the ones that are available for the final
user to be integrated in a third party control software or to be used in
the Qube Control Software to directly communicate with the driver via
the dedicated form in the Advanced tab. In order for the commands to
work, they must be sent at the appropriate Baud Rate and each command
must be terminated with the **\\n** character. If a suitable *query* is
issued, the Qube replies with a string containing the requested
informations. All the strings sent as a reply to a *query* are
terminated with the **\\r\\n** characters.

List of available commands
--------------------------

::: {#\\QubeModel _cmd_table_cm}
  **Cmd**   **Value**       **R/W**   **Action**                                                                                                                 **Output Format**   **Unit**
  --------- --------------- --------- -------------------------------------------------------------------------------------------------------------------------- ------------------- ----------
                                                                                                                                                                                     
  id:       ?               R         Returns the identificative code of the instrument                                                                          -\#\#\#\#           N.A.
  ilas:     ?               R         Returns the Output Current value readed from the monitor.                                                                  \#\#\#\#.\#\#       mA
            ?               R         Returns the Current setpoint.                                                                                              \#\#\#\#.\#\#       mA
            \#\#\#\#.\#\#   W         Sets the Current setpoint.                                                                                                 N.A.                mA
            on              W         Switches the Current ON.                                                                                                   N.A.                N.A.
            off             W         Switches the Current OFF. If the modulations were active, they're also switched OFF.                                       N.A.                N.A.
            ?               R         Returns the Output Current Maximum Limit set by the user.                                                                  \#\#\#\#.\#\#       mA
            \#\#\#\#.\#\#   W         Sets the Output Current Maximum Limit.                                                                                     \#\#\#\#.\#\#       mA
  vlas:     ?               R         Returns the measured Voltage Drop across the laser                                                                         \#\#\#\#.\#\#       V
            on              W         Enables the overall Modulation Switch. This command becomes active 10 seconds after. the use of the **iout:on** command.   N.A.                N.A.
            off             W         Disables the overall Modulation Switch. If some of the modulations are active, they are switched off too.                  N.A.                N.A.
            on              W         Enables the Modulation Channel 1.                                                                                          N.A.                N.A.
            off             W         Disables the Modulation Channel 1.                                                                                         N.A.                N.A.
            on              W         Enables the Modulation Channel 2.                                                                                          N.A.                N.A.
            off             W         Disables the Modulation Channel 2.                                                                                         N.A.                N.A.

  : Available commands for current
  generator.[\[\\QubeModel \_cmd\_table\_cm\]]{#\\QubeModel _cmd_table_cm
  label="\\QubeModel _cmd_table_cm"}
:::

::: {#\\QubeModel _cmd_table_tc}
  **Cmd**   **Value**       **R/W**   **Action**                                                                                                     **Output Format**   **Unit**
  --------- --------------- --------- -------------------------------------------------------------------------------------------------------------- ------------------- ----------
                                                                                                                                                                         
  tlas      ?               R         Return the Temperature of the laser measured by the TC Module.                                                 \#\#\#\#.\#\#       C
            on              W         Switches the Temperature Stabilization on.                                                                     N.A.                N.A.
            off             W         Switches the Temperature Stabilization off.                                                                    N.A.                N.A.
            ?               R         Return the laser Temperature Setpoint                                                                          \#\#\#\#.\#\#       C
            \#\#\#\#.\#\#   W         Sets the laser Temperature Setpoint                                                                            N.A.                C
  kp:       \#\#\#\#.\#\#   W         Sets the Proportional Gain Coefficient for the digital PID that manages the laser Temperature Stabilization.   N.A.                A/K
  ki:       \#\#\#\#.\#\#   W         Sets the Integral Gain Coefficient for the digital PID that manages the laser Temperature Stabilization.       N.A.                A/Ks
  kd:       \#\#\#\#.\#\#   W         Sets the Derivative Gain Coefficient for the digital PID that manages the laser Temperature Stabilization.     N.A.                As/K
                                      Returns the Gain Values of the Digital PID that manages the laser Temperature Stabilization.                                       
                                      kp                                                                                                             \#\#\#\#.\#\#:      A/K
                                      ki                                                                                                             \#\#\#\#.\#\#:      A/Ks
                                      kd                                                                                                             \#\#\#\#.\#\#       As/K
            dir             W         Sets the Temperature Stabilization PID to work in direct mode.                                                 N.A.                N.A.
            rev             W         Sets the Temperature Stabilization PID to work in reverse mode.                                                N.A.                N.A.
            ?               R         Returns the Maximum Temperature Setpoint for the Stabilization PID.                                            \#\#\#\#.\#\#       C
            \#\#\#\#.\#\#   W         Sets the Maximum Temperature Setpoint for the Stabilization PID.                                               N.A.                C
            ?               R         Returns the Minimum Temperature Setpoint for the Stabilization PID.                                            \#\#\#\#.\#\#       C
            \#\#\#\#.\#\#   W         Sets the Minimum Temperature Setpoint for the Stabilization PID.                                               N.A.                C
            ?               R         Returns the Maximum Current Output for the TC Module.                                                          \#\#\#\#.\#\#       A
            \#\#\#\#.\#\#   W         Sets the Maximum Current Output for the TC Module.                                                             N.A.                A
            ?               R         Returns the threshold for the Active Temperature Error Control.                                                \#\#\#\#.\#\#       C\*s
            \#\#\#\#        W         Sets the threshold for the Active Temperature Error Control.                                                   N.A.                C\*s

  : Available commands for temperature
  controller.[\[\\QubeModel \_cmd\_table\_tc\]]{#\\QubeModel _cmd_table_tc
  label="\\QubeModel _cmd_table_tc"}
:::

::: {#\\QubeModel _cmd_table_dds}
  --------- --------------- --------- ------------------------------------------------------------------------------------------------------------ ------------------- ----------
  **Cmd**   **Value**       **R/W**   **Action**                                                                                                   **Output Format**   **Unit**
            ?               R         Returns the status of the DDS on modulation channel 1. **1**: DDS is active. **0**: DDS is inactive.         \#                  Bool.
            on              W         Activates the DDS on channel 1.                                                                              N.A.                N.A.
            off             W         Switches off the DDS on channel 1.                                                                           N.A.                N.A.
            ?               R         Returns the waveform set for DDS on channel 1. **1**: Sine wave. **2**: Triangular wave.                     \#                  Int.
            \#              W         Sets the waveform for the DDS on channel 1. Accepted values are: **1**: Sine wave. **2**: Triangular wave.   N.A.                Int.
            ?               R         Returns the frequency of the DDS on channel 1.                                                               \#\#\#\#.\#\#       Hz
            \#\#\#\#.\#\#   W         Sets the frequency for the DDS on channel 1.                                                                 N.A.                Hz
            ?               R         Returns the amplitude of the DDS on channel 1.                                                               \#\#\#\#.\#\#       mA
            \#\#\#\#.\#\#   W         Sets the amplitude for the DDS on channel 1.                                                                 N.A.                mA
            ?               R         Returns the phase of the DDS on channel 1.                                                                   \#\#\#\#.\#\#       Deg.
            \#\#\#\#.\#\#   W         Sets the phase for the DDS on channel 1.                                                                     N.A.                Deg.
            ?               R         Returns the status of the DDS on modulation channel 2. **1**: DDS is active. **0**: DDS is inactive.         \#                  Bool.
            on              W         Activates the DDS on channel 2.                                                                              N.A.                N.A.
            off             W         Switches off the DDS on channel 2.                                                                           N.A.                N.A.
            ?               R         Returns the waveform set for DDS on channel 2. **1**: Sine wave. **2**: Triangular wave.                     \#                  Int.
            \#              W         Sets the waveform for the DDS on channel 2. Accepted values are: **1**: Sine wave. **2**: Triangular wave.   N.A.                Int.
            ?               R         Returns the frequency of the DDS on channel 2.                                                               \#\#\#\#.\#\#       Hz
            \#\#\#\#.\#\#   W         Sets the frequency for the DDS on channel 2.                                                                 N.A.                Hz
            ?               R         Returns the amplitude of the DDS on channel 2.                                                               \#\#\#\#.\#\#       mA
            \#\#\#\#.\#\#   W         Sets the amplitude for the DDS on channel 2.                                                                 N.A.                mA
            ?               R         Returns the phase of the DDS on channel 2.                                                                   \#\#\#\#.\#\#       Deg.
            \#\#\#\#.\#\#   W         Sets the phase for the DDS on channel 2.                                                                     N.A.                Deg.
            ?               R         Returns the frequency of the DDS channel to which the Sync. Out signal is synchronized.                      \#\#\#\#.\#\#       Hz
            ch1             W         Synchronizes the Sync. Out signal to the DDS1                                                                N.A.                N.A.
            ch2             W         Synchronizes the Sync. Out signal to the DDS2                                                                N.A.                N.A.
  --------- --------------- --------- ------------------------------------------------------------------------------------------------------------ ------------------- ----------

  : Available commands for the DDS
  submodule.[\[\\QubeModel \_cmd\_table\_dds\]]{#\\QubeModel _cmd_table_dds
  label="\\QubeModel _cmd_table_dds"}
:::

::: {#\\QubeModel _cmd_table_pll}
  --------- ----------- --------- --------------------------------------------------------------------------------------------------------------------------------------- ------------------- ----------
  **Cmd**   **Value**   **R/W**   **Action**                                                                                                                              **Output Format**   **Unit**
                                  Allow the user to select which signal is present on the DIVIDER MON output. Allowed values are:                                                             
                                  **0** DIVIDER MON switched off.                                                                                                                             
                                  **2** DIVIDER MON set on RF.                                                                                                                                
                                  **4** DIVIDER MON set on LO.                                                                                                                                
  sig:      \#          W         Set the sign of the PLL correction loop. Accepted values are: **0**: negative correction loop. **1**: positive correction loop.         N.A.                Int.
            ?           R         Returns the value of cp, which is the gain of the PLL. Must be switched ON.                                                             \#\#                HEX.
            on          W         Switches ON the proportional gain of the PLL chip.                                                                                      N.A.                N.A.
            off         W         Switches OFF the proportional gain of the PLL chip.                                                                                     N.A.                N.A.
            \#          W         Set the proportional gain. The value can range from 1 to 8.                                                                             N.A.                Int.
  ndiv:     \#\#\#\#    W         Sets the divisor coefficient for the RF frequency input.                                                                                N.A.                Int.
  rdiv:     \#\#\#\#    W         Sets the divisor coefficient for the LO frequency input.                                                                                N.A.                Int.
            off         W         Sets the PLL correction loop in proportional only mode.                                                                                 N.A.                N.A.
            on          W         Sets the PLL correction loop in proportional-integrative mode.                                                                          N.A.                N.A.
  tp:       \#          W         Sets the Integrative time constant of the PLL correction loop. Accepted values range from 0 to 3.                                       N.A.                Int.
  tz:       \#          W         Sets the Proportional gain of the PLL correction loop. Accepted values range from 0 to 3.                                               N.A.                Int.
  hg:       \#          W         Sets the proportional gain of the PLL chip. Accepted values ranges from 0 to 3.                                                         N.A.                Int.
            off         W         Switches OFF the correction current injected by the PLL module into the Bias Current.                                                   N.A.                N.A.
            on          W         Activates the correction current injected by the PLL module into the Bias Current. Overall modulation must be enabled for it to work.   N.A.                N.A.
  lm:       ?           R         Returns the value of the PLL correction loop output voltage.                                                                            \#\#\#\#.\#\#       mV
  --------- ----------- --------- --------------------------------------------------------------------------------------------------------------------------------------- ------------------- ----------

  : Available commands for the PLL locking
  module.[\[\\QubeModel \_cmd\_table\_pll\]]{#\\QubeModel _cmd_table_pll
  label="\\QubeModel _cmd_table_pll"}
:::

::: {#\\QubeModel _cmd_table_pdh}
  ------------ --------------- --------- --------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------ ----------
  **Cmd**      **Value**       **R/W**   **Action**                                                                                                                                    **Output Format**              **Unit**
               off             W         Sets the PDH correction loop in proportional only mode.                                                                                       N.A.                           N.A.
               on              W         Sets the PDH correction loop in proportional-integrative mode                                                                                 N.A.                           N.A.
               off             W         Deactivates the **HOLD** input of the PDH module.                                                                                             N.A.                           N.A.
               on              W         Activates the **HOLD** inptut of the PDH module.                                                                                              N.A.                           N.A.
               off             W         Deactivates the correction current injected into the Bias current by the PDH module.                                                          N.A.                           N.A.
               on              W         Activates the correction current injected into the Bias current by the PDH module. Overall modulation enable must be active for it to work.   N.A.                           N.A.
  pdhrint:     \#              W         Sets the first proportional gain of the PDH correction loop. Accepted values range from 0 to 3.                                               N.A.                           Int.
  pdhtz:       \#              W         Sets the second proportional gain of the PDH correction loop. Also affect the Integrative time constant. Accepted values range from 0 to 3.   N.A.                           Int.
  pdhtp:       \#              W         Sets the time constant of the PDH correction loop. Accepted values range from 0 to 3.                                                         N.A.                           Int.
  pdhmon:      \#              W         Sets which signal is present on the Monitor Output of the PDH module. Accepted values are: **0**: Error Signal. **1**: Correction signal.     N.A.                           Int.
  pdhmonint:   ?               R         Returns the values of the Error and Correction signals converted by the on board ADCs.                                                        \#\#\#\#.\#\#: \#\#\#\#.\#\#   mV
               ?               R         Returns the input offset of the PDH correction loop.                                                                                          \#\#\#\#.\#\#                  mV
               \#\#\#\#.\#\#   W         Sets the input offset of the PDH correction loop. The value can range from 0 to 5000. Default is 2500.                                        N.A.                           mV
               ?               R         Returns the PDH correction loop pre-amplifier gain.                                                                                           \#\#\#\#.\#\#                  mV
               \#\#\#\#.\#\#   W         Sets the PDH coorection loop pre-amplifier gain. Accepted values range from 0 to 63.                                                          N.A.                           mV
  ------------ --------------- --------- --------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------ ----------

  : Available commands for the PDH locking
  module.[\[\\QubeModel \_cmd\_table\_pdh\]]{#\\QubeModel _cmd_table_pdh
  label="\\QubeModel _cmd_table_pdh"}
:::

::: {#\\QubeModel _cmd_table_lia}
  --------- --------------- --------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ------------------- ----------
  **Cmd**   **Value**       **R/W**   **Action**                                                                                                                                                                                                                                  **Output Format**   **Unit**
            ?               R         Returns the mode of the correction loop: **0** stands for **P** mode. **1** stands for **PI** mode.                                                                                                                                         \#                  Bool.
            0               W         Sets the correction loop in P mode.                                                                                                                                                                                                         N.A.                Int.
            1               W         Sets the correction loop in PI mode.                                                                                                                                                                                                        N.A.                Int.
            ?               R         Returns the status of the Low Pass Filter of the correction loop: **0** stands for inactive. **1** stands for active.                                                                                                                       \#                  Bool.
            en              W         Activates Low Pass Filter                                                                                                                                                                                                                   N.A.                N.A.
            dis             W         Deactivates Low Pass Filter                                                                                                                                                                                                                 N.A.                N.A.
            ?               R         Returns the VGA Gain.                                                                                                                                                                                                                       \#\#\#\#.\#\#       dB
            \#\#\#\#.\#\#   W         Sets the VGA Gain                                                                                                                                                                                                                           N.A.                dB
            ?               R         Returns the pole of the correction loop.                                                                                                                                                                                                    \#                  Int.
            \#              W         Sets the pole of the correction loop. Accepted value ranges from 0 to 3.                                                                                                                                                                    N.A.                Int.
            ?               R         Returns the proportional gain of the correction loop.                                                                                                                                                                                       \#                  Int.
            \#              W         Sets the proportional gain of the correction loop. Accepted values ranges from 0 to 3.                                                                                                                                                      N.A.                Hz
            ?               R         Returns the frequency setting for the Low Pass Filter of the correction loop.                                                                                                                                                               \#                  Int.
            \#              W         Sets the frequency setting for the Low Pass Filter of the correction loop. Accepted value ranges from 0 to 3.                                                                                                                               N.A.                mA
            on              W         Activates the LIA correction loop.                                                                                                                                                                                                          N.A.                N.A.
            off             W         Deactivates the LIA correction loop.                                                                                                                                                                                                        N.A.                N.A.
            ?               R         Returns the demodulation mode of the LIA. **0** stands for **f** mod. **1** stands for **2f** mode. **2** stands for no deomdulation acrive.                                                                                                \#                  Int.
            f               W         Sets the **f** demodulation mode                                                                                                                                                                                                            N.A.                N.A.
            2f              W         Sets the **2f** demodulation mode                                                                                                                                                                                                           N.A.                N.A.
            free            W         Deactivates the demodulation                                                                                                                                                                                                                N.A.                N.A.
            ?               R         Returns the currently set for the output monitor of the LIA module: **0** stands for correction monitor. **1** stands for ERROR monitor.                                                                                                    \#\#\#\#.\#\#       Deg.
            err             W         Sets the output monitor to show the ERROR signal.                                                                                                                                                                                           N.A.                N.A.
            lock            W         Sets the output monitor to show the correction signal.                                                                                                                                                                                      N.A.                N.A.
            ?               R         Returns the digital filter currently in use: **1** stands for **BP0**. **2** stands for **BP1**. **3** stands for **BP2**. **4** stands for **LP1**. **5** stands for **LP2**. **6** stands for **Notch**. **7** stands for **All Pass**.   \#                  Int.
            BP0             W         Sets the BP0 filter                                                                                                                                                                                                                         N.A.                N.A.
            BP1             W         Sets the BP1 filter                                                                                                                                                                                                                         N.A.                N.A.
            BP2             W         Sets the BP2 filter                                                                                                                                                                                                                         N.A.                N.A.
            LP0             W         Sets the LP0LP0 filter                                                                                                                                                                                                                      N.A.                N.A.
            LP1             W         Sets the LP1 filter                                                                                                                                                                                                                         N.A.                N.A.
            NOTCH           W         Sets the NOTCH filter                                                                                                                                                                                                                       N.A.                N.A.
            ALLPASS         W         Sets the ALLPASS filter                                                                                                                                                                                                                     N.A.                N.A.
  --------- --------------- --------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ------------------- ----------

  : Available commands for the LIA locking
  module.[\[\\QubeModel \_cmd\_table\_lia\]]{#\\QubeModel _cmd_table_lia
  label="\\QubeModel _cmd_table_lia"}
:::

::: {#\\QubeModel _cmd_table_SlowLoop}
  -- ---------- --- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------- -------
     ?          R   Returns the current status of the Slow Loop: **0** stands for inactive. **1** stands for active.                                                                                                   \#         Bool.
     on         W   Activates the Slow Loop for the mounted locking module, if any.                                                                                                                                    N.A.       N.A.
     off        W   Deactivates the Slow Loop.                                                                                                                                                                         N.A.       N.A.
     ?          R   Returns which actuator is currently set to be used by the Slow Loop: **0** Slow Loop uses laser current. **1** Slow Loop uses laser temperature.                                                   \#         Bool.
     temp       W   Sets the Slow Loop to use the laser temperature as actuator.                                                                                                                                       N.A.       N.A.
     curr       W   Sets the Slow Loop to use the laser current as actuator.                                                                                                                                           N.A.       N.A.
     ?          R   Returns the sign of the Slow Loop: **0** Slow Loop acting in reverse mode. **1** Slow Loop acting in direct mode.                                                                                  \#         Bool.
     dir        W   Sets the Slow Loop to work in direct mode.                                                                                                                                                         N.A.       N.A.
     rev        W   Sets the Slow Loop to work in reverse mode.                                                                                                                                                        N.A.       N.A.
     ?          R   Returns the time interval at which the Slow Loop reads the locking module output in order to operate its correction. The smaller the reading interval, the faster the Slow Loop reacts.            \#\#\#\#   ms
     \#\#\#\#   W   Sets the time Interval at which the Slow Loop checks the Locking Module output amplitude. Acceptable values range from 1 to 2000.                                                                  N.A.       ms
     ?          R   Returns the maximum laser current change that the Slow Loop can produce.                                                                                                                           \#\#\#\#   mA
     \#\#\#\#   W   Sets the maximum change the Slow Loop can produce to the current output to the laser. This parameter must be set for safety reason in order not to damage the laser with excessive bias current.   N.A.       mA
  -- ---------- --- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---------- -------

  : Available commands to use the Slow Loop with locking modules.
  [\[\\QubeModel \_cmd\_table\_SlowLoop\]]{#\\QubeModel _cmd_table_SlowLoop
  label="\\QubeModel _cmd_table_SlowLoop"}
:::

::: {#\\QubeModel _cmd_table_stat}
  --------- --- --- ---------------------------------------------------------------- --------------- ---
  vcc:      ?   R   Returns the Supply Voltage for the CM Module measured by the .   \#\#\#\#.\#\#   V
  tsense:   ?   R   Returns the internal Temperature of the instrument.              \#\#\#\#.\#\#   C
  --------- --- --- ---------------------------------------------------------------- --------------- ---

  : Available commands to check the instrument
  status.[\[\\QubeModel \_cmd\_table\_stat\]]{#\\QubeModel _cmd_table_stat
  label="\\QubeModel _cmd_table_stat"}
:::
