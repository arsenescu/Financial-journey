# Financial-journey
Acest notebook interactiv permite simularea și analiza plăților lunare pentru credite, luând în considerare factori precum IRCC, DAE, dobândă, durată și suma împrumutată. Aplicația oferă și o analiză comparativă anuală, completată de un comentariu generat automat pentru interpretarea variației costurilor.

1. Tehnologii folosite

Python 3.x

pandas, numpy – manipulare de date

ipywidgets – interfață interactivă în Jupyter Notebook

matplotlib – vizualizare variații

IPython.display – afișare widgeturi și tabele

AI Asistent
O funcție simplificată generează comentarii bazate pe variația costurilor:

🔺 creșteri mari sunt marcate ca risc

🔻 scăderile sunt marcate ca pozitive

➖ variațiile mici sunt considerate nesemnificative

2. Obiective
Să ofer o interfață simplă și intuitivă pentru introducerea parametrilor unui credit.

Să calculez automat costuri lunare și totale pentru credite.

Să compar evoluția acestor costuri de la un an la altul.

Să genereze o analiză de tip „AI asistent” (bazată pe reguli) pentru a interpreta automat variațiile semnificative.

📌 Ce poți face cu acest notebook?
✅ Simulezi și adaugi mai multe scenarii de credit (pe ani diferiți)
✅ Vezi instant rata lunară, suma totală plătită și variația față de anul precedent
✅ Obții mediana dobânzilor, DAE și costurilor lunare
✅ Primești comentarii generate automat privind creșterea/scăderea costurilor
✅ Vizualizezi variația costurilor în timp într-un grafic ușor de interpretat

⚙️ Tehnologii utilizate
Bibliotecă	Scop
pandas	Manipulare și analiză de date tabelare
numpy	Calcule numerice și tratări ale valorilor lipsă
ipywidgets	Interfață interactivă pentru utilizator
matplotlib	Vizualizări grafice
IPython.display	Afișarea dinamică a tabelelor și rezultatelor

🖱️ Cum funcționează
1. Interfața de input
Utilizatorul completează:

Anul simulării

Suma împrumutată

IRCC (%)

DAE (%)

Durata creditului (ani)

Dobânda anuală

2. Calculul automat
La apăsarea butonului „Adaugă rând”, aplicația:

Calculează durata în luni

Calculează rata lunară fixă (anuitate)

Afișează rata și suma lunară fixă

Adaugă noul scenariu în tabelul istoric

Recalculează variația totală de plată față de anul precedent (în %)

3. Afișare rezultate
Tabel complet cu toate datele introduse

Tabel de comparație cu variația medie anuală a costurilor

Calcule mediane pentru dobândă, DAE, rata lunară, variație

Comentariu AI bazat pe variație (alertă, recomandare, observație)

Grafic cu variația costurilor totale în timp

🧠 Analiza automată (AI simplificat)
Funcția comentariu_ai() returnează automat un mesaj explicativ:

- Dacă variația este > 10%: avertisment privind creșterea semnificativă

- Dacă variația este negativă: semnal pozitiv pentru reducerea costurilor

- Dacă variația e mică: mesaj informativ fără alerta

5. Funcționalități


a.Permite introducerea datelor financiare despre un împrumut (credit):

Anul contractării

Suma împrumutată

IRCC (indice de referință)

DAE (dobânda anuală efectivă)

Durata în ani

Dobânda anuală

Calculează variatia

Afișează tabel cu istoricul

Afiseaza mediana si tabelul de comparatie ani 

 Oferă consiliere financiară automată


Introducerea parametrilor unui credit: an, sumă, IRCC, DAE, durată, dobândă

Calcul automat

Număr luni

Rată lunară

Suma lunară fixă

Variația totală de plată față de anul precedent

Afișarea unui tabel interactiv cu toate datele

Afișarea variației medii anuale (%)

Grafic de variație anuală

Comentariu generat automat (AI simplificat) pentru interpretarea variației

## Instrucțiuni
Rulează notebook-ul în Jupyter.

Introdu valorile dorite pentru un nou credit.

Apasă Adaugă rând.

Vei vedea un tabel complet cu datele și un sumar vizual + text interpretativ.

Poți adăuga mai multe rânduri pentru a compara evoluția în ani diferiți.
