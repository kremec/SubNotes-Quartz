Platforma za avtomatizirano nameščanje, skaliranje in upravljanje z vsebniki:
- izvajanje ==vsebnikov (containers)== na gruči ==gostiteljev (nodes)==
- avtomatska razporeditev vsebnikov na ustrezne gostitelje
- preverjanje vitalnosti (health check) vsebnikov
- avtomatsko horizontalno sklariranje vsebnikov preko metrik (npr. poraba CPU, ...)

V primeru izpada:
- vsebnika $\rightarrow$ vnovičen zagon
- gostitelja $\rightarrow$ prerazporeditev vsebnikov

Namestitvena datoteka - yaml: verzija + objekti
### Strukture
- ==strok (pod)==: 

- ==gostitelj (node)==: vozlišče v gruči, na katerem se izvajajo stroki
- ==imenski prostor (namespace)==: prepona imen virov omogoča deljenje gruče in organizacijo projektov
- ==preverjanje znanja (health check)==: sistem periodičnega preverjanja dostopnosti storitev in nadomeščanja nedelujočih replik
- ==skrivnosti (secrets)==: občutljivi podatki
![[Kubernetes-Image-1.png|400]]
### Namestitvene enote
#### Strok (pod)
Najmanjša namestitvena enota: atomarna enota enega/več vsebnikov
Vsebniki znotraj stroka si delijo: shrambo, IP naslov in vrata
Opcijski komponenti:
- ==nosilec podatkov (volume)==: imenik vsebnika, ki se preslika v imenik na gostiteljevem datotečnem sistemu
- ==označba (label)==: oznake strokov za identifikacijo / grupiranje

Ne kreiramo jih neposredno
#### Namestitev (deployment)
Deklarativni nadzor:
- namestitev in posodobitev strokov in replikacijskih nizov
- samodejna vzpostavitev ob izpadih
- upravljanje replik

Ne glede na lokacijo posameznih strokov je namestitev storitve dostopna na statičnem IP
#### Replikacijski nadzornik (replication controller) in replikacijski niz (replica set)
Zagotavlja, da v nekem trenutku teče zahtevano št. replik stroka - odstranitev odvečnih / zagon dodatnih replik
Samodejna nadomestitev strokov:
- izpad zaradi napake pri delovanju
- izbris / ustavitev stroka

Uporabimo, če ni zahteve po posodobitvah, sicer uporabimo namestitev
### Storitev (service)
Abstrakcija logičnega nabora strokov - politika dostopa (spremembe arhitekture ne smejo vplivati na odjemalce)
Tipi storitev:
- ==ClusterIP== (privzeto): storitev znotraj gruče dostopna na IP naslovu
- ==NodePort==: storitev izpostavljena na vratih na IP naslovu gostitelja $\rightarrow$ vsak gostitelj v gruči ločeno
- ==LoadBalancer==: storitev na voljo na porazdeljevalcu obremenitve
### Gruča
#### Kubernetes master
Vozlišče s komponentami za upravljanje gruče:
- kube-apiserver: izpostavlja Kubernetes API, hrani stanje gruče
- kube-controller-manager: izvaja nadzor stanja gruče preko API
- kube-scheduler: iskanje in določanje vozlišč za izvajanje strokov
#### Kubernetes node
Ena/več instanc vozlišč z izvajalnim okoljem:
- kube-proxy: izpostavlja storitve definirane v apiserver-ju - posredovanje TCP/UDP tokov
- kubelet: primarni agent za vzdrževanje strokov na vozlišču glede na specifikacije (yaml)
### kubectl
- `kubectl create -f conf.yaml` ... ustvari okolje iz konfiguracijske datoteke
- `kubectl get pods` ... prikaži vse stroke
- `kubectl describe pod y` ... prikaži opis stroka
- `kubectl proxy` ... dostop do GUI