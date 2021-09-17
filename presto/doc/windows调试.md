* 关闭系统校验

    ```
    PrestoSystemRequirements
    + warnRequirement("Hetu requires Linux or Mac OS X (found %s)", osName);
    - failRequirement("Hetu requires Linux or Mac OS X (found %s)", osName);
    ```
* getMaxFileDescriptorCount修改为固定值

    ```
    - OptionalLong maxFileDescriptorCount = getMaxFileDescriptorCount();
    + OptionalLong maxFileDescriptorCount = OptionalLong.of(10000);;
    ```

* 修改plugin加载方式
    *修改 presto-main 模块下 etc/config.properties 删除或注释 plugin.bundles 节点属性配置*
   `plugin.dir=../hetu-server/target/hetu-server-1.4.0-SNAPSHOT/plugin` 

* 配置hetu-metastore

    ```
    hetu.metastore.type=jdbc
    hetu.metastore.db.url=jdbc:mysql://localhost:3306/hetu
    hetu.metastore.db.user=root
    hetu.metastore.db.password=123456
    ```
* 配置memory.properties

    ```
    connector.name=memory
    memory.splits-per-node=4
    memory.max-data-per-node=2GB
    memory.spill-path=E:\\zybank\\code\\tmp\\data\\spill
    ```

* idea配置
	VM options: -ea -XX:+UseG1GC -XX:G1HeapRegionSize=32M -XX:+UseGCOverheadLimit -XX:+ExplicitGCInvokesConcurrent -Xmx2G -Dconfig=etc\config.properties -Dlog.levels-file=etc\log.properties
	working direction:$MODULE_DIR$

* 页面无法访问
  
  `hetu.queryeditor-ui.allow-insecure-over-http=true`