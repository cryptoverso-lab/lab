# lab.cryptoverso.net — le rotte del libro

*Read this in [English](README.en.md).*

Questo repository serve un solo host: **[lab.cryptoverso.net](https://lab.cryptoverso.net)**, l'indirizzo stampato accanto a ogni QR code del libro *La matematica di chi perde* di Luigi Garone.

Non contiene contenuti. Contiene **rotte**: una cartella per ogni codice stampato, con dentro una pagina che rimanda al quaderno di calcolo corrispondente.

```
lab.cryptoverso.net/l01   →   Lab 1  su Google Colab
lab.cryptoverso.net/c01   →   Calcolatore 1 su Google Colab
lab.cryptoverso.net/codice →  la repository del codice
lab.cryptoverso.net/errata →  gli errori trovati dopo la stampa
```

## Perché esiste

Un QR stampato non si corregge più. Se i QR del libro puntassero direttamente a GitHub o a Colab, il giorno in cui uno di quei servizi cambia un indirizzo — o il giorno in cui il codice si sposta sotto un'altra organizzazione — ogni copia già stampata diventerebbe un vicolo cieco.

Puntando invece a un host nostro, **la destinazione resta modificabile per sempre**: si cambia una riga qui, e i QR già stampati continuano a funzionare. È la stessa ragione per cui i DOI esistono.

Per questo vale una regola sola, e non ha eccezioni:

> **Le rotte non si rinominano e non si cancellano.** Un codice pubblicato su carta è un impegno permanente. Se una destinazione muore, la rotta va fatta puntare altrove — non tolta.

## Come si aggiorna

Le pagine **non si scrivono a mano**: sono generate dalla repository di produzione del libro, dove vive l'elenco delle rotte insieme ai capitoli che le citano.

```bash
uv run python codice/figure/genera_redirect.py --sito
```

Quel comando riscrive le pagine, il file `CNAME` e l'indice, tutto a partire dalla stessa fonte da cui nascono i QR stampati. Poi il contenuto viene portato qui e pubblicato. Modificare una pagina direttamente in questo repository significa creare uno scostamento fra ciò che è stampato e ciò che è servito: alla generazione successiva la modifica sparisce, e nessuno si ricorda perché.

Lo stesso generatore contiene un blocco di sicurezza: **si rifiuta di produrre QR verso un dominio che non risolve in DNS**. Un QR stampato su un nome che non esiste è l'errore più costoso di tutta la produzione, perché si scopre solo a libro rilegato.

## Com'è fatta una rotta

Una pagina, senza JavaScript, senza dipendenze:

- un `<meta http-equiv="refresh">` che porta a destinazione immediatamente;
- un `<link rel="canonical">` verso la stessa destinazione, così i motori di ricerca indicizzano il quaderno e non la rotta;
- un collegamento visibile, per chi ha il rinvio automatico disattivato o arriva con una connessione lenta.

Il rinvio è dichiarato in chiaro: chi apre la pagina vede dove sta andando prima di arrivarci.

## Infrastruttura

Servito da **GitHub Pages** su dominio proprio: il file `CNAME` dichiara `lab.cryptoverso.net`, e il record DNS del sottodominio è un CNAME verso `cryptoverso-lab.github.io`. Il file `.nojekyll` impedisce a Jekyll di ignorare i percorsi che cominciano con un trattino basso.

## Dove sta il resto

Il codice del libro — motore di calcolo, quaderni, dati congelati, generatori delle figure — è in **[cryptoverso-lab/matematica-di-chi-perde](https://github.com/cryptoverso-lab/matematica-di-chi-perde)**, insieme al generatore di queste pagine.

## Licenza

MIT, come il codice del libro.

---

<div align="center">

<br>

<img src="assets/cryptoverso-logo.svg" alt="Cryptoverso" width="56">

**Luigi Garone — [Cryptoverso](https://cryptoverso.net)**

</div>
