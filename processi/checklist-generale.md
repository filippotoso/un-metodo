# Checklist Generale

**Modifiche Sistemistiche**
Prima di fare una modifica sistemistica, verificare la checklist di produzione e agire di conseguenza.

**Memoria Storica**
Ogni volta che viene presa una decisione che influenza lo sviluppo, il design o l’architettura del progetto su cui si sta lavorando, inserirla nel notebook Memoria Storica del gestore progetti.

**Proof Of Concept**
Ogni volta che si implementa un POC (proof of concept), pianificare altrettanto tempo e risorse per il refactoring.

**Sottodomini**
Tutti i sottodomini cPanel devono essere configurati in una cartella /subdomains/{subdomain}/public_html. La prima volta che si aggiunge un sottodominio, includere un file .gitignore per escludere i contenuti della cartella /subdomains.

**Ambiente di Test**
Per tutti i progetti che richiedono ambienti di sviluppo, staging e produzione separati, creare:

- Un account cPanel: {progetto}.example.com
- Un sottodominio staging.{progetto}.example.com
- Un sottodominio dev.{progetto}.example.com

Dove example.com è il proprio dominio aziendale o un dominio registrato ad-hoc per ospitare i siti dei clienti durante la fase di sviluppo.

Per i progetti che richiedono solo ambiente di sviluppo e produzione separati (es. relativamente piccoli siti WordPress), creare:

- Un account cPanel: {progetto}.example.com
- Un sottodominio dev.{progetto}.example.com
