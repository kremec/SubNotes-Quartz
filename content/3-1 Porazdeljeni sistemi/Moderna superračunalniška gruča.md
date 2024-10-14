![[Moderna superračunalniška gruča-Image-2.png]]
**Glavno vozlišče**: koordinira gruščo
Podatke iz osebnega računalnika preko **prijavnega vozlišča** kopiramo na **podatkovna vozlišča**, **računska vozlišča** te podatke nato obdelujejo
### Simple Linux Utility for Resource Management
Vmesna programska oprema (middleware) - most med OS in uporabniško programsko opremo:
- upravljanje in dodeljevanje virov na gruči
- razvrščanje poslov, upravljanje čakalne vrste
- okolje za zaganjanje, izvajanje in nadziranje poslov
#### Arhitektura
- **slurmctrld**: glavno vozlišče - nadzira in dodeljuje vire, upravlja s čakalnimi vrstami
- **slurmd**: vsa vozlišča - čaka na posel, poskrbi za izvedbo, sporoča statuse
- **slurmstepd**: računska vozlišča - izvede posel
- **slurmdbd**: podatkovna vozlišča - dostopa do baze, shranjuje zgodovino
#### Delovanje
1. Uporabnik z ukazom `srun` pošlje zahtevo za dodelitev virov za posel, `slurmctrld` jo mora odobriti
2. `srun` po odobritvi pošlje zahtevo za vzpostavitev posla, `slurmctrld` izda poverilnice (gesla, dodeljene vire)
3. `srun` odpre komunikacijske kanale
4. `srun` pošlje poverilnice in podrobnosti o poslu na `slurmd`
5. `slurmd` podatke posreduje dodeljenim vozliščem
6. `slurmd` zažene `slurmstepd`
7. `slurmstepd` vzpostavi kanal z `srun` (na prijavnem vozlišču) in zažene posel (naloge v njem)
8. `slurmstepd` obvesti `srun` o zaključku posla
9. `srun` o zaključku posla obvesti `slurmctrld`
10. `slurmctrld` preko `slurmd` preveri, da je posel zaključen, in sprosti vire
#### Življenjski cikel posla
![[Moderna superračunalniška gruča-Image-3.png|500]]
**PD**: pending / **R**: running / **S**: suspended / **CA**: canceled / **TO**: timeout / **CG**: completing / **CD**: completed / **F**: failed / **CF**: configuring / **NF**: node failure / **RV**: revoked / **SE**: special exit state