## 之前的代码

```java
public Wechat getWechat() {
    StringBuilder hql = new StringBuilder();
    hql.append(" from Wechat w where 1=1 ");
    hql.append(" order by w.startTime desc ");
    Query query = this.getSession().createQuery(hql.toString());
    List<WxToKen> wxToKenList = query.list();
    if(wxToKenList.size()>0){
        return wxToKenList.get(0);
    }
    return null;
}
```
代码的意思是倒叙取第一条记录，也就是只需一条记录，其实正常逻辑这个表里只用存一条记录。
按现在的写法，会先把所有的记录都查出来，然后再取第一条（假分页），性能低。

## 现在的代码

```java
public Wechat getWechat() {
    String sql = "SELECT * FROM wechat limit 1";
    Query query = this.getSession().createSQLQuery(sql).addEntity(WxToKen.class);
    WxToKen token = (WxToKen) query.uniqueResult();
    return token;
}
```

hibernate的hql语句最终都是翻译成sql语句去执行，所以能用原声sql语句的尽量用sql。
这里用到了`limit 1`，就是从数据库取到一条记录就返回，就没必要继续往下查。