# Segmentacija i filtriranje oblaka točaka za izolaciju stabala primjenom strojnog učenja

Diplomski rad — **Lovro Ružman**, FERIT Osijek, 2026.

Cilj rada je **izdvajanje niske vegetacije (trave)** iz oblaka točaka snimljenih iz
prizemne perspektive. Uspoređuju se **tri metode podjele** oblaka na patcheve
(pohlepna, FPS i nasumična), **četiri arhitekture** dubokog učenja (PointNet,
PointNet++, RandLA-Net, DGCNN) te klasična metoda **RANSAC** kao referentna
usporedba. Oblaci se dijele na 4 klase: deblo, grane, potpora i trava.

---

## 📦 Skup podataka

Skup podataka (izvorni oblaci i unaprijed izrezani patchevi) dostupan je ovdje:

### **[⬇️ Preuzmi skup podataka](https://puh.srce.hr/s/exFQfwHmrWJKANc)**

---

## Što se nalazi u repozitoriju

- **`Dataset*.ipynb`** — skripte za podjelu oblaka na patcheve od 8000 točaka
  (`DatasetGreedy`, `DatasetFPS`, `DatasetRandom`).
- **`<Podjela>_<Model>.ipynb`** — bilježnice za treniranje i testiranje svake
  kombinacije metode podjele i arhitekture (npr. `Random_RandLANet.ipynb`,
  `FPS_DGCNN.ipynb`). Za lakše modele postoje i varijante s većom veličinom grupe
  (`*_BatchSize16`, `*_BatchSize8`).
- **`RANSAC.ipynb`** — klasična geometrijska metoda za izdvajanje trave i usporedbu
  s modelima.

---

## Kako se pokreće

Bilježnice se pokreću **blok po blok, od vrha prema dnu**. Blokovi su podijeljeni na:

1. **Konfiguracija** — putanje i hiperparametri.
2. **Učitavanje podataka** — učitavanje patcheva, normalizacija boje, augmentacija.
3. **Definicija modela** — arhitektura mreže.
4. **Podjela podataka** — na treniranje, validaciju i testiranje (po stablima).
5. **Treniranje** — uz funkciju gubitka, rano zaustavljanje i spremanje najboljeg modela.
6. **Testiranje** — rekonstrukcija stabala iz patcheva i izračun metrika.

> ⚠️ **Prije pokretanja potrebno je prilagoditi putanje** do podataka
> (`DATASET_PATH` i putanje do spremljenih modela) u prvom bloku svake bilježnice,
> ovisno o tome gdje je skup podataka spremljen.

---

## Okruženje

Svi su eksperimenti provedeni na istom računalnom sustavu, kako bi mjerenja vremena
i usporedba računalne zahtjevnosti bili pošteni:

- procesor **AMD Ryzen 5 3600**
- grafička kartica **NVIDIA GeForce RTX 2070**
- **32 GB DDR4 radne memorije (3200 MHz)**

Modeli dubokog učenja izvršavani su uz ubrzanje na grafičkoj kartici. Radi
ponovljivosti rezultata, svugdje je gdje je moguće korišten fiksni sjemenski broj
(*seed*) vrijednosti **42**.
