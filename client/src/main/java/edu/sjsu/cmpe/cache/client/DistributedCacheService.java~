package edu.sjsu.cmpe.cache.client;

import java.util.*;
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.JsonNode;
import com.mashape.unirest.http.Unirest;
import com.mashape.unirest.http.exceptions.UnirestException;

/**
 * Distributed cache service
 * 
 */
public class DistributedCacheService implements CacheServiceInterface {
    private final HashMap<Integer,String> cacheUrls;

    public DistributedCacheService() {
        this.cacheUrls = new HashMap<Integer,String>();
    }

    public void addUrl(String url) {
	int i=cacheUrls.size();
        cacheUrls.put(i,url);
	//System.out.println("hasmap"+cacheUrls.get(0));	
	//System.out.println("hasmap"+cacheUrls.get(1));					
    }
    
    public String getAppropriateUrl(long key) {
    	int N=cacheUrls.size();
    	int hashvalue=(int)key % N;
    	String url=cacheUrls.get(hashvalue);
	//System.out.println("return url " + url);
	return url;
    }
    
    /**
     * @see edu.sjsu.cmpe.cache.client.CacheServiceInterface#get(long)
     */
    @Override
    public String get(long key) {
        HttpResponse<JsonNode> response = null;
        try {
            response = Unirest.get(this.getAppropriateUrl(key) + "/cache/{key}")
                    .header("accept", "application/json")
                    .routeParam("key", Long.toString(key)).asJson();
        } catch (UnirestException e) {
            System.err.println(e);
        }
        String value = response.getBody().getObject().getString("value");
	
	System.out.println("GET -->"+key+"->"+value+" ---URL-->"+getAppropriateUrl(key));
	
        return value;
    }

    /**
     * @see edu.sjsu.cmpe.cache.client.CacheServiceInterface#put(long,
     *      java.lang.String)
     */
    @Override
    public void put(long key, String value) {
    	
        HttpResponse<JsonNode> response = null;
        try {
	response = Unirest
                    .put(this.getAppropriateUrl(key) + "/cache/{key}/{value}")
                    .header("accept", "application/json")
                    .routeParam("key", Long.toString(key))
                    .routeParam("value", value).asJson();

	System.out.println("PUT -->"+key+"->"+value+" ---URL-->"+getAppropriateUrl(key));
	
        } catch (UnirestException e) {
            System.err.println(e);
        }

        if (response.getCode() != 200) {
            System.out.println("Failed to add to the cache.");
        }
    }
}

