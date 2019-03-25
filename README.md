# Background

This is part of the [*Sustainable Industry: Rinse Over Run*](https://www.drivendata.org/competitions/56/predict-cleaning-time-series/) competition hosted by [DrivenData](https://www.drivendata.org/)

# Objective

Create a model that predicts the turbidity in the last rinsing phase of a clean-in-place (CIP) process in order to help minimize the use of water, energy and time, while ensuring high cleaning standards.

Predict the quantity of turbidity—the level of product traces or suspended solids in the effluent—that will be returned in last rinsing phase during the cleaning of food and beverage industrial equipment. Depending on the expected level of turbidity, the cleaning station operator can adjust the length of the final rinse accordingly, enabling high cleaning standards while minimizing unnecessary use of water and chemicals.

# Data

The datasets can be downloaded from the [competition site](https://www.drivendata.org/competitions/56/predict-cleaning-time-series/data/).

## Metadata

* `process_id` - Process ID
* `object_id` - Object ID
* `phase` - Phase of the cleaning process
* `timestamp` - Timestamp of measurement
* `pipeline` - Pipeline name

### Clean-In-Place Measurements

* `supply_flow` - Measure of the flow of the fluid entering the pipeline
* `supply_pressure` - Pressure in bar of the cleaning agents in the supply line
* `return_temperature` - Temperature in degrees Celsius of cleaning agents in the return line
* `return_conductivity` - Conductivity in millisiemens of cleaning agents in the return line
* `return_turbidity` - Turbidity in NTU of cleaning agents in the return line
* `return_flow` - Flow in liter per hour of cleaning agents in the return line
* `supply_pump` - State (Boolean) of the supply pump on the supply line
* `supply_pre_rinse` - State (Boolean) of the pre rinse valve on the supply line
* `supply_caustic` - State (Boolean) of the caustic valve on supply line
* `return_caustic` - State (Boolean) of the caustic valve on return line
* `supply_acid` - State (Boolean) of the acid valve on supply line
* `return_acid` - State (Boolean) of the acid valve on return line
* `supply_clean_water` - State (Boolean) of the clean water valve on supply line
* `return_recovery_water` - State (Boolean) of the recovery water valve on return line
* `return_drain` - State (Boolean) of the drain valve on return line
* `object_low_level` - Presence (Boolean) of liquid in the cleaning object (for example, liquid will remain if the pump on the CIP return line did not fully purge the object)
* `tank_level_pre_rinse` - Level in percentage of the pre rinse tank
* `tank_level_caustic` - Level in percentage of the caustic tank
* `tank_level_acid` - Level in percentage of the acid tank
* `tank_level_clean_water` - Level in percentage of the clean water tank
* `tank_temperature_pre_rinse` - Temperature in degrees Celsius in the water recovery tank
* `tank_temperature_caustic` - Temperature in degrees Celsius in the caustic tank
* `tank_temperature_acid` - Temperature in degrees Celsius in the acid tank
* `tank_concentration_caustic` - Concentration in millisiemens in the caustic tank
* `tank_concentration_acid` - Concentration in millisiemens in the acid tank
* `tank_lsh_caustic` - State (Boolean) of the High Level Switch of the acid tank (used to determine if the tank is full or not)
* `tank_lsh_acid` - State (Boolean) of the High Level Switch of the acid tank (used to determine if the tank is full or not)
* `tank_lsh_clean_water` - State (Boolean) of the High Level Switch of the clean water tank (used to determine if the tank is full or not)
* `tank_lsh_pre_rinse` - State (Boolean) of the High Level Switch of the pre rinse tank (used to determine if the tank is full or not)
* `target_time_period` - Indicator (Boolean) of if the observation is included when calculating the target variable.

`train_labels.csv` contains the target variable, `final_rinse_total_turbidity_liter`. This is defined as the quantity of turbidity returned multiplied by the outgoing flow during the `target_time_period.` The target time period is the portion of the final rinse phase when the return caustic and return acid valves have been closed for the last time. 

Every `process_id` in the training values data has a corresponding `final_rinse_total_turbidity_liter` label in this file. The calculation for the target variable is as follows: `sum(max(0, return_flow) * return_turbidity)` where `target_time_period=True`.
