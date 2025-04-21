**Classi Wrapper**
Le classi wrapper servono per poter usare i tipi primitivi come oggetti.
- In Java non tutto è object-oriented.

``` Java
Vector v = new Vector();
int i = 10;

// Creo un oggetto di tipo Integer e gli assegno i.

Integer iObject = new Integer(i);

// Lo aggiungo al vettore.

v.add(iObject);

// Assegno all'oggetto Integer il primo elemento del vettore.

iObject = (Integer)v.get(0);

// Assegno il valore dell'oggeto Integer ad i.

i = iObject.intValue();
```

**Autoboxing - Outboxing**
È possibile usare scalari in contesti di oggetti. Il compilatore gestisce il wrapping del tipo.
- Spesso le classi wrapper sono scomode da usare.

``` Java
Vector v = new Vector(10);

for (int i = 0; i < 5; i++)
{
	v.add(i);
	v.add((float)i * 2.5);
}

for (int i = 0; i < v.size(); i++)
	System.out.println(i + " = " + v.elementAt(i));

// Output: v[0] = 0 | v[1] = 0.0 | v[2] = 1 | v[3] = 2.5 e così via...
```

**Foreach**
`foreach` permette di scorrere tutti gli elementi di una struttura dati.
- Gestisce automaticamente l'aumento dell'indice e l'assegnamento dell'elemento successivo della struttura dati.

Affinchè una struttura dati sia utilizzabile in un ciclo `foreach` deve implementare la interfaccia `Iterable.` Non sono `null-safe` come i cicli standard.

``` Java
// for (variable_type variable_name : list)

public class foreach
{
	public static void main(String args[])
	{
		String array[] = new String[10];
		
		for (int i = 0; i < array.length; i++)
			array[i] = new String("Stringa n." + i);
		
		for (String s : array)
			System.out.println(s);
	}
}
```

**Foreach - Strutture Dati**

``` Java
import java.util.Vector;

public class foreach2
{
	public static void main(String args[])
	{
		Vector v = new Vector(10);
		
		for (int i = 0; i < 10; i++)
			v.add("String n." + i);
		
		/* I vectors memorizzano OBJECTS, non il tipo che aggiungiamo.
		   foreach non effettua cast. */
		
		for (Object s : v)
			System.out.println(s);
	}
}
```

**Foreach - Generics**

``` Java
public class foreach3
{
	public static void main(String argv[])
	{
		Vector<String> vettore = new Vector<String>();
		
		for (int i = 0; i < 10; i++)
			vettore.add(new String("stringa n.") + i);
		
		/* Se usiamo generics non dobbiamo usare una variabile di tipo
		   Object ma il tipo corretto. */
		
		for (String s : vettore)
			System.out.println(s);
	}
}
```

**Foreach - Estrazione**

``` Java
public class foreach4
{
	public static void main(String args[])
	{
		String array = new String[10];
		
		for (String s : array)
			s = "Ciao";
			
		for (String s : array)
			System.out.println(s);
	}
}

// Output: null per ogni posizione dell'array di stringhe.
// foreach può essere utilizzato solo per le estrazioni.
```

**Foreach - Considerazioni**
- Il compilatore fa il lavoro sporco.
- `foreach` riduce il rischio di errori banali.
- Non abbiamo accesso nè all'indice nè all'elemento corrente.

**Varargs**
Possiamo definire metodi che prendono un numero variabile di argomenti.
- Devono avere tutti lo stesso tipo oppure essere di tipo `Object.`

``` Java
public class varargs
{
	/* L'argomento di una funzione varargs diventa automaticamente un array. */
	
	public void mvar(String...pars) // <- ... è l'operatore varargs.
	{
		for (int i = 0; i < pars.length; i++)
			System.out.println("Parametro " + i + " = " + pars[i]);
	}
	
	public static void main(String args[])
	{
		varargs v = new varargs();
		v.mvar("ALFA", "BETA", "GAMMA");
	}
}

// Output: Parametro 0 = ALFA | Parametro 1 = BETA | Parametro 2 = GAMMA
```

``` Java
// Esempio equivalente

public class varargs
{
	public void mvar(String...pars)
	{
		for (String s : pars)
			System.out.println(s);
	}
	
	public static void main(String args[])
	{
		varargs v = new varargs();
		v.mvar("ALFA", "BETA", "GAMMA");
	}
}

// Output: ALFA | BETA | GAMMA
```

**Varargs - Overloading**
È possibile sovraccaricare un metodo varargs con una lista di argomenti dello stesso tipo.
- Viene eseguito il primo metodo il cui prototipo coincide con l'invocazione.
- L'overloading viene impedito se usiamo arrays come parametri. Il compilatore tratta un metodo varargs come un metodo ad array.

``` Java
public class varargs
{
	public void mvar(String...pars)
	{
		for (int i = 0; i < pars.length; i++)
			System.out.println("Parametro " + i " = " + pars[i]);
	}
	
	public void mvar(Object...pars)
	{
		for (int i = 0; i < pars.length; i++)
			System.out.println("Parametro di tipo: " + o.getClass());
	}
	
	public void mvar(String s1, String s2)
	{
		for (int i = 0; i < pars.length; i++)
			System.out.println("Stringa " + s1 + " Stringa " + s2);
	}
	
	public static void main(String args[])
	{
		varargs v = new varargs();
		v.mvar("ALFA", "BETA", "GAMMA");
		v.mvar(new Object(), new Integer(10);
		v.mvar("Ciao", "Pino");
	}
}
```

**Enumerazioni**
`enum` definisce le enumerazioni e sono oggetti.
- Un esempio classico è una lista statica di valori.

> Non bisogna confondere le enumerazioni con una serie di costanti. Il numero assegnato automaticamente alla variabile nella enumerazione serve solo per distinguere gli elementi nella lista.

``` Java
public class EventType
{
	public static enum type
	{
		OPEN,
		CLOSE,
		EXIT,
	} ;
}
```

``` Java
public class Enumerations
{
	public void fireEvent(EventType.type event)
	{
		System.out.println("L'evento ricevuto è: ");
		
		if (event == EventType.type.OPEN)
			System.out.println("APERTURA");
		else
		if (event == EventType.type.CLOSE)
			System.out.println("CHIUSURA");
		else	
		if (event == EventType.type.EXIT)
			System.out.println("USCITA");
	}
	
	public static void main(String args[])
	{
		Enumerations e = new Enumerations();
		e.fireEvent(EventType.type.OPEN);
		e.fireEvent(EventType.type.EXIT);
	}
}
```
