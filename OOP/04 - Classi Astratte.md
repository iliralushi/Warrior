**Classe Astratta**
È una classe che definisce variabili e metodi senza la loro implementazione. È utile per creare una classe con metodi condivisi da altre sottoclassi.
- Si definisce il comportamento ma non l'implementazione.

> ***Esempio:*** Se dobbiamo creare varie classi riguardanti veicoli abbiamo che molte informazioni ed azioni si ripeteranno tra loro. È meglio fattorizzarle attraverso una superclasse comune a tutti dal punto di vista progettuale e implementativo.

``` Java
/* Le caratteristiche comuni vengono fattorizzate nella classe
   Veicolo. */

public abstract class Veicolo
{
	private int cilindrata;
	private String nome;
	private String targa;
	
	public abstract String si_muove();
	public abstract String trasporta();
}
```

**Classe Astratta - Note**
La classe `Veicolo` sopra anche nella realtà è solo una generalizzazione non una classe che esiste nel concreto - le classi astratte **non possono essere istanziate.**
- Una classe che ha anche solo un metodo `abstract` deve essere dichiarata `abstract.` Inoltre una classe astratta può anche non aver metodi `abstract.` 
- Una sottoclasse che non definisce tutti i metodi abstract è una classe astratta.

**Classe Astratta - Costruttori**
Anche se non possiamo creare istanze di classe i costruttori sono utili per definire lo stato. Potrà ovviamente essere chiamato solo dalle sottoclassi.

``` Java
// Classe Veicolo completa

public abstract class Veicolo
{
	private String nome;
	public Veicolo (String s)
	{
		nome = s;
	}
	
	public abstract String si_muove();
	public abstract String trasporta();
	public abstract String chi_sei(); // Descrizione dell'oggetto
	
	public String toString()
	{
		return nome + ", " + chi_sei() + ", si muove" + si_muove() +
		       " e trasporta " + trasporta();
	}
}
```

**Criterio di Classificazione**
Per definire una gerarchia ci dobbiamo basare su determinati criteri ovvero i metodi astratti. Nel nostro caso abbiamo l'ambiente in cui un veicolo si muove e il tipo delle cose trasportate.

**Ambiente - Primo Livello Gerarchia**
- Decidiamo di suddividere l'ambiente in veicoli terrestri ed acquatici. `trasporta()` non verrà ancora definito, quindi saranno classi astratte.

``` Java
public abstract class VeicoloTerrestre extends Veicolo
{
	public VeicoloTerrestre(String s)
	{
		super(s);
	}
	
	@Override
	public abstract String si_muove()
	{
		return "sulla terra";
	}
	
	@Override
	public abstract String chi_sei()
	{
		return "un veicolo terrestre";
	}
}
```

``` Java
public abstract class VeicoloAcquatico extends Veicolo
{
	public VeicoloAcquatico(String s)
	{
		super(s);
	}
	
	@Override
	public abstract String si_muove()
	{
		return "sull'acqua";
	}
	
	@Override
	public abstract String chi_sei()
	{
		return "un veicolo acquatico";
	}
}
```

**Trasporto - Secondo Livello Gerarchia**
- Per esempio per i veicoli di terra possiamo avere automobili che trasportano persone oppure camion che trasportano merce. Saranno classi concrete dato che non ci sono più metodi astratti.

``` Java
public abstract class Camion extends VeicoloTerrestre
{
	public Camion(String s)
	{
		super(s);
	}
	
	@Override
	public String trasporta()
	{
		return "merci";
	}
	
	@Override
	public String chi_sei()
	{
		return "un camion";
	}
}
```

``` Java
public abstract class Automobile extends VeicoloTerrestre
{
	public Automobile(String s)
	{
		super(s);
	}
	
	@Override
	public String trasporta()
	{
		return "persone";
	}
	
	@Override
	public String chi_sei()
	{
		return "un'auto";
	}
}
```

``` Java
public class MondoVeicoli
{
	public static void main(String args[])
	{
		Camion c = new Camion("Fiat ZZ999XX");
		Automobile a = new Automobile("Volvo AA111BB");
		
		System.out.println(c.toString());
		System.out.println(a.toString());
	}
}

/* $ java MondoVeicoli
   OUTPUT: Fiat ZZ999XX, un camion, si muove sulla terra e trasporta         merci.
   Volvo AA111BB, un'auto, si muove sulla terra e trasporta persone. 
*/
```

**Array di Veicoli**
Possiamo creare un array di `Veicoli` perchè non istanziamo alcun oggetto.
- Il polimorfismo fa si che per ogni oggetto reale il metodo `toString` stampi un output diverso.

``` Java
public class Città
{
	public static void main(String args[])
	{
		Veicolo v[] = new Veicolo[4];
		v[0] = new Camion("Fiat ZZ999XX");
		v[1] = new Automobile("Volvo AA111BB");
		v[2] = new Camion("Mercedes MM123NN");
		v[3] = new Automobile("Volkswagen GG777CC");
		
		for (int i = 0; i < 4; i++)
			System.out.println(v[i].toString());
	}
}
```

**Ereditarietà e Classificazione**
Per la classificazione potevamo scegliere due criteri e partire sia dall'ambiente che dalla merce trasportata. Usando l'ereditarietà singola però dividiamo il concetto di ambiente (se partiamo dalla merce trasportata) tra le altre classi.

**Ereditarietà Multipla**
Soluzione al problema precedente. In Java non esiste.
- È complicato da gestire. Per esempio un caso non gestito è se la sottoclasse eredita variabili e metodi ononimi da due o più superclassi.

**Interfaccia**
È una insieme di dichiarazione di metodi. Una classe implementa un interfaccia se da un corpo a tutti i metodi. C'è ereditarietà multipla **tra interfacce.**
- `interface` per definire un interfaccia, `implements` per implementarla. Una classe può implementare zero o più interfacce.
- Java definisce alcune interfacce vuote. Hanno lo scopo di **marcatori** come `Serializable` e `Cloneable.`

``` Java
public interface VeicoloPersone
{
	public void viaggia();
}
```

``` Java
// Ereditarietà multipla

public interface AutoDiplomatica extends VeicoloPersone, Interface2
{
	...
}
```

``` Java
public class Automobile extends VeicoloTerrestre
implements VeicoloPersone
{
	@Override
	public void viaggia()
	{
		...
	}
}
```

**Variabili di Tipo Interfaccia**
Possiamo creare variabili di tipo interfaccia finchè non istanziamo un oggetto.

``` Java
public class Esempio5
{
	public static void main(String args[])
	{
		VeicoloPersone a[] = new VeicoloPersone[20];
		
		a[1] = new Automobile();
		a[1].viaggia();
	}
}
```