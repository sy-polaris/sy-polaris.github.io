---
id: 2177
title: 'Sistema di navigazione RASPINAV [opencpn + AIS + wi-fi NMEA data server]'
date: 2015-11-25T16:37:22+01:00
author: polaris
layout: post
categories:
  - Senza categoria
---
**HARDWARE**  
-RaspberryPi 2 Mod. B  
-monitor 7″ VGA a 12V  
-convertitore HDMI-VGA  
-convertitore DC-DC 12V-5V 2A a 2 posti (per alimentare Raspberry e USB hub)  
-tastiera e mouse wireless Rapoo  
-USB hub 7 porte  
-USB WiFi dongle  
-NooElec NESDR Mini SDR & DVB-T USB Stick (RTL2832 + R820T) (ricezione segnali AIS)  
-Seatalk-NMEA bridge USB (SeatalkLink) collegato a porta Seatalk del Raymarine ST60+ Tridata  
-strumentazione Raymarine GPS 125, Serie ST60+ (Tridata, Wind), autopilota ST6001+ Smartpilot

**SOFTWARE**  
-Raspbian Jessie [https://www.raspberrypi.org/downloads/raspbian/]  
-Opencpn 4.0.0 \[http://opencpn.org\] \[http://www.agurney.com/raspberry-pi/pi-chart\]  
-rtl-sdr [http://sdr.osmocom.org/trac/wiki/rtl-sdr]  
-aisdecoder [http://www.aishub.net/aisdecoder-via-sound-card.html]  
-hostapd  
-dnsmsq

Dal Seatalk-NMEA bridge esce il flusso dati NMEA (USB) che alimenta opencpn.  
Con hostapd + dnsmasq viene creata una rete wifi di bordo.  
opencpn legge i dati NMEA e AIS e li ritrasmette sulla rete wifi di bordo.

**Client**  
-Nexus 5 con app SeaWi per dati NMEA + AIS  
-Nexus 9 con opencpn per Android, SeaWi

&nbsp;