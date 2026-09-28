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
