


# Thread-Programmierung

## Übersicht
In dieser Dokumentation werden die Grundlagen der Thread-Programmierung in C# behandelt. Es wird erklärt, wie Threads gestartet und gestoppt werden, wie man einem Thread Parameter übergibt und wie man den Status eines Threads überprüft. Zum Abschluss gibt es ein kleines Demo-Programm, das diese Konzepte veranschaulicht.

## Inhaltsverzeichnis
1. [Einleitung](#einleitung)
2. [Wie können Threads programmiert werden (Start, Stop usw.)](#wie-können-threads-programmiert-werden-start-stop-usw)
3. [Wie kann ein Thread beim Starten Parameter erhalten](#wie-kann-ein-thread-beim-starten-parameter-erhalten)
4. [Wie kann geprüft werden, ob ein Thread noch läuft oder beendet wurde](#wie-kann-geprüft-werden-ob-ein-thread-noch-läuft-oder-beendet-wurde)
5. [Demo-Programm: Thread starten und stoppen](#demo-programm-thread-starten-und-stoppen)





## Einleitung
Im Thread-Programming wird das Programm in mehrere unabhängige Ausführungseinheiten, sogenannte Threads, unterteilt. Diese Threads können gleichzeitig (parallel) ausgeführt werden, was die Leistung und Effizienz des Programms verbessern kann. Jeder Thread läuft in einem gemeinsamen Speicherbereich des Prozesses, was einen schnellen Datenaustausch ermöglicht.

### Vorteile
- **Parallelität:** 
- **Reaktionsfähigkeit:** 
- **Ressourcenteilung:** 

### Herausforderungen
- **Synchronisation:** 
- **Race Conditions:** 
- **Deadlocks:** 




## Wie können Threads programmiert werden (Start, Stop usw.)
Threads können in C# mit der Klasse `Thread` aus dem `System.Threading`-Namespace programmiert werden. Ein Thread kann gestartet und gestoppt werden, indem die Methoden `Start()` und `Join()` verwendet werden.

### Beispiel:
```csharp
using System;
using System.Threading;

class Program
{
    static void Worker()
    {
        Console.WriteLine("Thread gestartet");
        Thread.Sleep(2000);
        Console.WriteLine("Thread gestoppt");
    }

    static void Main()
    {
        // Thread erstellen
        Thread thread = new Thread(Worker);

        // Thread starten
        thread.Start();

        // Warten, bis der Thread beendet ist
        thread.Join();
        Console.WriteLine("Hauptprogramm beendet");
    }
}
```

## Wie kann ein Thread beim Starten Parameter erhalten
Ein Thread kann beim Starten Parameter erhalten, indem ein `ParameterizedThreadStart`-Delegat verwendet wird. Die Parameter werden mit der `Start`-Methode übergeben.

### Beispiel:
```csharp
using System;
using System.Threading;

class Program
{
    static void Worker(object data)
    {
        var tuple = (Tuple<string, int>)data;
        string name = tuple.Item1;
        int duration = tuple.Item2;
        Console.WriteLine($"Thread {name} gestartet");
        Thread.Sleep(duration);
        Console.WriteLine($"Thread {name} gestoppt");
    }

    static void Main()
    {
        // Parameter erstellen
        var parameters = Tuple.Create("TestThread", 3000);

        // Thread erstellen und Parameter übergeben
        Thread thread = new Thread(new ParameterizedThreadStart(Worker));

        // Thread starten
        thread.Start(parameters);

        // Warten, bis der Thread beendet ist
        thread.Join();
        Console.WriteLine("Hauptprogramm beendet");
    }
}
```

## Wie kann geprüft werden, ob ein Thread noch läuft oder beendet wurde
Um zu prüfen, ob ein Thread noch läuft oder beendet wurde, kann die Eigenschaft `IsAlive` verwendet werden. Diese Eigenschaft gibt `true` zurück, wenn der Thread noch läuft, und `false`, wenn er beendet wurde.

### Beispiel:
```csharp
using System;
using System.Threading;

class Program
{
    static void Worker()
    {
        Console.WriteLine("Thread gestartet");
        Thread.Sleep(2000);
        Console.WriteLine("Thread gestoppt");
    }

    static void Main()
    {
        // Thread erstellen
        Thread thread = new Thread(Worker);

        // Thread starten
        thread.Start();

        // Überprüfen, ob der Thread noch läuft
        while (thread.IsAlive)
        {
            Console.WriteLine("Thread läuft noch...");
            Thread.Sleep(1000);
        }

        Console.WriteLine("Thread ist beendet");
    }
}
```

## Demo-Programm: Thread starten und stoppen




