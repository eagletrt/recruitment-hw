# Componentistica
    - LM25085 buck switching controller
    - IRF9383M P-Channel power MOSFET
    - Diodo Schottky B330
Tutti i link ai Datasheet sono accessibili dallo schema elettrico in Kicad

# Informazioni sul dimensionamento dei componenti del Buck converter

    Questo documento contiene informazioni sintetiche sui componenti usati e calcoli fatti
    secondo datasheet.
    In particolare:
        - On-Time
        - Frequenza di switching
        - Limitazione della corrente in uscita
        - Tensione in uscita
        - Filtro passa basso LC

## Calcolo del tempo Ton e fissaggio di alcune variabili

    La frequenza di switching è stata fissata a 300Kohm
    Altre informazioni e dati sono accessibili nel file 'Calcolo RT e Ton.ipynb'

## Tensione in uscita 

    La tensione in uscita in funzione della rete di feedback composta da Rfb1 ed Rfb2 secondo la relazione:

        Vout = 1.25 * (Rfb1+Rfb2) / Rfb1

    Il rapporto Rfb2/Rfb1 è quindi:

         Rfb2/Rfb1 = Vout/1.25

    Le due resistenze secondo datasheet vanno scelte in un range che va da 1kΩ a 20kΩ e che soddisfano tale rapporto


    

