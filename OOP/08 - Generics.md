**Type-Safety**
Un programma è `type-safe` quando è coerente nei tipi di dati in ogni struttura dati.
- Il controllo avviene a `runtime` ma dobbiamo fare in modo che avvenga durante la compilazione per dire che il programma è `type-safe.`

**Conformità in Java**
Il compilatore controlla se le operazioni svolte sono compatibili rispetto ai vari tipi di dati coinvolti. Grazie alla conformità possiamo usare sottoclassi come fossero classi base.
- Allo stesso tempo può creare problemi di `type-safety.` Per esempio la struttura dati `Vector` accetta come tipo di dato `Object` - è un problema. 

**Esempio**
Dobbiamo costruire un archivio di studenti e professori. Deve essere omogeneo.
- Studenti e professori sono accomunati dal fatto che sono entrambe persone. Si ha un legame tra studenti e professori, si ha quindi una gerarchia.

``` Java
public class Persona
{
	private String nome, cognome;
	private int età;
	
	public Persona(String nome, String cognome, int età)
	{
		this.nome = nome;
		this.cognome = cognome;
		this.età = età;
	}
	
	public String toString()
	{
		return nome + " " + cognome " " + età;
	}
}
```

``` Java
public class Professore extends Persona
{
	private String materia;
	
	public Professore(String nome, String cognome, int età, String materia)
	{
		super(nome, cognome, età);
		this.materia = materia;
	}
	
	public String getMateria()
	{
		return materia;
	}
}
```

``` Java
public class Studente extends Persona
{
	private int matricola;
	
	public Studente(String nome, String cognome, int età, int matricola)
	{
		super(nome, cognome, età);
		this.matricola = matricola;
	}
	
	public int getMatricola()
	{
		return matricola;
	}
}
```

``` Java
import java.util.Vector;

public class ArchivioScuola
{
	private Vector persone;
	
	public ArchivioScuola()
	{
		persone = new Vector(10);
	}
	
	public void aggiungi(Persona p)
	{
		persone.add(p);
	}
	
	public void rimuovi(Persona p)
	{
		persone.remove(p);
	}
	
	public Persona get(int index)
	{
		return (Persona)persone.get(index);
	}
	
	public int size()
	{
		return persone.size();
	}
}
```

**Esempio - Problema**
1) La classe `ArchivioPersone` non controlla il tipo gestito. Posso aggiungere tutti i tipi che derivano da `Persone.` Si ha `type-unsafety` nel programma.
2) Il controllo non avviene durante la compilazione.

``` Java
// Utilizzo scorretto.

public class Archivio
{
	public static void main(String args[])
	{
		Studente s1 = new Studente("Luca", "Ferrari", 26, 41191);
		Studente s2 = new Studente("James", "Gosling", 50, 41193);
		
		Professore pr1 = new Professore("Silvia", "Rossi", 27, "Analisi");
		Professore pr2 = new Professore("Simon", "Ritter", 40, "OOP");
		
		ArchivioScuola archivio_prof = new ArchivioScuola();
		ArchivioScuola archivio_stud = new ArchivioScuola();
		
		archivio_prof.aggiungi(pr1);
		archivio_prof.aggiungi(pr2);
		archivio_prof.aggiungi(s1); // Non dovremmo poterlo fare!
		
		archivio_stud.aggiungi(s1);
		archivio_stud.aggiungi(s2);
		archivio_stud.aggiungi(pr1); // Non dovremmo poterlo fare!
		
		/* Il cast svolto in teoria è corretto; nell'archivio di studenti ci
		   devono essere solo studenti e viceversa. Nella pratica ci sarà una
		   eccezione; non possiamo castare studenti a professori e viceversa.
		*/
		
		for (int i = 0; i < archivio_prof.size(); i++)
		{
			Professore pTemp = (Professore)archivio_prof.get(i);
			System.out.println("Professore " + i + " " + pTemp + " " + 
			                    pTemp.getMateria());
		}
		
		for (int i = 0; i < archivio_stud.size(); i++)
		{
			Studente sTemp = (Studente)archivio_stud.get(i);
			System.out.println("Studente " + i + " " + sTemp + " " + 
			                    sTemp.getMatricola());
		}
	}
}
```

**Soluzioni Errate**
1) ***Creare un archivio per tipo di persona:*** Non mantenibile a lungo termine. Richiede la creazione di un archivio per ogni tipo di persona che viene aggiunta.
2) ***Creare interfacce differenti per ogni archivio:*** Meno codice da scrivere rispetto alla prima soluzione però è potenzialmente `type-unsafe.`
3) ***Eliminare la gerarchia:*** Non una soluzione OO. Dobbiamo scrivere molto più codice.

**Generics**
Tipo di dato parametrico. Se una classe usa generics non ha un tipo di dato ma lo riceve dopo la istanziazione. La coerenza dei tipi viene controllata durante la compilazione.
- Possiamo costruire classi che agiscono su più tipi di dati in modo coerente.
- Supportati da Java. Una volta dichiarato il tipo non dobbiamo usare casting.

``` Java
import java.util.Vector;

public class ArchivioS2<E> /* <- Questa dichiarazione indica che il tipo
							     di dato verrà specificato dalla classe
								 che userà ArchivioScuola. */
{
	private Vector persone;
	
	public ArchivioS2()
	{
		persone = new Vector(10);
	}
	
	public void aggiungi(E p) // <- I metodi usano variabili di tipo generics.
	{
		persone.add(p);
	}
	
	public void rimuovi(E p)
	{
		persone.remove(p);
	}
	
	public E get(int index)
	{
		return (E)persone.get(index);
	}
	
	public int size()
	{
		return persone.size();
	}
}
```

``` Java
public class Archivio
{
	public static void main(String args[])
	{
		ArchivioS2<Professore> archivio_prof = new ArchivioS2<Professore>();
		ArchivioS2<Studente> archivio_stud = new ArchivioS2<Studente>();
		ArchivioS2<Persona> archivio_pers = new ArchivioS2<Persona>();
		
		archivio_prof.aggiungi(pr1);
		archivio_prof.aggiungi(pr2);
		archivio_prof.aggiungi(s1); // Errore in compilazione!
	}
}
```

**Generics - Wildcards**
Possiamo usare il carattere `?` come wildcard.
- `? extends <type>` indica tutti i tipi che ereditano da `type.` Non si possono usare classi diverse da quelle della gerarchia di `Persona` se prendiamo come esempio l'archivio.
- `?` assegna ad una variabile un oggetto parametrizzato con un sottotipo.
- `? super <type>` è un caso simile che funziona con le superclassi.

``` Java
// 1)
ArchivioScuola<? extends Persona> 

// 2)
Vector<Persona> v = new Vector<Studente> // Errore.
Vector<? extends Persona> v = new Vector<Studente>;
```

**Generics - Ereditarietà**
È possibile ereditare da una classe e aggiungere il supporto ai generics nello stesso tempo.
- I metodi non devono essere in conflitto tra loro.

``` Java
public class ArchivioII<E> extends ArchivioScuola
{
	/* Studente/Professore sono anche Persona quindi un metodo con un generics
	   come parametro potrebbe andare in conflitto col metodo della classe 
	   padre se abbiamo un tipo Persona. Overriding non voluto. */
	   
	public void aggiungiElement(E p)
	{
		persone.add(p);
	}
}
```

**Generics - Funzionamento**
Il compilatore svolge passi di **manipolazione sintattica** che forzano errori di casting.
1) Il compilatore rimuove il tag generics e lo sostituisce ad `Object.`
2) Il compilatore rimuove il tag generics e forza dei cast.

``` Java
public class ArchivioScuola<E>
{
	private Vector persone;
	
	public ArchivioScuola()
	{
		persone = new Vector(10);
	}
	
	public void aggiungi(E p) // Diventa Object p.
	{
		persone.add(p);
	}
	
	...
}
```

``` Java
archivio_prof.aggiungi(pr1); // (Professore)pr1.
archivio_prof.aggiungi(pr2); // (Professore)pr2.
archivio_prof.aggiungi(s1);  // (Professore)s1 - Errore!
```

``` Java
// Esempio corretto.

import java.util.Vector;

public class ArchivioScuola<E>
{
	private Vector<E> persone;
	
	public ArchivioScuola()
	{
		persone = new Vector<E>(10);
	}
	
	public void aggiungi(E p)
	{
		persone.add(p);
	}
	
	public void rimuovi(E p)
	{
		persone.remove(p);
	}
	
	public E get(int index) // No cast.
	{
		return persone.get(index);
	}
	
	public int size()
	{
		return persone.size();
	}
}
```

**Generics - Classi Normali**
Se usiamo una classe normale come generics abbiamo un errore in compilazione.
- `ArchivioScuola<Professore> a = new ArchivioScuola<Professore>();`

**Generics - Tradeoff**
Generics permette di creare classi completamente generiche e `type-safe` - non impedisce però di inserire tipi di dato non coerenti col programma!
- Questo succede perchè avviene un casting ad `Object` durante la compilazione.

**Generics - Limitazione Tipi**
Possiamo limitare i tipi assegnabili tramite la keyword `extends.`
- `public class ArchivioScuola <E extends Persona>`

Dopo questa definizione se creiamo un `ArchivioScuola` con un tipo di dato non conforme al programma allora abbiamo un errore in compilazione.
- `ArchivioScuola<String> archivio_stud = new ArchivioScuola<String>();`

**Generics - Relazioni**
Tutte le istanze di oggetti create tramite generics condividono la stessa classe. Non sono in relazione anche se `Studente` eredita da `Persona!`

``` Java
ArchivioScuola<Persona> = aPersona; // ArchivioScuola<? extends Persona>
ArchivioScuola<Studente> = aStudente;

aPersona = aStudente; // Non possiamo farlo. Dobbiamo usare le wildcards.
```

**Generics - Extend Generics**
Possiamo estendere una classe che usa generics. La sottoclasse può fare uso di generics. Valgono tutte le regole dell'ereditarietà.