
MongoDB分页插件
======

![](https://img.shields.io/badge/Java-1.8-orange.svg)

为MongoDB提供了开箱即用的分页能力. 详情参见我的博客[MongoDB分页的Java实现和分页需求的思考](https://www.cnblogs.com/woshimrf/p/mongodb-pagenation-performance.html)



# How to use


Maven for instance.
```xml
<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
</repositories>
```

For the latest release code:
```xml
<dependency>
    <groupId>com.github.Ryan-Miao</groupId>
    <artifactId>mongo-page-helper</artifactId>
    <version>1.0</version>
</dependency>
```

For the latest code:
```xml
<dependency>
    <groupId>com.github.Ryan-Miao</groupId>
    <artifactId>mongo-page-helper</artifactId>
    <version>master-SNAPSHOT</version>
</dependency>
```


接下来就可以愉快的玩耍了。


配置Configuration类
```java
@Configuration
public class MongoConfiguration{

    @Autowired
    private MongoTemplate mongoTemplate;
    @Bean
    public MongoPageHelper mongoPageHelper() {
        return new MongoPageHelper(mongoTemplate);
    }

}
```

直接在项目中使用

```java
public PageResult<StatByClientRs> findByDurationPage(FindByDurationPageRq rq) {
    final Query query = new Query(Criteria.where("duration").is(rq.getDuration()));

    return mongoPageHelper.pageQuery(query, StatByClient.class, rq.getPageSize(),
        rq.getPageNum(), mapper::mapToRs, rq.getLastId());
}
```

