**Type-Safety**
Un programma è `type-safe` quando è coerente nei tipi di dati in ogni struttura dati.
- Il controllo avviene a runtime ma potrebbe essere troppo tardi. Problema non banale se vogliamo capire se il programma è `type-safe` a compile time.

**Conformità in Java**
Con la conformità possiamo usare le sottoclassi come se fossero classi base.
- Normalmente è avvantaggiosa, però per esempio i `Vector` accettano qualsiasi tipo di oggetto. Si possono avere problemi di `type-safety.` Usiamo i generics.

**Esempio**
1) Abbiamo due tipi di persone - studenti e professori.
2) L'archivio deve contenere sia studenti che professori.
3) L'archivio deve essere omogeneo - no immischi tra studenti e professori.

Studenti e professori sono accomunati dal fatto di essere entrambi persone. Si crea quindi un legame tra studenti e professori - una gerarchia.

``` Java
public class Persona
{
	private String nome;
	private String cognome:
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

public class Archivio1
{
	private Vector persone;
	
	public Archivio1()
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
		return(Persona)persone.get(index);
	}
	
	public int size()
	{
		return persone.size();
	}
```

**Esempio - Problema**
Il codice scritto gestisce con una sola logica tutti i tipi `Persona` - non abbiamo differenze tra studenti e professori! Possiamo avere `type-unsafety` nel programma.
- Non abbiamo alcun controllo e le incoerenze non possono essere rilevate a compile time.

> Utilizzo scorretto:

``` Java
public class Archivio
{
	public static void main(String args[])
	{
		Studente s1 = new Studente("Luca", "Ferrari", 26, 41191);
		Studente s2 = new Studente("Santi", "Caballe", 29, 21192);
		Studente s3 = new Studente("James", "Gosling", 50, 41193);
		
		Professore pr1 = new Professore("Silvia", "Rossi", 27, "Analisi");
		Professore pr2 = new Professore("Simon", "Ritter", 40, "OOP");
		
		Archivio1 archivio_prof = new Archivio1();
		Archivio1 archivio_stud = new Archivio1();
		
		archivio_prof.aggiungi(pr1);
		archivio_prof.aggiungi(pr2);
		archivio_prof.aggiungi(s1); // Illegale!
		
		archivio_stud.aggiungi(s1);
		archivio_stud.aggiungi(s2);
		archivio_stud.aggiungi(s3);
		archivio_stud.aggiungi(pr1); // Illegale!
		
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