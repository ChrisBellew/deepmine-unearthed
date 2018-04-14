# Deepmine Unearthed 2018 Challenge

### Tag Names Spreadsheet
https://docs.google.com/spreadsheets/d/1VHEmBi-e7DS0N7x_oVzxAAmPAF1_llo8CB_pIk1cC24/edit?usp=sharing


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
- Since there are three first stage claves, let's divide the tonnes/hour of each metal by 3, and thats how much tonnes/hour of each metal that is going into each first stage clave
	#### 1A clave tonnes/hour Nickel input = Feed tonnes/hour Nickel / 3
	#### 1A clave tonnes/hour Iron input = Feed tonnes/hour Iron / 3
	####... etc