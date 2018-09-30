# Sviluppo HTML / CSS

L’obiettivo di questo documento è fornire un **metodo affidabile, ripetibile e veloce** per realizzare delle layout HTML e CSS di progetti complessi (ma non solo) che possono essere facilmente implementate dagli sviluppatori backend.

> “Un metodo è meglio di nessun metodo”

# Regole Generali

Questo metodo richiede l'applicazione di alcune regole generali:

- Usare sempre un framework CSS (es. Bulma.io).
- Scrivere estensioni generalizzate per estendere il framework scelto secondo necessità (es. spacing.scss : https://gist.github.com/filippotoso/2680b3d6fba8e7c1c93ddddef3322913).
- Scrivere il minore numero possibile di classi CSS specialistiche.
- Utilizzare la stessa convenzione per tutte le classi personalizzate (es. kebab-case con prefisso relativo al progetto - vedi poi).
- Evitare il più possibile l'utilizzo di selettori per #id (es. #about) e preferire classi e altre tipologie di selettori (es. tag, attributi, etc.).
- Usare sempre git per il controllo versione.

# Panoramica del Workflow

Il workflow operativo segue alcuni step logici che hanno l’obiettivo di evitare lo spreco di risorse e, al tempo stesso, ottenere una base di codice affidabile in ogni fase di sviluppo.

- Analisi delle layout
- Identificazione e indicizzazione degli elementi principali
- Sviluppo delle layout wireframe
- Sviluppo delle singole componenti
- Unione degli elementi in layout complete
- Revisione degli stili

# Struttura delle Cartelle

Il risultato finale sarà una serie di file HTML, CSS e JS (eventualmente). Questi file dovranno essere salvati in questa struttura di directory:

```
/
	/assets
		/assets/css
		/assets/js
		/assets/img
	/includes
		/includes/elements
		/includes/components
		/includes/contents

```

I file sono suddivisi come segue:

- */* (root del progetto): file con le layout wireframe;
- */assets* (e relative sottocartelle): css, javascript e immagini;
- */includes/elements*: elementi ripetuti (uno per file);
- */includes/components*: singoli componenti (uno per file);
- */includes/contents*: singoli blocchi di contenuto editoriale (uno per file);

Per comodità puoi scaricare questo mockup (TODO) per partire con il piede giusto.

# Workflow Dettagliato

Il primo step è analizzare tutte le layout del sito e:

- identificare le griglie che le costituiscono;
- individuare i macro elementi ripetuti (es. form filtro recensioni);
- individuare i singoli componenti ripetuti (es. box rating);
- individuare i singoli elementi tipografici (es. titoli, paragrafi, liste).

# Sviluppo Wireframe

Realizzare la struttura delle singole pagine inserendo nel file *structure.css* le sole classi che definiscono la struttura. Utilizzando un framework CSS il numero di classi personalizzate dovrebbe essere limitato al massimo.

In questa fase è importante utilizzare un CSS di debug per visualizzare al meglio la struttura della griglia in modalità desktop e mobile. Ref: https://gist.github.com/filippotoso/e01481c7290ec445fa00c6f39225814d

# Sviluppo Stili Tipografici

In questa fase, inserire nel file *typography.css* le sole classi che si riferiscono agli elementi tipografici.

Se l'indicizzazione è stata fatta correttamente, il numero di classi personalizzate dovrebbe essere limitata. Nella maggior parte dei casi, si dovrebbe poter far riferimento direttamente ai tag (es. H1, P, etc.) invece di creare delle classi ad-hoc per ogni singolo elemento tipografico.

Nel caso in cui lo stesso stile (es. H1 di tutte le pagine) richieda differenti attributi di spacing (es. margin, padding), creare delle specifiche classi ad-hoc (es. bi-title-spacing) invece di inserire tali attributi nell'elemento tipografico stesso.

Ad esempio, invece di scrivere questo:

```css
.bi-homepage-title {
    color: blue;
    /* ... */
    margin-top: 1rem;
}

.bi-aboutpage-title {
    color: blue;
    /* ... */
    margin-top: 0.5rem;
}
```

```html
<h1 class="bi-homepage-title">Hello World!</h1>
...
<h1 class="bi-aboutpage-title">Hello World!</h1>
```

Scrivere una cosa tipo:

```css
.bi-blue-title {
    color: blue;
    /* ... */
}

.bi-margin-top-medium {
    margin-top: 0.5rem;
}

.bi-margin-top-large {
    margin-top: 1rem;
}
```

```html
<h1 class="bi-blue-title bi-margin-top-large>Hello World!</h1>
...
<h1 class="bi-blue-title bi-margin-top-medium">Hello World!</h1>
```

Il tutto cercando sempre di utilizzare le classi già esistenti (es. quelle offerte dal framework) invece di crearne di nuove.

# Sviluppo Componenti

In questa fase, inserire nel file *components.css* le sole classi che si riferiscono ai componenti ripetuti.

Ogni componente dovrebbe avere un nome univoco, auto-esplicativo e prefissato da una breve stringa per evitare collisioni. Ad esempio, per il progetto Mario Rossi il prefisso potrebbe essere *"mr-"* (es. mr-slider) e per Acme Inc potrebbe essere *"ai-"* (es. ai-footer) e così via.

# Sviluppo Macro Elementi

In questa fase, inserire nel file *elements.css* le sole classi che si riferiscono ai macro elementi ripetuti.

In linea generale, sarebbe sempre meglio che ogni componente e macro elemento sia contenuto in un elemento radice (es. header, nav, article, section, aside, footer, div, etc.) a cui viene applicata una classe specifica. Questa classe sarà poi utilizzata come primo selettore nella creazione degli stili CSS. Ad esempio:

```html
<div class="mr-user-ratings">
    <h1>Hello World!</h1>
    <p>Lorem Ipsum...</p>
</div>
```

```css
.mr-user-ratings h1 {
    color: red;
}

.mr-user-ratings p {
    line-height: 1.85rem;
}
```

# Integrazione Contenuti nelle Layout

In questa fase, utilizzando una tecnologia server side, i componenti, i macro elementi e il resto dei contenuti vanno inseriti all’interno delle layout wireframe delle pagine realizzate.

È fondamentale che il codice HTML non venga semplicemente copiato all’interno delle layout perché questo aumenterebbe inutilmente il carico di lavoro degli sviluppatori backend e incrementerebbe il rischio di introdurre errori dovuti al lavoro manuale.

Per sviluppare nel modo più performante possibile è consigliabile utilizzare un web server locale (per evitare il continuo upload dei file). Se non hai un server a tua disposizione, più in basso troverai le istruzioni per scaricarne uno per le attività di sviluppo.

All’interno della sua document root (es. *public_html*) creiamo una cartella per il progetto dove metteremo tutti i file del nostro progetto.

Nei file di layout, invece di incollare i vari codici (elementi, componenti e contenuti), utilizzeremo la direttiva *include()* di PHP. Ad esempio:

```html
<html>
<body>
<?php include(‘includes/components/header.php’); ?>
<?php include(‘includes/components/navigation.php’); ?>
<?php include(‘includes/contents/home-page-body.php’); ?>
<?php include(‘includes/components/footer.php’); ?>
</body>
</html>
```

In questo modo, a prescindere dal numero di pagine che contiene elementi comuni (es. barra di navigazione, sidebar, etc.), tra tutti i file del progetto ve ne sarà sempre e solo una versione. Inoltre, qualsiasi modifica fatta a quella singola istanza sarà automaticamente visibile in tutte le pagine che la includono.

Nella fase di inserimento dei contenuti poi tenere sotto controllo a situazione semplicemente salvando il file e digitando CTRL + F5 nella finestra del browser. Questa si aggiornerà cancellando la cache e mostrando la modifica apportata.

# Server di Sviluppo

Se non disponi di un server di sviluppo, puoi trovarne uno stand-alone a questo indirizzo: [https://github.com/filippotoso/frontend-server](https://github.com/filippotoso/frontend-server)

Una volta scaricato l’archivio ed estrattone il contenuto, è sufficiente che copi all’interno della cartella *public_html* i file del progetto ed esegui lo script *server.bat*. Una volta fatto ciò, il tuo browser di default si aprirà automaticamente mostrando la lista dei file (o il file index.htm, etc.) a cui potrai accedere cliccando sui relativi link.

# Inclusione CSS

Nel sito finito, l’inclusione dei file CSS avverrà nel seguente ordine:

- *framework.css* (es. *bulma.min.css*)
- *structure.css*
- *typography.css*
- *elements.css*
- *components.css*
- *custom.css*

Il file *custom.css* include delle classi ad-hoc per gestire casi specifici che non trovano collocazione negli altri file. Mantenere una separazione rigorosa tra struttura, elementi tipografici, elementi ripetuti e componenti è fondamentale per disporre di una base di codice pulito, ordinato e facilmente mantenibile.

Ovviamente, prima della pubblicazione in produzione, verrà utilizzato un module bundler (es. *webpack*) che si occuperà di unire, minificare e mappare automaticamente i vari file CSS senza che un’attività manuale possa introdurre errori di sorta.

# Sviluppo Javascript

Nei casi in cui il codice Javascript sia meramente a supporto del frontend (es. slider, tabs, tooltips, etc.) è consigliabile inserire il codice all'interno del file HTML più rilevante. Ad esempio, se un componente richiede del codice Javascript di supporto, esso dovrà essere inserito in un tag *<SCRIPT>* in fondo al file che contiene il componente stesso.

Nel caso in cui la parte Javascript sia più consistente, è consigliabile creare una classe dedicata all'applicazione (es. App) che espone le singole funzionalità richieste dal sito. Questo permetterà di ridurre i tempi di sviluppo e mantenere una base di codice più pulita.
