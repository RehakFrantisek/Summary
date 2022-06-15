# Java tahák

## Knihovní třída

* `public final` – třída je viditelná pro všechny, z třídy nelze dědit
* Privátní konstruktor – nelze tvořit instance
* Všechny metody statické

```java
public final class Library {
    private Library() {}
    // public static metody
}
```

## Main a instanční třída

```java
public class Main{
  public static void main(String[] args){
    InstanceTridy instanceNazev = new InstanceTridy();
    UI ui = new UI(instanceNazev);
    ui.menu();
  }
}
```

```java
public class InstanceTridy{
  private ArrayList<Trida> nazev = new ArrayList<>();
  // konstruktor
  public InstanceTridy(){
    }
```

## Metody řazení třídou Comparator
### Řazení Stringu
```java
public class SortString implements Comparator<Trida>{
    @Override
    public int compare(Trida o1, Trida o2){
        return o1.getString().compareTo(o2.getString());
    }
}
```
### Řazení Intu
```java
public class SortInt implements Comparator<Trida>{
    @Override
    public int compare(Trida o1, Trida o2){
        return o1.getInt() - o2.getInt();
    }
}
```
### Collections Sort
```java
// volání třídy Comparator
public void sortString/Int(){
    Collections.sort(this.ArrayList, new SortString/Int());
}
```

## Práce se soubory

* Preferujeme konstrukci _try-with-resources_
* Proudy obvykle vyhazují výjimky, třeba odchytit

### Čtení textových souborů

#### BufferedReader

```java
public static String souborDoStringu(String cesta){
    File input = new File(cesta);
    String s="";
    try (BufferedReader br = new BufferedReader(new FileReader(input))) {
        // v případě hlavičky, ji můžeme "zahodit" takto:
        String hlavicka = br.readLine();
        String line;
        // Vypisujeme řádky do Stringu dokud nenarazíme na prázdný
        while ((line = br.readLine()) != null) {
            s += line + "\n";
        }
    }
    return s;
}
```

### Načtení souboru do ArrayListu

```java
public void nacistSouborDoList(String cesta){
    String s = "";
    try{
        // Obsah souboru do stringu
        s = SouborDoStringu(cesta);
    } catch ( ) { }
    // Rozdělení stringu na řádky
    String[] radky = s.split("\n");
    // Procházení všech řádků
    for(String radek : radky) {
        // Nahrazení 2 a více mezer za jednu mezeru
        radek = radek.replaceAll("\\s{2,}", " ");
        // Rozdělení řádku delimetrem
        String[] att = radek.split(" ");
        // Přidání nového objektu
        DatovyTypTridy nazevNove = new InstanceTridy(Integer.parseInt(att[0]), att[1]);
        this.instanceTridy.add(nazevNove);
    }
}
```

### Zápis textových souborů

#### PrintWriter

```java
public static void ulozeniDoSouboru(String cesta, String output){
    File file = new File(cesta);
    // parametr true / false jako `boolean append`
    try(BufferedWriter bw = new BufferedWriter(new PrintWriter(new FileWriter(file, true/false))){
        pw.write(output+"\n");
        pw.flush();
        pw.close();
    }
}
```

### Zápis binárních souborů

```java
public void ulozeniBinarky(String cesta, String output){
    File binaryFile = new File(cesta);
    try (DataOutputStream out = new DataOutputStream(new FileOutputStream(binaryFile, true/false))) {
        for(InstanceTridy nazevInstance:ArrayList){
            out.writeUTF("Text");
            out.writeBoolean(false);
            out.writeInt(50);
        }
    }    
}
```

* Mezi proudy ještě můžeme přidat `BufferedOutputStream`

### Čtení binárních souborů

```java
public static String cteniBinarky(String cesta){
StringBuilder sb = new StringBuilder();
try (DataInputStream in = new DataInputStream(new FileInputStream(cesta))) {
    boolean end = false;
    String text;
    int cislo;
    boolean pravda;
    while (!end) {
        try {
            text = in.readUTF();
            pravda = in.readBoolean();
            cislo = in.readInt();
            sb.append(StringFormat("%s %d %s", text, cislo, pravda));
            sb.append("\n");
        }
        catch (EOFException ex) {
            end = true;
        }
    }
    return sb.toString();
}
```

* Mezi proudy ještě můžeme přidat `BufferedInputStream`
