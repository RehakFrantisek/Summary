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

## Metody řazení
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
### Sort
```java
public void sortString/Int(){
    Collections.sort(this.ArrayList, new SortString/Int());
}
