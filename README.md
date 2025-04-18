Weather Pipeline
Weather Pipeline on Google Colab -ympäristössä toteutettu koneoppimisprojekti, joka hyödyntää Helsingin säähistoriaa vuosilta 2013–2023. Projektissa noudetaan säädata Open-Meteo API:sta (avoin rajapinta, joka ei vaadi API-avainta) Helsingin alueelta, esikäsitellään data (mm. lasketaan päivittäiset keskilämpötilat ja luodaan viivästetyt piirteet), ja koulutetaan lineaarinen regressiomalli ennustamaan lämpötilaa. Mallin tarkkuutta arvioidaan (esim. virhemittarein kuten MSE ja $R^2$) ja tulokset visualisoidaan. Notebook tallentaa lopuksi koulutetun mallin tiedoston (models/-kansioon) ja tuottaa ennusteen kuvaajana (outputs/-kansioon). 
Projektin päävaiheet
Datan haku: Projekti hakee historiatiedot Helsingin säästä vuosilta 2013–2023 Open-Meteo-rajapinnan kautta. Data sisältää päivän säämuuttujia, joista tässä keskitytään lämpötilaan.
Esikäsittely: Raakadatan pohjalta lasketaan päivittäinen keskilämpötila, jos data on tuntitasolla. Lisäksi luodaan viivästettyjä piirteitä eli lisätään ennustemallille syötteiksi aiempien päivien lämpötiloja (esimerkiksi edeltävä päivän lämpötila), jotta malliin tuodaan ajallista riippuvuutta.
Mallin koulutus: Esikäsitellystä datasta erotellaan osa mallin kouluttamiseen (training data) ja osa testaamiseen (testidata). Mallina käytetään lineaarista regressiota (scikit-learn-kirjaston LinearRegression), joka oppii ennustamaan seuraavan päivän keskilämpötilan aiempien päivien arvojen perusteella.
Mallin arviointi: Koulutettua mallia testataan ennustamalla tunnettuja lämpötiloja testidatalle. Mallin ennusteita verrataan toteutuneisiin arvoihin ja lasketaan arviointimittareita (kuten keskimääräinen neliövirhe MSE sekä selitysaste $R^2$) mallin suorituskyvyn mittaamiseksi.
Visualisointi ja tallennus: Mallin ennustetulokset visualisoidaan kuvaajana. Esimerkkinä piirretään ennustettu lämpötilakäyrä verrattuna toteutuneeseen lämpötilaan valitulta ajanjaksolta, jotta nähdään, kuinka hyvin malli seuraa todellista kehitystä. Lopuksi pipeline tallentaa koulutetun mallin (serialized model) models-hakemistoon ja tallentaa ennustekaavion kuvana outputs-hakemistoon.

Kuva 1: Lineaarisen mallin tuottama ennustekäyrä (sininen) verrattuna toteutuneisiin lämpötiloihin (oranssi) vuoden 2023 lopussa.
Käyttöohjeet
Projektia on helppo kokeilla itse Google Colab -ympäristössä. Voit avata interaktiivisen Jupyter-muistikirjan napsauttamalla yllä olevaa “Open in Colab” -painiketta. Tämän jälkeen:
Kun Colab-muistikirja avautuu, valitse “Run all” (Aja kaikki) tai suorita solut yksitellen ylhäältä alas. Notebook huolehtii datan noutamisesta, esikäsittelystä ja mallin koulutuksesta automaattisesti.
Seuraa muistikirjan tulostamia viestejä ja kuvaajia. Datan lataus Open-Meteo-rajapinnasta tapahtuu ohjelmallisesti (ilman erillistä avainta) heti ensimmäisissä soluissa.
Mallin koulutuksen valmistuttua näet tulostettuna mallin arviointimittareita, jotka kertovat ennusteen tarkkuudesta. Myös ennusteen kuvaaja piirretään automaattisesti muistikirjaan.
Notebook tallentaa lopuksi koulutetun mallin tiedostoon models-kansioon sekä ennusteen kuvana outputs/temperature_forecast.png. Voit ladata nämä tiedostot itsellesi tai löytää ne Colabin tiedostoselaimesta vasemmalta (kirjauduttaessa Google-tilillä).
Halutessasi voit muokata lähdekoodia – esimerkiksi vaihtaa paikkakuntaa (muuttamalla API-kyselyn koordinaatteja) tai säätää mallin parametreja – ja ajaa solut uudelleen nähdäksesi vaikutukset ennusteeseen.
Kehitysideoita
Jatkossa projektia voisi laajentaa ja parantaa monin tavoin, esimerkiksi:
Ennustemallin parantaminen: Kokeile muita mallityyppejä (esim. päätöspuut, satunnaismetsä tai neuroverkot) lineaarisen mallin rinnalla ja vertaile niiden suorituskykyä.
Lisäpiirteiden hyödyntäminen: Tuota monipuolisempia piirteitä ennusteen pohjaksi – esimerkiksi mukaan voisi ottaa sademäärän, tuulen nopeuden tai edellisten päivien keskiarvo-/minimi-/maksimilämpötilat tuomaan lisätietoa mallille.
Aikajänteen laajentaminen: Kokeile ennustaa useampia päiviä eteenpäin (esim. 7 päivän sääennuste) käyttämällä sekvenssimalleja tai liukuvan ikkunan menetelmää. Tämä toisi esiin mallin kyvyn pidemmän aikavälin ennusteisiin.
Mallin automaattinen päivitys: Integroi pipelineen toiminnallisuus, joka noutaa uutta säähavaintodataa päivittäin ja päivittää mallin säännöllisesti, jotta ennuste pysyy ajan tasalla.
Visualisointien kehitys: Lisää interaktiivisia tai informatiivisempia visualisointeja – esimerkiksi graafeja, joista käyttäjä voi valita aikavälin, tai ennusteen ja toteutuneen erojen kuvaajia.
Lisenssi
Tämän projektin sisältö on vapaa tutkimus- ja oppimiskäyttöön. Voit vapaasti hyödyntää, jakaa ja muokata materiaalia ei-kaupallisissa tarkoituksissa. Tämä README ja siihen liittyvä koodi on tarjolla sellaisenaan ilman takuuta. Usein viitattaessa toivotaan mainittavan lähde. Kiitos!
