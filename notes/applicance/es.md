- [一、python连接es所需依赖](#一python连接es所需依赖)
- [二、链接es集群](#二链接es集群)
- [三、es查询](#三es查询)
- [四、es删除](#四es删除)

## 一、python连接es所需依赖

- `pip3 install elasticsearch`

## 二、链接es集群

```python
es = Elasticsearch(hosts=[{"host": "", "port": ""}, {"host": "", "port": ""}])
```

## 三、es查询
**es 查询基础语法**
- index：代表一个document存放在哪个index中
- doc_type：代表document属于index中的哪个类别（type）
- body：查询条件

```python
es.search(index="index_name", doc_type="type_name", body=body)

# 查询所有数据
body = {"query": {"match_all": {}}}

# 等于查询，term与terms
# term: 查询 xx = “xx”
body = {"query": {"term": {"name": "python"}}}
# terms: 查询 xx = “xx” 或 xx = “yy”
body = {"query": {"terms": {"name": ["python", "java"]}}}

# 包含查询，match与multi_match
# match: 匹配name包含"python"关键字的数据
body = {"query": {"match": {"name": "python"}}}
# multi_match: 在name和addr里匹配包含深圳关键字的数据
body = {"query":{"multi_match":{"query":"深圳", "fields":["name", "addr"]}}}

#  ids
body = {"query": {"ids": {"type": "type_name","values": ["1", "2"]}}}

# 复合查询bool，bool有3类查询关系，must(都满足),should(其中一个满足),must_not(都不满足)
body = {"query":{"bool":{"must":[{"term":{"name":"python"}},{"term":{"age":18}}]}}}

# 切片式查询
# 从第2条数据开始，获取4条数据
body = {"query":{"match_all":{}}, "from":2,"size":4}

# 范围查询
# 查询18<=age<=30的所有数据
body = {"query":{"range":{"age":{"gte":18,"lte":30}}}}

# 前缀查询
# 查询前缀为"p"的所有数据
body = {"query":{"prefix":{"name":"p"}}}

# 通配符查询
# 查询name以id为后缀的所有数据
body = {"query":{"wildcard":{"name":"*id"}}}
```

## 四、es删除
```python
# 删除指定index,type,id的数据
es.delete(index=index, doc_type=doc_type, id=id)

# 删除满足条件的所有数据,body必须符合DLS格式
es.delete_by_query(index=index, doc_type=doc_type, body=body)
```
