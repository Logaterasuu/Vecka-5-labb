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
 







