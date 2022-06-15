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
        s = SouborDoStringu(cesta);
    } catch ( ) { }
    String[] radky = s.split("\n");
    for(String radek : radky) {
        radek = radek.replaceAll("\\s{2,}", " ");
        String[] att = radek.split(" ");
        DatovyTypTridy nazevNove = new InstanceTridy(Integer.parseInt(att[0]), att[1]);
        this.instanceTridy.add(nazevNove);
    }
}
