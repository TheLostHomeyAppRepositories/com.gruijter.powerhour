# Power by the Hour

Get data from a Homey power/gas/water meter device, and show the usage / production per hour, per day, per month and per year. Know the monetary value and use dynamic tariffs. Know how much your Always-on appliances are using and safe hundreds of Euros per year!

This app can be used for instance together with the Enelogic and Youless app, the Plugwise Smile P1 app, the BeeClear app, the Solar Power app, the Homewizard app, Tibber pulse, or any other app that has a cumulative Energy Meter (meter_power capability), a Power Meter (measure_power capability) a cumulative Gas Meter (meter_gas capability), or a cumulative Water Meter (meter_water capability).

<img src="https://global.discourse-cdn.com/business4/uploads/athom/original/3X/5/5/55d1f95545e8389c18729221bf901a71321811fb.jpeg" alt="device information tile" width="375"/>
 <br>
 <br>
 <br>

## PBTH summarizer device setup
Add a PBTH device and select if you want to summarize power, gas or water. A list of all compatible source devices is shown. Just select the one you want to add. Note that PBTH allows you to use power meters (Watt) as source device. This is however a fallback method that is less accurate then when using an energy meter (kWh) as source device. During pairing PBTH will automatically select the best available source. In the device settings you can manually switch this. If your device doesn't show up at all, you can select the VIRTUAL_METER at the bottom of the list. 

<img src="https://global.discourse-cdn.com/business4/uploads/athom/original/3X/1/2/12a1275dde87ca9c92c8d79ce12db4f586e2866b.jpeg" alt="driver selection" width="250"/>
<img src="https://global.discourse-cdn.com/business4/uploads/athom/optimized/3X/5/0/50cf03f760502098a2a017832b2b1aeb9948c6d5_2_225x500.jpeg" alt="device selection" width="200"/>  
<br>
<br>
<br>

## Using the PBTH Virtual Meter Summarizer
Selecting the virtual meter will allow any app/device that has an energy(kWh)/gas(m3)/water(m3) meter to use PBTH, even when the source app is using non-standard meter capability naming. The meter values must then be send to PBTH via a flow. Note that the meter value for energy must be the total kWh, meaning (consumed_high + consumed_low - returned_high - returned_low).

<img src="https://global.discourse-cdn.com/business4/uploads/athom/original/3X/5/5/55e82da0ff03a2e8357db5e83bf71d458e72040b.png" alt="virtual meter upload flow" width="200"/>  
 <br>
 <br>
 <br>

## Setting summarizer meter readings
From the device settings you can enter the meter readings as they were at the beginning of a period (this month, this year). You only need to do this once after adding the PBTH device. The meter values will automatically be updated every hour.  
<br>

## Setting tariff and money values
**PBTH can be used with any currency.** From the device settings you can set the monetary values of various periods (month, year). You only need to do this once after adding the PBTH device. The money values will automatically be updated every hour based on the tariff you set. If your tariff only changes once once a year it is easiest to do this from the device settings. If your tariff often changes, e.g. during nights and weekends, you can dynamically set the active tariff from a flow. You can use a scheduler app to do this, or use a flow like below example.  

<img src="https://global.discourse-cdn.com/business4/uploads/athom/original/3X/4/d/4d66a18295c0e18112eed0150d22ca9864a2773c.jpeg" alt="tariff change flow" width="200"/> 
<br>
<br>
<br>

## Compare usage with a yearly budget
Real-time comparison with a yearly reference gas/electricity/water usage, based on a settable budget. Since in winter you usually use more then in summer, a distribution is applied. Next to a linear (flat) distribution, I implemented the distribution that is used by the Netherlands Government for the 2023 price ceiling (‘prijsplafond’), and a PV-system (solar panels) distribution.

## Finding out how much your Always-On appliances are using
The Minimum value from your main meter can be used to see how much power your always-on equipment is using (e.g. wifi routers, NAS, TV in stand-by, etc). **Every 10 Watt you save on this value will result in a yearly saving of around 90kWh (20 Euro)!** Note that if you have solar panels you can only measure this value correctly at night. The best moment is therefore just before sunrise in the morning.

<img src="https://global.discourse-cdn.com/business4/uploads/athom/original/3X/2/3/238b5a7c7a3495dd4e375d5b8f3621ccc97b8bf6.jpeg" alt="detecting leaks" width="200"/>  
<br>
<br>
<br>

## Finding out gas or water leaks
The Minimum value can be used to detect a gas leak or water leak. If the minimum over a 24Hr period is not 0, you have a leak! Note that a leak is only detected this way if the leakage is more then 0.5 liter per minute.
<br>
<br>

## Using Day-Ahead pricing (EU market spot pricing)
If you have a European energy provider that changes its pricing every hour (electricity) or every day (gas), you can use the built-in `Day-ahead Pricing` driver. Add the pricing device and select the correct Bidding Zone.
From the device settings you can set the taxes and markups your provider is charging on top of the net purchase price. All purchase prices are in EURO, but you can set an exchange rate to any other currency. If you enable 'Send tariff' all PBTH power summarize devices will be automatically updated every hour. Use the price_changed flowcard, combined with the average price for the next 8 hours, to save money. E.g. Control the car charging per hour, start the dish-washer at the perfect moment, or even put fridges ‘on pause’ for an hour if that is cost effective.

<img src="https://global.discourse-cdn.com/business4/uploads/athom/original/3X/b/5/b536b76cdb308d7d3745e087f17280ac481600b4.jpeg" alt="1H Day-Ahead pricing" width="200"/> 
<br>
<br>
<br>

The electricity pricing information is fetched from ENTSO-E, the European Network of Transmission System Operators for Electricity. https://transparency.entsoe.eu/transmission-domain/r2/dayAheadPrices/show
Nordpool is used as backup for electricity pricing: https://www.nordpoolgroup.com/
All Gas spot pricing (EOD and EGSI) is coming from EEX: https://www.eex.com/en/market-data/natural-gas/spot
TTF LEBA gas pricing is derived from EasyEnergy as seen here: https://www.nieuwestroom.nl/energiemarkt/energiebeurzen/gas-handelsbeurs/

### DONATE
If you like the app, don't hesitate to [DONATE](https://www.paypal.me/gruijter)