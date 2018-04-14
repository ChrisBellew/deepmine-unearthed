# Deepmine Unearthed 2018 Challenge

### Tag Names Spreadsheet
https://docs.google.com/spreadsheets/d/1VHEmBi-e7DS0N7x_oVzxAAmPAF1_llo8CB_pIk1cC24/edit?usp=sharing


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
	####... etc