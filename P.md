## Docker
- start all
    ```
        docker start $(docker ps -a | awk '{ print $1}' | tail -n +2)
    ```
    - ~~这里可能存在mac和linux的区别.$或许不应该加入~~ `发现原因.是因为fish shell 导致的 换用bash没有问题`
    - 该命令类似的可以使用到更多的docker通用命令上
    ```
        docker exec test_mongo mongo aaa --eval "db.createUser({user: 'bbb', pwd:  'aaa', roles:[{role:'readWrite',db:'aaa'}]});"
    ```
## Genymotion
- dev tools path
```
/Applications/Genymotion.app/Contents/MacOS/tools
```
## Spring
- spring-data-redis
  - 多个redisTemplate
    ```scala
    @Configuration
        class RedisConfig {

        @Bean(name = Array("longRedisTemplate"))
        def longTemplate(redisConnectionFactory: RedisConnectionFactory): RedisTemplate[String, Long] = {
            val longTemplate = new RedisTemplate[String, Long]
            longTemplate.setConnectionFactory(redisConnectionFactory)
            longTemplate.setValueSerializer(new GenericToStringSerializer(classOf[Long]))
            longTemplate
        }

        @Bean(name = Array("objectRedisTemplate"))
        def objectTemplate(redisConnectionFactory: RedisConnectionFactory): RedisTemplate[String, Object] = {
            val objectTemplate = new RedisTemplate[String, Object]
            objectTemplate.setConnectionFactory(redisConnectionFactory)
            objectTemplate
        }
        
        }
    ```
## Scala 
- match case
  - case 无法区别无类型和null 但是 因为 case 存在判断顺序 所以把null的判断写在上面的位置就可以避免这种情况
## Chrome
- 切回老版本标签栏样式
```
chrome://flags/#top-chrome-md
```
## java bean<->map
```java
/** 
 * 将对象装换为map 
 * @param bean 
 * @return 
 */  
public static <T> Map<String, Object> beanToMap(T bean) {  
    Map<String, Object> map = Maps.newHashMap();  
    if (bean != null) {  
        BeanMap beanMap = BeanMap.create(bean);  
        for (Object key : beanMap.keySet()) {  
            map.put(key+"", beanMap.get(key));  
        }             
    }  
    return map;  
}  
  
/** 
 * 将map装换为javabean对象 
 * @param map 
 * @param bean 
 * @return 
 */  
public static <T> T mapToBean(Map<String, Object> map,T bean) {  
    BeanMap beanMap = BeanMap.create(bean);  
    beanMap.putAll(map);  
    return bean;  
}  
  
/** 
 * 将List<T>转换为List<Map<String, Object>> 
 * @param objList 
 * @return 
 * @throws JsonGenerationException 
 * @throws JsonMappingException 
 * @throws IOException 
 */  
public static <T> List<Map<String, Object>> objectsToMaps(List<T> objList) {  
    List<Map<String, Object>> list = Lists.newArrayList();  
    if (objList != null && objList.size() > 0) {  
        Map<String, Object> map = null;  
        T bean = null;  
        for (int i = 0,size = objList.size(); i < size; i++) {  
            bean = objList.get(i);  
            map = beanToMap(bean);  
            list.add(map);  
        }  
    }  
    return list;  
}  
  
/** 
 * 将List<Map<String,Object>>转换为List<T> 
 * @param maps 
 * @param clazz 
 * @return 
 * @throws InstantiationException 
 * @throws IllegalAccessException 
 */  
public static <T> List<T> mapsToObjects(List<Map<String, Object>> maps,Class<T> clazz) throws InstantiationException, IllegalAccessException {  
    List<T> list = Lists.newArrayList();  
    if (maps != null && maps.size() > 0) {  
        Map<String, Object> map = null;  
        T bean = null;  
        for (int i = 0,size = maps.size(); i < size; i++) {  
            map = maps.get(i);  
            bean = clazz.newInstance();  
            mapToBean(map, bean);  
            list.add(bean);  
        }  
    }  
    return list;  
}  
```
