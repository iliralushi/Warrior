**Strutture Dati - Java**
Java implementa le strutture dati usando un mix di interfacce e classi.
- Le interfacce definiscono il tipo della struttura dati mentre le classi contengono le implementazioni delle strutture dati specifiche. Si trovano nel package `java.util.`
- Le strutture dati sono definite come generics.

**Interfacce - Collection**
`Collection<E>` è una interfaccia che definisce strutture dati di oggetti senza **specificare l'ordine** o se sono presenti dei **duplicati.**
- Abbiamo almeno due costruttori base: quello senza parametri e quello con parametro la struttura dati utilizzata.

![](../+Immagini/OOP/09/Collection.png)

**Interfacce - Map**
`Map<K, V>` è una interfaccia che definisce strutture dati che associano chiavi a valori.
- Chiavi e valori sono **oggetti.** Le chiavi devono essere **uniche** e verranno associate ad un solo valore. Anche le strutture dati derivanti da `Map` hanno almeno due costruttori base.

![](../+Immagini/OOP/09/Map.png)

``` Java
// Associazione CF -> Persona usando una Hash Map.

Map<String, Person> people = new HashMap<String, Person>();

people.put("ALCSMT", new Person("Alice", "Smith"));
people.put("RBTGRN", new Person("Robert", "Green"));

Person bob = people.get("RBTGRN");

if (bob == null)
	System.out.println("Not found!");

int populationSize = people.size();
```

**Collection - List**
`List<E>` contiene una sequenza di elementi (anche duplicati). L'ordine di inserimento è mantenuto. Possiamo accedere agli elementi tramite l'index.
- Aggiunge funzionalità rispetto all'interfaccia `Collection.`

![](../+Immagini/OOP/09/List.png)

**List - Implementazioni**
- `ArrayList:` Basata su un array dinamico. `get(index)` è costante, inserimento e cancellazione di un elemento sono lineari.
- `LinkedList:` Basata su puntatori. `get(index)` è lineare, inserimento e cancellazione di un elemento sono costanti.

`Costruttori + Metodi`

![](../+Immagini/OOP/09/ArrayList_LinkedList.png)

``` Java
List<Integer> al = new ArrayList<Integer>();

al.add(10);
al.add(25);
al.add(13);

System.out.println(al); // [10, 25, 13].

for (int i : al)
	System.out.println(i);
	
System.out.println(al.get(2)); // 13.
```

**List - Vector**
`Vector` è una classe che implementa `List.` Molto simile ad `ArrayList` - l'unica differenza è che `Vector` è `thread-safe` quindi leggermente più lento.
- È considerato obsoleto perchè tutti i metodi sono sincronizzati e lo sono per singola istruzione, non multipla. Questo comporta il blocco delle istruzioni anche quando non necessario.

**Collections - synchronizedList()**
Il metodo `<T> List<T> synchronizedList(List<T> list)` restituisce una lista sincronizzata a partire da una qualsiasi lista.

**List - Ridimensionamento Dinamico**
Sia `ArrayList` che `Vector` si basano su array. Hanno ridimensionamento dinamico.
1) La struttura dati ha sempre posto per inserire un altro elemento (memory's the limit).
2) Se l'array non ha spazio lo ricrea più grande e copia il vecchio array nel nuovo.
3) Ci sono **politiche** per evitare di copiare l'array ad ogni inserimento. Costerebbe `O(n).` Non bisogna scrivere codice che supponga una certa politica.

**Collection - Set**
`Set<E>` rappresenta un insieme. Non contiene elementi duplicati - se vengono aggiunti non succede niente e gli elementi aggiunti non hanno ordine particolare.
- Non aggiunge metodi rispetto a `Collection.`

**Set - SortedSet**
`SortedSet<E>` rappresenta un insieme ordinato naturalmente.

![](../+Immagini/OOP/09/SortedSet.png)

**Set - Altre Implementazioni**
- `HashSet`: Implementazione di `Set` - la struttura interna è una tabella hash - veloce.
- `LinkedHashSet:` Sottoclasse di `HashSet` - gli elementi hanno ordine di inserimento.
- `TreeSet:` Implementazione di `SortedSet` - la struttura interna è un albero - costo computazionale alto.

**SortedSet - Ordinamento**
È possibile specificare un ordine personalizzato tramite il costruttore.
- `TreeSet(Comparator c).`

**Map - SortedMap**
`SortedMap<E>` rappresenta una `Map` ordinata. Abbiamo sempre associazioni chiave-valore ma abbiamo un ordine naturale sugli elementi.

![](../+Immagini/OOP/09/SortedMap.png)

**Map - Altre Implementazioni**
- `HashMap:` Implementazione di `Map` - la struttura interna è una tabella hash - veloce.
- `LinkedHashMap:` Sottoclasse di `HashMap` - gli elementi hanno ordine di inserimento.
- `TreeMap:` Implementazione di `SortedMap` - la struttura interna è un albero - costo computazionale alto.

**Iterator**
`Iterator` fornisce un modo indipendente dalla struttura dati per scorrerla. È una operazione comune specialmente nelle strutture dati che implementano `Collection.`
1) Un iteratore tiene traccia dell'ultimo elemento visitato.
2) Si sposta sul prossimo elemento dopo ogni lettura se esistono elementi da leggere.

**Iterator - Interfaccia**
`Iterator<E>` definisce due metodi principali:
- `boolean hasNext():` se esiste un altro elemento ritorna `true.`
- `E next():` restituisce il prossimo elemento.

Successivamente sono stati aggiunti altri due metodi:
- `default void remove():` rimove l'oggetto corrente.
- `default void forEachRemaining(Consumer<? super E> action):` svolge una azione su tutti gli elementi rimanenti.

**Iterator - Iterable**
`Iterable<E>` è l'interfaccia da implementare se una struttura dati vuole usare un iteratore.
- `Iterable<E>` mette a disposizione il metodo `Iterator<E> iterator()` che restituisce un iteratore ad una struttura dati.

``` Java
Collection<Person> persons = new LinkedList<Person>();
Iterator<Person> i = persons.iterator();

while (i.hasNext())                           
{
	Person p = i.next();
	System.out.println(p);
}

/*
for (Person p : persons)
	System.out.println(p);
*/
```

> È pericoloso modificare una struttura dati che sta venendo iterata! Si ha undefined behaviour! Bisogna usare i metodi di `Iterator/ListIterator` come `add()` e `remove().`

**Ordinamento**
L'ordinamento degli elementi di una struttura dati è basato sul poter definire quale elemento è minore/maggiore rispetto ad un altro.

**Ordinamento Naturale**
- Ad ogni elemento è associato un numero naturale. Gli elementi sono ordinati a seconda del numero che hanno associato (ASCII).

**Interfacce - Comparable**
`Comparable<T>` permette di definire un ordinamento personalizzato. Mette a disposizione il metodo `public int compareTo(T obj)` - fa il confronto tra l'elemento su cui viene chiamato il metodo e l'elemento preso come parametro.
- Il valore di ritorno può essere `< 0` se l'elemento su cui viene chiamato il metodo è minore di `obj,` `= 0` se hanno ordine uguale oppure `> 0` se maggiore di `obj.`
- `Comparable` è già implementato in alcuni tipi come le Stringhe.

> Nell'esempio seguente l'ordinamento avviene tenendo conto sia del nome che cognome.

``` Java
public class PersonaOrdinata implements Comparable<PersonaOrdinata>
{
	private String nome, cognome;
	
	public PersonaOrdinata(String nome, String cognome)
	{
		this.nome = nome;
		this.cognome = cognome;
	}
	
	public String toString()
	{
		return nome + " " + cognome;
	}
	
	public int compareTo(PersonaOrdinata p)
	{
		int cmp = this.cognome.compareTo(p.nome)
		
		if (cmp != 0)
			return cmp;
		else
			return this.nome.compareTo(p.cognome);
	}
}
```

``` Java
public class PersonaOrdinataMain
{
	public static void main(String args[])
	{
		PersonaOrdinata p1 = new PersonaOrdinata("Mario", "Rossi");
		PersonaOrdinata p2 = new PersonaOrdinata("Giovanni", "Verdi");
		PersonaOrdinata p3 = new PersonaOrdinata("Alberto", "Rossi");
		PersonaOrdinata p4 = new PersonaOrdinata("Giovanni", "Neri");
		
		if (p1.compareTo(p3) < 0)
			System.out.println(p1 + " viene prima di " + p3);
		else
			System.out.println(p3 + " viene prima di " + p1);
			
		/* TreeSet prende il compareTo della classe dell'oggetto
		   personalizzato e ordina automaticamente gli elementi.
		   Con oggetti personalizzati SERVE il compareTo. */
		
		Set<PersonaOrdinata> persone = new TreeSet<PersonaOrdinata>;
		
		persone.add(p1);
		persone.add(p2);
		persone.add(p3);
		persone.add(p4);
		
		System.out.println(persone);	
	}
}

/* Output:
   Alberto Rossi viene prima di Mario Rossi
   Giovanni Neri, Alberto Rossi, Mario Rossi, Giovanni Verdi
*/
```

**Interfacce - Comparator**
`Comparator<T>` implementa un comparatore esterno alla classe. Usiamo più `Comparator` quando il `Comparable` non è sufficiente per gestire tutti i casi di ordinamento.
- `public int compare(T o1, T o2):` Confronta i due oggetti passati come parametro. Il valore di ritorno è `< 0` se `o1` è minore di `o2,` `= 0` se `o1` è nella stessa posizione di `o2` e `> 0` se `o1` è maggiore di `o2.`

> Nell'esempio seguente l'ordinamento avviene tenendo conto sia del nome che cognome ma anche del numero di matricola. In questo caso non basta solo il metodo `Comparable`
> perchè dobbiamo gestire delle stringhe e degli interi, meglio separare.

``` Java
public class StudenteMatricola
{
	private String nome, cognome;
	private int matricola;
	
	public StudenteMatricola(String nome, String cognome, int matricola)
	{
		this.nome = nome;
		this.cognome = cognome;
		this.matricola = matricola;
	}
	
	public String toString()
	{
		return nome + " " + cognome " " + matricola;
	}
	
	public String getNome()
	{
		return nome;
	}
	
	public String getCognome()
	{
		return cognome;
	}
	
	public int matricola()
	{
		return matricola;
	} 
}
```

``` Java
import java.util.*;

public class SCComparator implements Comparator<StudenteMatricola>
{
	public int compare(StudenteMatricola s1, StudenteMatricola s2)
	{
		int cmp = s1.getCognome().compareTo(s2.getCognome());
		
		if (cmp != 0)
			return cmp;
		else
			return s1.getNome().compareTo(s2.getNome());
	}
}
```

``` Java
import java.util.*;

public class SMComparator implements Comparator<StudenteMatricola>
{
	public int compare(StudenteMatricola s1, StudenteMatricola s2)
		return s1.getMatricola() - s2.getMatricola();
}
```

``` Java
import java.util.*;

public class StudenteMatricolaMain // StudenteMatricola abbreviato in SM
{
	public static void main(String args[])
	{
		SM s1 = new SM("Mario", "Rossi", "12");
		SM s2 = new SM("Giovanni", "Verdi", "8");
		SM s3 = new SM("Alberto", "Rossi", "37");
		SM s4 = new SM("Giovanni", "Neri", "25");
		
		Set<SM> studenti1 = new TreeSet<SM>(new SMComparator());
		
		studenti1.add(s1);
		studenti1.add(s2);
		studenti1.add(s3);
		studenti1.add(s4);
		
		System.out.println("Ordine per matricola: " + studenti1);
	}
}

/* Output:
   Ordine per matricola: Giovanni Verdi 8, Mario Rossi 12, Giovanni Neri 25,
   Alberto Rossi 37.
*/
```

``` Java
import java.util.*;

public class StudenteMatricolaMain // StudenteMatricola abbreviato in SM
{
	public static void main(String args[])
	{
		SM s1 = new SM("Mario", "Rossi", "12");
		SM s2 = new SM("Giovanni", "Verdi", "8");
		SM s3 = new SM("Alberto", "Rossi", "37");
		SM s4 = new SM("Giovanni", "Neri", "25");
		
		Set<SM> studenti2 = new TreeSet<SM>(new SCComparator());
		
		studenti1.add(s1);
		studenti1.add(s2);
		studenti1.add(s3);
		studenti1.add(s4);
		
		System.out.println("Ordine per cognome: " + studenti2);
	}
}

/* Output:
   Ordine per matricola: Giovanni Neri 25, Alberto Rossi 37, Mario Rossi 12,
   Giovanni Verdi 8.
*/
```

**Algoritmi Generici**
- ***Package Sort Liste***: `java.util.Collections.`
- ***Package Sort Arrays:*** `java.util.Arrays.`

- `sort():` Merge sort.
- `binarySearch():` Richiede una sequenza ordinata.

``` Java
// Metodi Liste
```


- `shuffle():` Mescola la lista.
- `reverse():` Richiede una sequenza ordinata.
- `rotate():` Di una certa distanza.
- `min/max():` Di una `Collection.`

``` Java
// Metodi Arrays
```

- `compare():` Confronta arrays.
- `copyOf():` Copia arrays.
- `equals():` Dice se due array sono uguali.