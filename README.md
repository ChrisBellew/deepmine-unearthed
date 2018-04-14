# Deepmine Unearthed 2018 Challenge

### Tag Names Spreadsheet
https://docs.google.com/spreadsheets/d/1VHEmBi-e7DS0N7x_oVzxAAmPAF1_llo8CB_pIk1cC24/edit?usp=sharing


### Refinery information
- The ore is offloaded by trucks
- There are 2 ball mills which grind the ore to a fine powder
- There are 6 claves which use chemical reactions to try and leach out the Nickel. They end up leaching Nickel, but also the biproducts Cobalt and Copper. Copper is interesting because it can affect the efficiency of the downstream copper boil. Cobalt is not interesting.
    - The claves are arranged into 3 stages.
        - Stage 1 has two claves in parallel
        - Stage 2 has three claves in parallel
        - Stage 3 has one clave
    - Each clave has 4 compartments
    - Ammonia and air is added at each clave to try and leach the Nickel
        - Ammonia is being added in the first compartment of each clave
        - Air is being added in each compartment of each clave
- The measurement of the total mass and metal composition of the ore is measured at the start of the refinery, before it is divided into two ball mills.
- The amount of ammonia and air being added is measured for each clave
- The outputs of each clave are measured:
    - The amount of each metal that has leached into the LIQUOR    
    - The amount of each metal that has not leached, and is still in SOLID form.
    - The temperature of the outputs. (Not sure if this is the temperature of the LIQUOR or the SOLID?)
    - 

### Data Spreadsheets Explanation
#### Leach Data - Raw - Stable Period: This  is a spreadsheet of SCADA data that is measured every 30 seconds. This contains:
- Measurements of the outputs after each clave. The outputs are:
    - The amount of Nickel that has leached into the liquor as measured after THIS CLAVE.
        - Measured in grams/litre
            - (For example: 02ALA000001.NI.LIQ for clave 1A)
            - (For example: 02ALA000002.NI.LIQ for clave 1B)
        - Measured as a %, by MASS, of the ALL the Nickel that input to the ENTIRE REFINERY
            - (For example: 02ALA000001.NI_EX.SOL for clave 1A)
            - (For example: 02ALA000002.NI_EX.SOL for clave 1B)
    - The amount of Nickel that is remaining in the solid, and has failed to leach. 
        - Measured as the % mass of all the solids found after THIS CLAVE, is Nickel.
            - (For example: 02ALA000001.NI.SOL for clave 1A)
            - (For example: 02ALA000002.NI.SOL for clave 1B)
    [The above Nickel measurements are repeated for all ]
- Measurements about the thickener - I dont know anything about these

# EVERYONE SHOULD READ THIS SECTION BELOW!

## Inputs into entire refinery

- When ore is offloaded from the trucks it it goes into two ball mills in parallel to be ground down (Mill 1 and Mill 2).
- The weight of the ore coming in is measured before both Mill 1 and Mill 2. The units are tonnes/hour.
	#### Mill 1 (WC32000.PV) - TONNE/HR - No1 MILL FEED - (Leach Data - Raw - Stable Period)
	#### Mill 2 (WC32100.PV) - TONNE/HR - No2 MILL FEED - (Leach Data - Raw - Stable Period)

- If we add these two together we can get the total tonnes/hour of ore that are being input into the refinery
	#### Total Tonnes/hour Ore input = WC32000.PV + WC32100.PV
	
- At the same place before both mills, the composition of the metals in the ore is also measured. These are in % of the total ore.
	#### Feed % Nickel (OA_KNR_MATT_RFNY.NI) - % - (Refinery Feed)
	#### Feed % Iron (OA_KNR_MATT_RFNY.FE) - % - (Refinery Feed)
	#### Feed % Copper (OA_KNR_MATT_RFNY.CU) - % - (Refinery Feed)
	#### Feed % Cobalt (OA_KNR_MATT_RFNY.CO) - % - (Refinery Feed)
	#### Feed % Sulphur (OA_KNR_MATT_RFNY.S) - % - (Refinery Feed)
	#### Feed % Arsenic (OA_KNR_MATT_RFNY.AS) - % - (Refinery Feed)
	
- So using the above % measurements and the tonnes/hour of the total, we can work out the tonnes/hour of each metal.
	#### Feed tonnes/hour Nickel = (OA_KNR_MATT_RFNY.NI / 100) * Total Tonnes/hour Ore input
	#### Feed tonnes/hour Iron = (OA_KNR_MATT_RFNY.FE / 100) * Total Tonnes/hour Ore input
	#### ... etc

- So we know how much of each metal in tonnes/hour that is entering into each of the first stage claves.

## Inputs into First Stage Claves

- Since there are three two stage claves, let's divide the tonnes/hour of each metal by two, and thats how much tonnes/hour of each metal that is going into each first stage clave
	#### 1A clave tonnes/hour Nickel input = Feed tonnes/hour Nickel / 2
	#### 1A clave tonnes/hour Iron input = Feed tonnes/hour Iron / 2
	#### ... etc

## Inputs into all claves
- The volume of slurry being fed into each clave
    #### LCH 2A FEED (FI02045B.PV) - L/MIN - (Leach Data - Raw - Stable Period)

## Additives being added to each clave

- Ammonia and air are added to each clave
    - Ammonia:
        #### LEACH CLAVE 2A ANHYD. NH3 (FC02039B.PV) - TONNE/HR - (Leach Data - Raw - Stable Period)
        #### LEACH CLAVE 2B ANHYD. NH3 (FC02033B.PV) - TONNE/HR - (Leach Data - Raw - Stable Period)
        #### LEACH CLAVE 3A ANHYD. NH3 (FC02042B.PV) - TONNE/HR - (Leach Data - Raw - Stable Period)
        #### LEACH CLAVE 3B ANHYD. NH3 (FC02036B.PV) - TONNE/HR - (Leach Data - Raw - Stable Period)
        #### A2C - 1A Lch Clv Ammonia (FC02309.PV) - TONNE/HR - (Leach Data - Raw - Stable Period)
        #### A2C - 1B Lch Clv Ammonia (FC02312.PV) - TONNE/HR - (Leach Data - Raw - Stable Period)
    - Air by compartment:
        #### LCH 1A C1 AIR (FC02094A.PV) - NM3/HR - (Leach Data - Raw - Stable Period)
        #### LCH 1A C2 AIR (FC02095A.PV) - NM3/HR - (Leach Data - Raw - Stable Period)
        #### ... etc
    - Air by clave:
        #### LCH 1B TOTAL AIR (FI02352.PV) - NM3/HR - (Leach Data - Raw - Stable Period)
        #### ... etc

## Temperature measurements
- Temperature is being measured in each clave
    - In each compartment
        #### A2C-1A C1 TEMPERATURE (TI02260A.PV) - DegC - (Leach Data - Raw - Stable Period)
        #### A2C-1A C2 TEMPERATURE (TI02261A.PV) - DegC - (Leach Data - Raw - Stable Period)
        #### ... etc
    - Each compartment has a cooling coil which water flows through to cool the reaction. The temperature is measured at the end of each of these coils
        #### LCH 1A C1 (FC02094A.PV) - NM3/HR - (Leach Data - Raw - Stable Period)
        #### ... etc
