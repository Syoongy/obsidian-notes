# What does it do?
Stores (key, value) pairs and is also known as associative arrays

----
## Abstract Data Type
```Java
public interface Map<K,V> {  
	int size(); /** Returns the number of entries in the map. */  
	boolean isEmpty(); /** Tests whether the map is empty. */  
	V get(K key); /** Returns the value associated with the key, or null */  
	V put(K key, V value); /** Associates the given value with the given key. */  
	V remove(K key); /** Removes the entry with the key, and returns its value. */  
	/** Returns an iterable collection of the keys */  
	Iterable<K> keySet();  
	/** Returns an iterable collection of the values contained in the map. */  
	Iterable<V> values();  
	/** Returns an iterable collection of all key-value entries of the map. */  
	Iterable<Entry<K,V>> entrySet();  
}
```
![[map_example.png]]