# Financial-journey
Acest notebook interactiv permite simularea și analiza plăților lunare pentru credite, luând în considerare factori precum IRCC, DAE, dobândă, durată și suma împrumutată. Aplicația oferă și o analiză comparativă anuală, completată de un comentariu generat automat pentru interpretarea variației costurilor.

1. Obiective
Să ofer o interfață simplă și intuitivă pentru introducerea parametrilor unui credit.

Să calculez automat costuri lunare și totale pentru credite.

Să compar evoluția acestor costuri de la un an la altul.

Să genereze o analiză de tip „AI asistent” (bazată pe reguli) pentru a interpreta automat variațiile semnificative.


2. Importuri

import pandas as pd
-> Pandas este o bibliotecă Python folosită pentru lucrul cu date tabelare (ex: Excel, baze de date, tabele CSV).
-> pd este aliasul sub care o folosim, ca să scriem mai scurt.
-> În proiectul meu o folosesc pentru a crea și gestiona tabelul de credite (DataFrame), ca în:

   "st.session_state.istoric = pd.DataFrame([...])"

import numpy as np
-> NumPy este o bibliotecă pentru calcul numeric performant.
-> Este adesea folosită pentru operații matematice sau pe matrice/vectoare.
-> În proiectul meu nu este încă folosită direct — e un import neutilizat, dar util dacă voi adăuga calcule mai avansate.


import matplotlib.pyplot as plt
-> NumPy este o bibliotecă pentru calcul numeric performant.
-> Este adesea folosită pentru operații matematice sau pe matrice/vectoare.
-> În proiectul meu nu este încă folosită direct — e un import neutilizat, dar util dacă vei adăuga calcule mai avansate.

import streamlit as st
-> Streamlit este biblioteca care transformă codul tău Python într-o aplicație web interactivă.
-> st e aliasul sub care accesez funcții ca:

st.title(), st.number_input(), st.dataframe() — pentru UI.

st.session_state — pentru stocarea datelor între interacțiuni.

st.button() — pentru acțiuni.


3. Setări inițiale pentru Streamlit

st.set_page_config(page_title="Calcul Credit", layout="wide")     -> Cconfigurează aspectul paginii Streamlit:

page_title="Calcul Credit"     —> setează titlul paginii (afișat în tab-ul browserului).

layout="wide" — lărgește layout-ul paginii, util pentru afișarea tabelelor și graficelor.

st.title("💰 Simulare Credit și Analiză    -> afișează titlul aplicației în partea de sus a paginii, cu un emoji sugestiv.


 Inițializare variabilă de sesiune (st.session_state)

if "istoric" not in st.session_state:
    st.session_state.istoric = pd.DataFrame(columns=[
        "an_", "suma", "ircc", "dae", "durata", "dobanda", "luni", "suma_lunara", "rata", "variatia"  
   
    ->st.session_state păstrează date între interacțiunile utilizatorului cu aplicația.
    ->st.session_state este folosit pentru a păstra datele între interacțiuni ale utilizatorului (fără să se piardă la fiecare reîncărcare).
    ->se creează o variabilă numită istoric — un tabel (DataFrame) cu coloane predefinite:
    ->dacă nu există deja o variabilă istoric, se creează una goală — un DataFrame cu coloanele pentru datele despre credite.

Coloana	Descriere
an_	Anul contractării creditului
suma	Valoarea totală a creditului
ircc	Indice de referință IRCC (%)
dae	Dobânda anuală efectivă (%)
durata	Durata creditului (în ani)
dobanda	Dobânda nominală anuală (%)
luni	Durata creditului exprimată în luni
suma_lunara	Suma medie rambursată lunar (principalul împărțit la luni)
rata	Rata lunară totală (inclusiv dobândă)
variatia	Variația procentuală a totalului plătit față de anul anterior


4. Inputuri utilizator (formular)

st.subheader("🔧 Introdu datele creditului")

col1, col2, col3 = st.columns(3)  -> creează o secțiune de input pentru utilizator cu 3 coloane.

an = col1.number_input("An", min_value=2000, max_value=2100, value=2025)
suma = col1.number_input("Suma credit")
ircc = col2.number_input("IRCC (%)")
dae = col2.number_input("DAE (%)")
durata = col3.number_input("Durata (ani)", min_value=1, max_value=50, value=10)
dobanda = col3.number_input("Dobândă (%)")

-> st.subheader(...) — afișează un subtitlu cu un emoji pentru a marca secțiunea de introducere a datelor.

-> st.columns(3) — împarte pagina în 3 coloane verticale, pentru o organizare mai clară a câmpurilor de input.

Explicația fiecărui câmp de input:
Variabilă	Etichetă UI	Descriere
an	"An"	Anul în care se accesează creditul
suma	"Suma credit"	Valoarea totală a împrumutului
ircc	"IRCC (%)"	Indice de referință pentru creditele în lei
dae	"DAE (%)"	Dobânda Anuală Efectivă (include toate costurile)
durata	"Durata (ani)"	Numărul de ani pentru rambursare (1-50)
dobanda	"Dobândă (%)"	Dobânda anuală nominală aplicată

-> number_input permite introducerea de valori numerice, cu validare (ex. minim/maxim).

def calculeaza_variatia(df):
    df = df.sort_values('an_')
    df['total_plata'] = df['rata'] * df['luni']  ->Calculează plata totală (total_plata) ca rata * număr luni.
   
    df['variatia'] = df['total_plata'].pct_change().fillna(0) * 100           ->Calculează variația procentuală a plății totale față de anul precedent (pct_change).
    return df

->Primele valori care nu au an anterior primesc 0.

pct_change() calculează procentul de variație față de anul anterior.

fillna(0) — pune 0 la prima linie (nu are cu ce să compare).

Această funcție ma ajută să vad cum costul total al creditului variază în timp.

6. Buton pentru adăugare credit    -> este elementul care „salvează” datele introduse.

if st.button("➕ Adaugă credit"):
    luni = calculeaza_luni(durata)
    rata = calculeaza_rata(suma, dobanda, luni)
    suma_lunara = suma / luni if luni > 0 else 0

    rand_nou = {
        "an_": an,
        "suma": suma,
        "ircc": ircc,
        "dae": dae,
        "durata": durata,
        "dobanda": dobanda,
        "luni": luni,
        "suma_lunara": round(suma_lunara, 2),
        "rata": round(rata, 2),
        "variatia": 0
    }

    st.session_state.istoric = pd.concat(
        [st.session_state.istoric, pd.DataFrame([rand_nou])],
        ignore_index=True
    )

    istoric_calc = calculeaza_variatia(st.session_state.istoric)
    st.session_state.istoric['variatia'] = istoric_calc['variatia'].values
Când se apasa butonul:

->Calculează:
-luni
-rata lunară
-suma lunară simplă (fără dobândă)

->Construiește un dicționar cu toate datele creditului.

->Adaugă noul rând în DataFrame-ul din sesiune.

->Actualizează variația plăților pentru toate creditele.

7. Afișare tabel cu credite

st.subheader("📋 Tabel credite introduse")
->Afișează un subtitlu (text mai mic decât st.title(), dar mai mare decât textul normal).
->Textul este „📋 Tabel credite introduse” — apare pe pagină ca un antet de secțiune.
->Este folosit în aplicația ta:
->Este plasat chiar înainte de afișarea tabelului cu toate creditele adăugate de utilizator:

df_afisat = st.session_state.istoric.copy()   -> creează o copie independentă a tabelului (DataFrame-ului) salvat în sesiunea Streamlit.

st.dataframe(df_afisat, use_container_width=True)  -> oferă un tabel interactiv: pot sorta coloane, derula, etc.

Copiază DataFrame-ul din sesiune și îl afișează într-un tabel interactiv pe pagină.

8. Recomandări AI simple pe baza datelor introduse

if len(df_afisat) > 0:
    st.subheader("🤖 Recomandări AI")
    med_dobanda = df_afisat["dobanda"].median()
    med_dae = df_afisat["dae"].median()

    if med_dobanda > 7:
        st.warning("💬 Dobânda medie este ridicată. Recomand negocierea unei dobânzi mai mici.")
    elif med_dobanda < 3:
        st.success("💬 Dobânda medie este scăzută. Credit avantajos.")
    else:
        st.info("💬 Dobânda medie este moderată.")

    if med_dae > med_dobanda + 1.5:
        st.warning("💬 DAE este semnificativ mai mare decât dobânda. Posibile costuri ascunse.")
Dacă există cel puțin un credit, calculează mediana dobânzii și DAE.

Afișează mesaje condiționate pentru utilizator (sfaturi bazate pe nivelul dobânzii și diferența DAE vs dobândă).


9. Grafic variație plăți

if df_afisat["an_"].nunique() > 1:
    st.subheader("📈 Variație total plata (%) pe ani")
    fig, ax = plt.subplots()
    df_sorted = df_afisat.sort_values("an_")
    ax.plot(df_sorted["an_"], df_sorted["variatia"], marker='o', color='purple')
    ax.set_xlabel("An")
    ax.set_ylabel("Variație (%)")
    ax.set_title("Evoluția variației totale")
    ax.grid(True, linestyle='--')
    st.pyplot(fig)
Dacă există date din cel puțin 2 ani diferiți, afișează un grafic linie.

-> Graficul arată variația procentuală a plăților totale în timp.

-> Folosește matplotlib pentru desenarea graficului.

-> Afișează graficul în aplicația Streamlit.


10 Pentru a porni aplicația web Streamlit:

Am deschis CMD și am intrat în directorul corect:
cd "C:\Users\arsen\OneDrive\Desktop\financial-journey"   -> folderul unde am scriptul main.py.

Am rulat aplicația Streamlit:
"streamlit run main.py"     ->  aceasta este comanda oficială pentru a porni aplicația web Streamlit.

Am primit ceva de genul
  C:\Users\arsen>cd "C:\Users\arsen\OneDrive\Desktop\financial-journey"

C:\Users\arsen\OneDrive\Desktop\FINANCIAL-JOURNEY>streamlit run main.py

      Welcome to Streamlit!

S-a  deschis browserul http://localhost:8501    

      

## Instrucțiuni
Rulează notebook-ul în Jupyter.

Introdu valorile dorite pentru un nou credit.

Apasă Adaugă rând.

Vei vedea un tabel complet cu datele și un sumar vizual + text interpretativ.

Poti adăuga mai multe rânduri pentru a compara evoluția în ani diferiți.
