package edu.sjsu.cmpe.cache.client;

import edu.sjsu.cmpe.cache.client.DistributedCacheService;

public class Client {

    public static void main(String[] args) throws Exception {
        System.out.println("Starting Cache Client...");
        DistributedCacheService cache = new DistributedCacheService();
	
        // Add servers to cache
        cache.addUrl("http://localhost:3000");
        cache.addUrl("http://localhost:3001");
        cache.addUrl("http://localhost:3002");

        // Add data to cache
        cache.put(1, "a");
        cache.put(2, "b");
        cache.put(3, "c");
        cache.put(4, "d");
        cache.put(5, "e");
        cache.put(6, "f");
        cache.put(7, "g");
        cache.put(8, "h");
        cache.put(9, "i");
        cache.put(10, "j");
        
        //Retrieve data from cache  
        //System.out.println("put(1 => foo)");

      for ( long i =1; i < 11; i++) {
        	String value = cache.get(i);
        	System.out.println("get(" + i+ ") => " + value);
        }

      
        System.out.println("Existing Cache Client...");
    }

}

