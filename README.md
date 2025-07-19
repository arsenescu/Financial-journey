# Financial-journey
Acest notebook interactiv permite simularea și analiza plăților lunare pentru credite, luând în considerare factori precum IRCC, DAE, dobândă, durată și suma împrumutată. Aplicația oferă și o analiză comparativă anuală, completată de un comentariu generat automat pentru interpretarea variației costurilor.

1. Obiective
Să ofer o interfață simplă și intuitivă pentru introducerea parametrilor unui credit.

Să calculez automat costuri lunare și totale pentru credite.

Să compar evoluția acestor costuri de la un an la altul.

Să genereze o analiză de tip „AI asistent” (bazată pe reguli) pentru a interpreta automat variațiile semnificative.


2. Tehnologii folosite

a.Python 3.x

b.pandas, numpy – manipulare de date

c.ipywidgets – interfață interactivă în Jupyter Notebook

d.matplotlib – vizualizare variații

e.IPython.display – afișare widgeturi și tabele

f. AI Asistent-  funcție simplificată generează comentarii bazate pe variația costurilor:

- creșteri mari sunt marcate ca risc

- scăderile sunt marcate ca pozitive

- variațiile mici sunt considerate nesemnificative


3.Functii:

a. Interfața de input

Utilizatorul completează:

Anul simulării

Suma împrumutată

IRCC (%)

DAE (%)

Durata creditului (ani)

Dobânda anuală

b. Calculul automat
La apăsarea butonului „Adaugă rând”, aplicația:

Calculează durata în luni

Calculează rata lunară fixă (anuitate)

Afișează rata și suma lunară fixă

Adaugă noul scenariu în tabelul istoric

Recalculează variația totală de plată față de anul precedent (în %)

c. Afișare rezultate
Tabel complet cu toate datele introduse

Tabel de comparație cu variația medie anuală a costurilor

Calcule mediane pentru dobândă, DAE, rata lunară, variație

Comentariu AI bazat pe variație (alertă, recomandare, observație)

Grafic cu variația costurilor totale în timp


d. Analiza automată (AI simplificat)-funcția comentariu_ai() returnează automat un mesaj explicativ:

- Dacă variația este > 10%: avertisment privind creșterea semnificativă

- Dacă variația este negativă: semnal pozitiv pentru reducerea costurilor

- Dacă variația e mică: mesaj informativ fără alerta


## Instrucțiuni
Rulează notebook-ul în Jupyter.

Introdu valorile dorite pentru un nou credit.

Apasă Adaugă rând.

Vei vedea un tabel complet cu datele și un sumar vizual + text interpretativ.

Poti adăuga mai multe rânduri pentru a compara evoluția în ani diferiți.
