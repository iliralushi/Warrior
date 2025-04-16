**Java Swing**
Swing è una libreria di Java (evoluta da AWT) usata per realizzare GUI.

**Da AWT a Swing**
- ***AWT:*** Sistema peer-to-peer per visualizzare i componenti grafici. Ogni componente è mappato direttamente su un componente del SO.
- ***Swing:*** Disegna separatamente dal SO i suoi componenti grafici.

**Componenti Swing**
Non usano codice nativo quindi hanno più widgets. Il suo comportamento non dipende dal SO in uso. Swing definisce due componenti:
- ***Leggeri:*** Disegnati da Swing stesso.
- ***Pesanti:*** Hanno bisogno un peer (componente nativo) dell'SO per funzionare tipo `JFrame.`

**Componenti Swing - OOP**
La programmazione delle interfacce grafiche segue la OOP. Ogni componente è implementato tramite una classe. Si possono creare oggetti e specializzare.
- ***Packages:*** `java.awt + javax.swing`

**Classi Swing - Derivazione**
Tutte le classi di Swing derivano da quelle di AWT `(Component).`
- Anche i `Container` sono sottoclassi di `Component.`

**Classi Swing - JFrame**
`JFrame` è la classe che implementa la finestra dell'applicazione.
- Ha un bordo e una barra in alto con pulsanti per interagire con la finestra.
- Lo stile dipende dal Window Manager del SO

``` Java
import java.awt.*;
import javax.swing.*;

public class EsSwing1
{
	public static void main(String args[])
	{
		/* Crea un nuovo JFrame inizialmente invisibile con titolo
		   "Esempio 1". */
		
		JFrame f = new JFrame("Esempio 1");
		
		f.setVisible(true); // Rende il JFrame visibile.
	}
}
```

**JFrame - Posizione e Dimensione**
Senza alcuna indicazione avremo una finestra piccolissima.
Per impostare la posizione iniziale ed una dimensione usiamo un metodo.
- `public void setBounds(int x, int y, int width, int height)`
- `(x, y)` indicano la posizione nello schermo, `(width, height)` indicano la larghezza e la lunghezza della finestra.

``` Java
import java.awt.*;
import javax.swing.*;

public class EsSwing1
{
	public static void main(String args[])
	{
		JFrame f = new JFrame("Esempio 1");
		f.setBounds(200, 100, 300, 150);
		f.setVisible(true);
	}
}
```

**JFrame - Chiusura Applicazione**
Senza alcuna indicazione la chiusura non distrugge il frame.
Possiamo specificare cosa deve fare il frame quando viene premuto il pulsante di chiusura del frame tramite metodo `setDefaultCloseOperation(int Operation).`
- `EXIT_ON_CLOSE` fa in modo di terminare il frame.

**JFrame - Personalizzazione**
La classe `JFrame` può essere estesa e personalizzata.
- ***Esempio:*** Definiamo una classe `MyFrame` con due costruttori; uno senza parametri e uno con una stringa come parametro che rappresenta il titolo. Entrambi impostano posizione e dimensione. Inoltre specifichiamo il comportamento del frame alla chiusura.

``` Java
import java.awt.*;
import javax.swing.*;

public class MyFrame extends JFrame
{
	public MyFrame()
	{
		/* Facendo this("") richiamiamo il costruttore con parametro
		   settando anche posizione, dimensione e comportamento dopo
		   la chiusura. */
		
		this("");
	}
	
	public MyFrame(String titolo)
	{
		super(titolo);
		setBounds(200, 100, 300, 150);
		setDefaultCloseOperation(EXIT_ON_CLOSE);
	}
}
```

``` Java
import java.awt.*;
import javax.swing.*;

public class EsSwing2
{
	public static void main(String args[])
	{
		MyFrame f = new MyFrame("Esempio 2");
		f.setVisible(true);
	}
}
```

**JFrame - Inserire Componenti**
In Swing si possono aggiungere componenti direttamente al `JFrame.`
- Tipicamente si aggiunge un `JPanel` tramite metodo `add().`

Precedentemente (JDK < 1.5) si recuperava il `Container`  del `JFrame` tramite `getContentPane()` e si aggiungevano nuovi componenti al Container stesso.

``` Java
import java.awt.*;
import javax.swing.*;

public class EsSwing3
{
	public static void main(String args[])
	{
		MyFrame f = new MyFrame("Esempio 3");
		JPanel panel = new JPanel(); // Creo pannello.
		f.add(panel); // Aggiungo pannello al JFrame.
		f.setVisible(true);
		
		// JDK < 1.5
		
		/* Container c = f.getContentPane();
		   JPanel panel = new JPanel();
		   c.add(panel);
		   f.setVisible(true); */
	}
}
```

**Classi Swing - JPanel**
`JPanel` è la classe che implementa un pannello da inserire in un frame/finestra.
- Possiamo disegnarci oppure aggiungerci componenti grafici come bottoni o etichette.

**JPanel - Inserire Componenti**
I componenti sono oggetti veri e propri. Per aggiungerli al `JPanel` bisogna sfruttare il costruttore del pannello stesso.

**Classi Swing - JLabel**
`JLabel` rappresenta una etichetta.
- A differenza di una stringa disegna si può cambiare la scritta, la posizione e posso ricavare cosa c'è scritto.

``` Java
import javax.swing.*;

public class MyPanel extends JPanel
{
	// Uso il costruttore del pannello stesso per aggiungere un JLabel
	public MyPanel()
	{
		super();
		JLabel l = new JLabel("Etichetta");
		add(l);
	}
}
```

``` Java
import java.awt.*;
import javax.swing.*;

public class Es4Swing
{
	public static void main(String args[])
	{
		MyFrame f = new MyFrame("Esempio 4");
		MyPanel p = new MyPanel();
		f.add(p);
		
		// Dimensiona il frame in modo da contenere il pannello
		f.pack();
		
		f.setVisible(true);
	}
}
```

**Programmazione ad Eventi**
Fino ad adesso l'utente non poteva interagire con la GUI ma solo guardare. L'interazione viene programmata tramite eventi (che sono oggetti).
1) Quando l'utente compie un'azione viene generato un evento appropriato.
2) L'evento viene inviato ad un ascoltatore.
3) L'ascoltatore esegue il codice appropriato all'evento.

**Ascoltatore**
Un ascoltatore è un oggetto che implementa un'interfaccia di tipo `Listener.`

**Classi Swing - JButton**
`JButton` implementa il classico bottone premibile dall'utente.

**JButton - Eventi**
Quando premuto viene generato un evento di classe `ActionEvent.` Esso viene inviato al `listener` specifico di quell'evento.
- L'ascoltatore degli eventi deve implementare la interfaccia `ActionListener` e definire il metodo `actionPerformed(ActionEvent ev)` che specifica il comportamento da assumere durante l'evento.
- L'ascoltatore degli eventi può essere il pannello stesso oppure una classe al di fuori del pannello.

**JButton - Esempio**
Applicazione con un `JLabel` ed un `JButton.` Ogni volta che il pulsante viene premuto l'etichetta cambia da Tizio a Caio e viceversa.

``` Java
import java.awt.event.*;
import javax.swing.*;

public class MyPanel extends JPanel implements ActionListener
{
	/* La label deve essere visibile a tutti i metodi della classe,
	   in particolare all'actionPerformed, quindi la definiamo all'
	   esterno del costruttore. */
	
	private JLabel l;
	
	public MyPanel()
	{
		super();
		l = new JLabel("Tizio");
		add(l);
		
		JButton b = new JButton("Tizio/Caio");
		
		/* Il metodo addActionListener definisce l'ActionListener
		   per una determinata componente. In questo caso stiamo
		   definendo come ActionListener del bottone il pannello 
		   stesso. */
		   
		b.addActionListener(this);
		add(b);
	}
	
	public void actionPerformed(ActionEvent e)
	{
		if (l.getText().equals("Tizio"))
			l.setText("Caio");
		else
			l.setText("Tizio");
	}
}
```

``` Java
import java.awt.*;
import javax.swing.*;

public class Es5Swing
{
	public static void main(String args[])
	{
		MyFrame f = new MyFrame("Esempio 5");
		MyPanel p = new MyPanel();
		f.add(p);
		f.pack();
		f.setVisible(true);
	}
}
```