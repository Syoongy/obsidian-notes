# Definition

----
## UnsortedTableMap
- Stores (key, value) pairs in a list
- any type of access would be a linear search voer the array
```Java
public class UnsortedTableMap<K,V> extends AbstractMap<K,V> {  
	/** Underlying storage for the map of entries. */  
	private ArrayList<MapEntry<K,V>> table = new ArrayList<>();  
	/** Returns the index of an entry with equal key, or -1 if none found. */  
	private int findIndex(K key) {  
		int n = table.size();  
		for (int j=0; j < n; j++)  
			if (table.get(j).getKey().equals(key))  
				return j;  
			return -1; // special value denotes that key was not found  
	}
...
```

