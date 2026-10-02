Ditt första bash-skript

1.
#!/bin/bash
echo "Hej Världen!"

2.
#!/bin/bash
# Presentation av mig, Ahmed
echo "Namn: Ahmed"
echo "Ort: Rinkeby"
echo "Favorit mat: Pizza"

3.
#!/bin/bash
echo "Vad heter du?"
read namn
echo "Hej $namn! Hur gammal är du?"
read age
echo "Du heter $namn och är $age år gammal"

Del 2 
Övning 5
#!/bin/bash
echo "Skriv ett tal"
read tal1
echo "skriv ett till tal"
read tal2
sum=$((tal1 + tal2))
skillnad=$((tal1 - tal2))
produkten=$((tal1 * tal2))

echo "Produkten är $produkten"
echo "Summan är $sum"
echo "skillnaden är $skillnad"

Övning 6
#!/bin/bash
whoami=$(whoami)
date=$(date)
pwd=$(pwd)

echo "Inloggad användare:$whoami"
echo "Datum: $date"
echo "Du står i mappen:$pwd "

Del 3
Övning 7
#!/bin/bash
echo "Hur gammal är du?"
read alder
if [ "$alder" -ge 18 ]; then 
	echo "Du är myndig"
else 
	echo "Du är inte myndig än"
fi

Övning 8
#!/bin/bash
echo "skriv ditt lösenord"
read losenord
echo ""
if [ "$losenord" = "hemligt" ]; then
	echo "korrekt"
else 
	echo "fel!"
fi

Övning 9¨
#!/bin/bash
if [ -f "$1" ]; then
	echo "filen finns"
else
	echo "finns inte"
fi

Del 4 
Övning 10
#!/bin/bash
echo "Hur många varv vill du köra?"
read antal
for (( i=1; i<=antal; i++)); do
	echo "varv nummer $i"
done

Övning 11
#!/bin/bash
antal=0

for f in rndmfiler/*.txt; do
    if [ -e "$f" ]; then
        echo "Hittade: $f"
        ((antal++))
    fi
done

echo "Totalt hittades $antal txt-filer."

Övning 12
#!/bin/bash

fil="logg.txt"

if [ ! -f "$fil" ]; then
    echo "Fel: Filen $fil finns inte."
    exit 1
fi

rader=$(wc -l < "$fil")

> "$fil"


echo "$fil hade $rader rader. Filen är nu tömd."

övning 13
#!/bin/bash

datum=$(date +%F)

antal=$(ls -l *.txt 2>/dev/null | wc -l)

tar -czf "backup-$datum.tar.gz" *.txt 2>/dev/null

echo "Säkerhetskopierade $antal filer till backup-$datum.tar.gz"

övningar: grep, sed, awk och RegEx

Del 1 

1. grep ^Anna kontakter.txt
Anna Svensson, anna.svensson@skolan.se, 070-123 45 67

2. grep in$ server.log
2026-09-21 08:14:02 INFO Användare anna loggade in
2026-09-21 09:02:33 INFO Användare erik loggade in

3. grep [9-9][0-9]$ elever.csv
Erik Johansson,NA23,Natur,92
Maja Holm,EK23,Ekonomi,95

4. grep -E 'TE23|EK23' elever.csv
Anna Svensson,TE23,Teknik,78
Sara Lind,TE23,Teknik,65
Omar Hassan,EK23,Ekonomi,88
Johan Ek,TE23,Teknik,71
Maja Holm,EK23,Ekonomi,95

5. grep -E 'ERROR|WARNING' server.log
2026-09-21 08:15:47 WARNING Diskutrymme under 20%
2026-09-21 08:17:10 ERROR Kunde inte ansluta till databasen
2026-09-21 10:30:00 ERROR Timeout vid anrop till api.skolan.se
2026-09-21 11:45:21 WARNING Högt minnesanvändande

6. grep -E '07' kontakter.txt
Anna Svensson, anna.svensson@skolan.se, 070-123 45 67
Erik Johansson, erik.j@mail.com, 073-9876543
Omar Hassan, omar_h@skolan.se, 0701234567
Lisa Berg, lisa.berg@skolan, 072-111 22 33

7. grep -E .se kontakter.txt
Anna Svensson, anna.svensson@skolan.se, 070-123 45 67
Omar Hassan, omar_h@skolan.se, 0701234567

Lisa är inte med eftersom hennes e-postadress inte sluta på .se

8.  awk -F',' '/@/ {print $2}' kontakter.txt
 anna.svensson@skolan.se
 erik.j@mail.com
 omar_h@skolan.se
 lisa.berg@skolan

 Del 2

 1. sed 's/INFO/INFORMATION/' server.log

 2. sed 's/,/|/g' elever.csv Endast kommatecknet efter namnet ändras, medan kommatecknen mellan klass, program och poäng står kvar orörda

 3. sed '/INFO/d' server.log

 4. sed -n '2,4p' elever.csv

 5. sed '1d' elever.csv

 6.sed 's/^2026-09-21 //' server.log

 7. sed -E 's/[10-18]{2}:[10-18]{2}:[10-18]{2}/XX:XX:XX/' server.log

 Del 3

 1. 
 awk -F',' '{print $1}' elever.csv

 2.
awk '{print $3}' server.log

3. 
awk -F',' '{print $1 " har " $4 " poäng"}' elever.csv

4.
awk -F',' 'NR > 1 && $4 > 80 {print $1, $4}' elever.csv

5.
awk -F',' '$3 == "Natur" {print $1}' elever.csv

6.
awk 'END {print NR}' server.log

7. 
awk -F',' 'NR > 1 {sum += $4; count++} END {print sum/count}' elever.csv

8. 
awk -F',' 'NR > 1 {prog[$3]++} END {for (p in prog) print p ": " prog[p]}' elever.csv

Fem enradare - awk

1.
awk -F';' '$2=="drift" {print $1}' data.txt
 
 2.
awk -F ';' '{sum+= $3} END {print sum}' data.txt

3.
awk -F';' '$3>max {max=$3; namn=$1} END {print namn, max}' data.txt

4.
awk -F';' '{antal[$2]++} END {for (a in antal) print a, antal[a]}' data.txt

5.
awk -F';' 'substr($4,1,4) < 2020 {print $1, substr($4,1,4)}' data.txt

fem enrader - sed

1. 
sed -E 's/([0-9]{4})-([0-9]{2})-([0-9]{2})$/\3\/\2\/\1/' data.txt

2.
sed -e 's/;/ | /g' data.txt

3.
sed -E 's/^[a-z]/\u&/g' data.txt

4.
sed -E 's/([0-9]{5})/XXXXX/' data.txt

5.
 sed -E 's/;ekonomi;/;finans;/' data.txt

 PowerShell — de tre frågorna
 Jag använder: PSVersion 5.1.26100.1591

 Del 1 

 1. 1. Hur många kommandon finns det totalt på din maskin?
 1669

 2. Vilka kommandon gör något med processer? Du ska få en handfull, inte hundra.
Debug-Process, Get-Process,  Start-Process, Stop-Process, Wait-Process

3. Hur många kommandon börjar med verbet Get?
469

4. Vilka verb är godkända i PowerShell? Ta reda på skillnaden mellan Get och Read — de låter lika men betyder 
olika saker.
`Get` hämtar en resurs, `Read` läser från en källa.


5. Hur många kommandon kommer från modulen Microsoft.PowerShell.Utility?
107

6. Du minns att det finns något kommando med tjänster men inte vad det heter. Hitta alla som har med saken 
att göra, med ett enda kommando.

Get-Service
New-Service
Restart-Service
Resume-Service
Set-Service
Start-Service
Stop-Service
Suspend-Service

 Del 2

7. Vad gör Get-ChildItem, och vilka parametrar tar den?\
The `Get-ChildItem` cmdlet gets the items in one or more specified locations.

 - `Archive`
        - `Compressed`
        - `Device`
        - `Directory`
        - `Encrypted`
        - `Hidden`
        - `IntegrityStream`
        - `Normal`
        - `NoScrubData`
        - `NotContentIndexed`
        - `Offline`
        - `ReadOnly`
        - `ReparsePoint`
        - `SparseFile`
        - `System`
        - `Temporary`

		8. Visa bara exemplen för Get-Process. Det är oftast snabbaste vägen till ett användbart kommando.
		get-help get-process -examples
 
 9. Tar Stop-Process emot indata från pipen, och i så fall på vilken parameter? Svaret står i hjälpen — leta efter 
raden Accept pipeline input.
  Accept pipeline input?       false

10. Finns det ett hjälpämne om operatorer? De ämnena är inte kommandon utan begreppsförklaringar, och de 
heter något särskilt.
Get-Help about_Operators


 Del 3

11. Vilken objekttyp ger Get-Service? Det fullständiga namnet, inte "en tjänst".
System.ServiceProcess.ServiceController

12. Vilka egenskaper har ett sådant objekt? Lista bara egenskaperna, inte metoderna
Egenskaperna är vad objektet innehåller

13. Vilka metoder har det? Alltså: vad kan objektet göra, till skillnad från vad det innehåller.
Close                   
Continue                 
CreateObjRef            
Dispose                  
Equals                    
ExecuteCommand           
GetHashCode               
GetLifetimeService        
GetType                  
InitializeLifetimeService 
Pause                     
Refresh                  
Start                    
Stop                      
WaitForStatus

14. På Windows fungerar ls, cat och dir. Vilka riktiga cmdlets är det egentligen som körs?
Get-ChildItem, Get-Content

15. Skriv ett kommando som listar alla kommandon som både börjar med Get och har med tjänster att göra
Get-command -verb Get -noun service

16. Mät hur lång tid det tar att köra Get-Command utan filter, och jämför med samma sökning filtrerad direkt i 
kommandot. Vilken är snabbast, och varför?  

Det tog runt 20x längre med vanliga get-command, filtrerad är snabbare eftersom du söker inte i var ända modul efter kommandot.

Loggjakten — en gång till, i PowerShell

1. Hur många rader har loggen, och hur många unika IP-adresser förekommer? 

30 rader och 6 unika

2. Vilka IP-adresser står för flest anrop? Antal och adress, flest först. 

Count Name
----- ----
    8 203.0.113.45
    7 198.51.100.77
    6 192.168.10.14
    3 192.0.2.130
    3 192.168.10.52
    3 192.168.10.31

3. Hur många anrop gav varje statuskod?
Count Name
----- ----
   14 200
    5 401
    8 404
    3 403

  4. Vilka sökvägar gav 404, och hur många gånger var?  
    2 404, /wp-login.php
    1 404, /phpmyadmin
    1 404, /.env
    1 404, /backup.zip
    1 404, /config.php
    1 404, /.git/config
    1 404, /saknas.html

    5. 5. Vilken timme på dygnet hade flest anrop?

    Count Name
----- ----
    9 09
    7 10
    6 08
    5 11
    3 12

    6. Vilka är de tre mest efterfrågade sökvägarna? Samma tvetydighet finns kvar som förra gången — hitta den, 
och lös den.
    Count Name
----- ----
    6 /index.html
    4 /admin/login
    4 /admin

    7. Hur många byte har servern skickat totalt? Och i megabyte, med två decimaler?
    99916 bytes

    0.10 MB
    8. Vilka IP-adresser har fått 401 eller 403? Lista varje adress en gång.
    Count Name
----- ----
    8 203.0.113.45


9. En av IP-adresserna beter sig som en sårbarhetsskanner. Visa beviset med en pipe.

$logg |Where-Object { $_.Status -eq 404 }| Group-Object IP | Sort-Object Count -Descending | Select-Object Count,Name

Count Name
----- ----
    7 198.51.100.77
    1 192.0.2.130


10. $logg | Group-Object IP | Sort-Object count -Descending | Select-Object Count,Name | Tee-Object -FilePath topp.txt


 







