**Java**
È ***imperativo*** quindi il programma viene visto come una sequenza di istruzioni. ***Ad oggetti*** quindi possiamo creare entità che incapsulano dati e funzioni. Inoltre è:
- ***Fortemente tipizzato, interpretato, portabile***.

**Gestione della Memoria**
Java usa la filosofia `Smalltalk` quindi:
- L'allocazione è fatta dal programmatore tramite keyword `new` mentre la deallocazione è gestita dal garbage collector.

**Ambiente di Sviluppo**
Per programmare in Java serve il `JDK` che comprende:
- ***Compilatore:*** `javac` produce bytecode da passare all'interprete e file `.class`
- ***Interprete:*** Legge il bytecode riga per riga e produce l'output del programma senza creare un file eseguibile.
- ***Debugger***

**Classi ed Istanze**
- ***Tipi Primitivi:*** `byte, short, int, long, float, double, char (2 byte).`
- ***Tipi Riferimento:*** Oggetto di una classe referenziato da una variabile. `null` se indichiamo nessun riferimento.

**Assegnamento**
Viene fatto tramite l'operatore `=`
- `l-value = r-value` dove `l-value` è una variabile ed `r-value` una espressione.
- ***Esempio:*** `a = 5.`

**Casting**
Il cambio forzato del tipo di una variabile. Il cast è necessario se l'assegnamento produce perdita di informazioni.

``` Java
int i;
float f = 5.15F;
i = (int)f;
```

**Operatori**
- ***Aritmetici:*** `(+), (-), (*), (/), (%), (++), (--).`
- ***Booleani:*** `(!), (&&), (||).` Funzionano in cortocircuito.
- ***Bitwise:*** `(|), (&), (>>), (<<).`
- ***Confronto:*** `(==), (!=), (>), (<), (>=), (<=).`

**Blocco di Istruzioni**
Un blocco è un insieme di istruzioni rinchiuso tra parentesi graffe.
- Può essere vuoto.

**Costrutto Condizionale - IF**
Esegue un blocco di istruzioni se è VERA altrimenti viene ignorato.
- La keyword `else` fa eseguire un altro blocco se la condizione è FALSA.

``` Java
if (a > 10)
   {b = 1;}
else
   {b = 0;}
```

**Costrutto Condizionale - SWITCH**
Viene eseguito il blocco corrispondente al valore della variabile.
- Senza `break` vengono eseguiti tutti i blocchi a partire dal primo eseguito.

``` Java
String day = "Monday";

int dayOfWeek = switch(day)
{
	case "Monday" -> 1;
	case "Tuesday" -> 2;
	...
	default -> -1;
} ;
```

**Costrutto Iterativo - FOR**
Esegue l'assegnamento iniziale. Se la condizione è vera allora viene eseguito il blocco di istruzioni. Alla fine di una iterazione viene eseguito l'incremento.

``` Java
for (int i = 0; i < 10; i++)
	{a = a * 2;}
```

**Costrutto Iterativo - WHILE**
Esegue il blocco di istruzioni finchè la condizione è vera.

``` Java
while (i < 10)
	  {i++;}
```

**Costrutto Iterativo - DO-WHILE**
Simile al `while` ma la condizione viene testata dopo l'esecuzione del blocco.
- Il blocco viene eseguito minimo una volta.

**Funzioni**
Sono i metodi. Possono essere definiti solo all'interno di una classe.
- Possono esistere metodi con lo stesso nome ma parametri diversi.

``` Java
int somma (int a, int b)
	{return a + b;}
```

**Commenti**
In Java è possibile commentare in tre modi:
- ***C:*** `/* */ - più righe.`
- ***C++:*** `// - una riga.`
- ***Documentazione:*** `/** */ - più righe.`

**Classe**
Insieme di variabili e metodi. È un template che serve per definire oggetti con variabili e metodi uguali a quelli della classe.
- Gli oggetti vengono creati con la keyword `new.`

**Classe Wrapper**
Classe contenitore. In Java abbiamo `Byte, Short, Integer...` e sono utili per trattare i tipi primitivi come oggetti.

**Metodo Costruttore**
Ogni classe ha uno o più metodi **speciali** che servono per inizializzare l'oggetto.
- Stesso nome della classe, non c'è un valore di ritorno e possono essere più di uno a patto che abbiano parametri diversi.
- ***Costruttore Default:*** Se il programmatore non ne aggiunge si ha un costruttore con corpo vuoto e no parametri.

``` Java
class Contatore // Classe                    
{
	private int val; // Stato
	
	public Contatore() {val = 0;} // Costruttore
	
	// Interfaccia
	
	public void setVal(int newVal) {val = newVal;}
	public void inc() {val++;}
	public int getVal() {return val;}
}
```

**Creazione Oggetto**
`cont` è una variabile che contiene il riferimento ad un'area di memoria nella quale l'oggetto creato con `new` è contenuto.

``` Java
Contatore cont;
cont = new Contatore();
```

**Main**
Il main di un programma Java è il seguente:
- `public static void main(String args[])` - il metodo può creare oggetti ed invocare i suoi metodi.

**Compilazione vs Interpretazione**
Java usa un misto di **compilazione** (più veloce, meno portabile) e **interpretazione** (maggiore portabilità, molto lento).
- Crea il **bytecode** che è un formato intermedio ed è più leggero da interpretare rispetto ad ogni sorgente, mantenendo portabilità.

Il sorgente Java viene compilato tramite `javac:`
- `javac nomefile.java` - produce il file contenente il bytecode della classe con estensione `.class`

Il bytecode del main per essere eseguito viene poi interpretato usando il nome della classe e NON del file.
- `java nomeclasse`

**Stampa**
Classe `System,` variabile predefinita `out,` metodo `println().`
- `System.out.println();

**Primo Programma**

``` Java
public class PrimoEsempio
{
	public static void main(String args[])
	{
		Contatore c;
		c = new Contatore();
		
		c.setVal(0);
		c.inc();
		
		System.out.println(c.getVal());
	}
}
```
`
**Stringhe**
In Java sono classificate come oggetti. Non sono buffer modificabili come in C. Per memorizzare stringhe modificabili bisogna usare la keyword `StringBuffer.`
- La selezione di un carattere si fa attraverso il metodo `charAt().` 

``` Java
String s = "ciao";
String s = "ciao" + " " + "pippo";
char ch = s.charAt(2); // ch vale a. 
```

**Stringhe - Metodi**

``` Java
boolean endsWith (String suffix) // VERO se finisce con suffix.
boolean beginsWith (String prefix) // VERO se inizia con prefix.
boolean equals (Object other) // VERO se stringa è uguale a other.

// Restituisce stringa compresa tra bI ed eI.
String substring (int beginIndex, int endIndex)

int length() // Restituisce la lunghezza della stringa.

String toLowerCase() // Restituisce una stringa in maiuscolo/
String toUpperCase() // minuscolo.
```

**Array**
In Java sono classificati come oggetti. Creando un array definiamo un riferimento e per definirlo usiamo `new.` La selezione di un carattere si fa attraverso i brackets.
- La lunghezza dell'array si recupera attraverso il campo `length.`

``` Java
class EsempioArray
{
	public static void main(String args[])
	{
		int[] v1 = {1, 2, 3, 4}; // Vettore statico di 4 elementi
		int[] v2;                // Riferimento a vettore int
		v1[0];                   // Equivale ad 1
		v2 = new int[5];         // Definizione vettore 5 int
	}
}
```

- Creare un array con `new` significa creare `N` celle di tipo primitivo oppure `N` riferimenti ad oggetti di tipo `null` e vanno inizializzati tutti singolarmente.

``` Java
class EsempioArrayContatori
{
	public static void main(String args[])
	{
		Contatore v[] = new Contatore[3];
		
		v[0] = new Contatore(10);
		v[1] = new Contatore(100);
		v[2] = new Contatore(1000);
	}
}
```

**Documentazione**
Possiamo generare documentazione con i commenti dedicati e **javadoc** che crea pagine HTML. Per creare i file HTML si può usare il comando:
- `javadoc -author -version -d doc file.java`
- Le opzioni dicono di aggiungere `@author` `@version` e di mettere i file nella directory `doc.`

**Package**
Sono contenitori logici di classi. Corrispondono a contenitori fisici dei file `.class` inoltre un package può contenere classi e sotto-package.

**Package - Esempio**
Supponiamo di inserire le classi `Contatore` e `Data` all'interno del package `Utilità`
- Il nome completo delle classi diventa `Utilità.Contatore` e `Utilità.Data.` I file `.class` si trovano in una directory `Utilità.`

**Package - Uso di Classi**
In teoria dobbiamo specificare il percorso completo. In pratica possiamo importare le classi del package tramite comando `import` (simile a `include` in C).
- `import utilità.Classe` oppure `import utilità.*` per importare tutte le classi di un package. Non è però ricorsivo! Quindi non importiamo i sotto-package.

**Package - Inserimento della Classe**
È sufficiente specificare la direttiva `package nomePackage` all'inizio del file.

``` Java
package utilità;

public class Contatore
{
	...
}
```

``` Java
// Per sottopackage

package utilità.file;

public class FileComparator
{
	...
}
```

**Package - Percorso e Visibilità**
I package creati si trovano nel **CLASSPATH**.
- Il package di default si trova nella directory corrente.
- Il package determina anche un ambito di visibilità. Le entità senza una visibilità specifica sono visibili solo all'interno del package.

``` Shell
# Esempio di CLASSPATH. Il primo trovato viene usato.

# /home/ilir/java/utilità
# /usr/lib/java/utilità
# /directory_attuale/utilità
```

**Costanti**
Le costanti vengono create attraverso la keyword `final.`
- Tipicamente variabili `static` oppure variabili locali.

**Riferimenti ad Oggetti**
Le variabili di tipo `riferimento` contengono un riferimento ad un oggetto.
- `r1 = r2` NON duplica `r2` ma copia il riferimento di `r2` in `r1` quindi entrambi gli oggetti punteranno allo stesso.

``` Java
Contatore p1 = new Contatore();
Contatore p2 = p1;

p2.inc();
System.out.println(p1.getVal());
// c1.dec(); // NO: dec() non c’è in Contatore
// Risultato: 1
```

**Clonazione di Oggetti**
Se vogliamo duplicare un oggetto usiamo il metodo `clone().`
- `Contatore p2 = (Contatore)p1.clone();`

**Confronto di Oggetti**
Per confrontare gli oggetti usiamo il metodo `equals().`
- Restituisce `true` solo se entrambi i riferimenti puntano allo stesso oggetto.

**Passaggio dei Parametri**
I parametri in Java sono passati per **copia.**
- Se di tipo primitivo viene passato il valore, se di tipo riferimento viene passato l'indirizzo. Se una funzione modifica un valore allora al ritorno NON si modifica.

**This**
La keyword `this` svolge due funzionalità:
1) Specifica variabili e metodi di istanza in modo da non avere ambiguità.
2) Chiama costruttori della stessa classe.

``` Java
class Contatore
{
	private int val;
	
	// 1) 
	public Contatore(int val) {this.val = val}
	
	// 2)
	public Contatore() {this(0);}
}
```

**Garbage Collector**
È una componente dell'interprete che si occupa di liberare memoria automaticamente quando un'oggetto viene deallocato.

``` Java
Contatore c = new Contatore();
c = null;

// Il garbage collector può tranquillamente liberare la memoria di c.
```