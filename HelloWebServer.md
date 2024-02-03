# x) Artikkelitiivistelmät 

# Name-based Virtual Host Support

- IP-pohjainen virtuaali-isäntä käyttää yhteyden IP-osoitteita oikean virtuaali-isännän määrittämiseen ja tätä varten jokaisella samassa yhteydessä olevalla isännällä on oltava erillinen IP-osoite, jotta se voisi palvella oikeaa isäntää.
- Nimipohjaisessa virtuaali-isännöinnissä palvelin luottaa siihen, että käyttäjä määrittää itse kunkin isännän nimen HTTP-otsikoinnissa ja tämän myötä moni eri isäntä voi jakaa keskenään saman IP-soitteen.
- Nimipohjainen virtuaali-isännöinti on helpompaa veraattuna IP-pohjaiseen isännöintiin, koska käyttäjän tarvitsee vain määrittää DNS-palvelin yhdistämään jokainen eri virtuaali-isäntä oikeaan IP-soitteeseen nimen perusteella ja sen jälkeen määrittää Apachen HTTP-palvelin tunnistamaan eri isännät.
- Nimipohjainen virtuaali-isännöinti perustuu IP-pohjaisen virtuaalipalvelimen valinta-algoritmiin, joka tarkoittaa sitä, että oikea palvelin etsitään vain virtuaalisten isäntien väliltä IP-osoitteen mukaan.
- Palvelin valitsee sopivan nimipohjaisen virtuaali-isännän siten, että nimipohjainen IP-resoluutio valitsee vain sopivimman virtuaali-isännän parhaan IP-osoitteen mukaan.
- Kun pyyntö tulee palvelimelle, palvelin löytää parhaiten vastaavan <VirtualHost>-argumentin perustuen pyynnön lähettäjän IP-osoitteeseen ja sen käyttämään porttiin.
- Jos useampi kuin yksi isäntä jakaa saman IP-osoitteen ja portin, Apache vertaa edelleen niiden ServerName- ja ServerAlias-tietoja palvelimen nimeen.
- Jos vastaavaa ServerName- tai ServerAlias-nimeä ei löydy, käytetään ensimmäistä vastaavaa palvelinta
- Kun nimipohjaista virtuaali-isäntiä aletaan luomaan, ensimmäiseksi luodaan <VirtualHost>-lohko jokaiselle eri isännälle ja sen sisälle vähintään ServerName-käskyn, joka määrittää mitä isäntää palvellaan, ja sen lisäksi DocumentRoot-käskyn, joka näyttää, missä tiedostojärjestelmässä kyseisen isännän tiedot sijaitsevat
- Myös ServerAlias-komento on hyvä olla, jos haluaa että palvelin on käytettävissä usealla eri nimellä

# Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address

Tässä artikkelissa kerrotaan, kuinka voidaan luoda monta eri web-sivua saman IP-osoitteen alle. Seuraavaksi kerrotaan askel askeleelta, miten se käytännössä tehdään.
- Ensimmäiseksi asennetaan Apachen web-serveri komennolla:
     $ sudo apt-get -y install apache2
