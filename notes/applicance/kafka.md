- [一、python连接kafka所需依赖](#一python连接kafka所需依赖)
- [二、kafka的生成者](#二kafka的生成者)
  - [2.1 带key和value的正常生产者](#21-带key和value的正常生产者)
  - [2.2 不带key的生产者](#22-不带key的生产者)
  - [2.3 带key但是value为空的生产者](#23-带key但是value为空的生产者)
- [三、消费者](#三消费者)

## 一、python连接kafka所需依赖
- `pip install kafka`
```python
from kafka import KafkaProducer, KeyedProducer
from kafka.errors import kafka_errors
```
## 二、kafka的生成者
### 2.1 带key和value的正常生产者
```python
def kafka_producer(key_data, value_data):
    producer = KafkaProducer(
        bootstrap_servers="",
        key_serializer=lambda k: json.dumps(k).encode(),
        value_serializer=lambda v: json.dumps(v).encode(),
    )
    future = producer.send(
        topic="",
        key=key_data,
        value=value_data
    )
    try:
        future.get(timeout=10)
    except kafka_errors as e:
        traceback.format_exc()
    finally:
        producer.close()
```

### 2.2 不带key的生产者
```python
def kafka_producer(key_data, value_data):
    producer = KafkaProducer(
        bootstrap_servers="",
        value_serializer=lambda v: json.dumps(v).encode(),
    )
    future = producer.send(
        topic="",
        value=value_data
    )
    try:
        future.get(timeout=10)
    except kafka_errors as e:
        traceback.format_exc()
    finally:
        producer.close()
```

### 2.3 带key但是value为空的生产者
- value为空，代表是为了进行删除操作，所以这个时候的key必须有值
- value为空，不是不传值，而是传空对象，在java代码中为 `Null` , python代码中为 `None`

```python
def kafka_producer(key_data, value_data):
    producer = KafkaProducer(
        bootstrap_servers="",
        key_serializer=lambda k: json.dumps(k).encode(),
        # value_serializer 不用设置，否则传 None 就会被转换
        # value_serializer=lambda v: json.dumps(v).encode(),
    )
    future = producer.send(
        topic="",
        key=key_data,
        value=None
    )
    try:
        future.get(timeout=10)
    except kafka_errors as e:
        traceback.format_exc()
    finally:
        producer.close()
```
## 三、消费者
```python
def kafka_consumer(topic):
    # 根据时间戳生成groupid
    group_id = get_distinct_groupid()
    consumer = KafkaConsumer(
        bootstrap_servers="",
        group_id=group_id,
        value_deserializer=lambda m: json.loads(m.decode()),
        auto_offset_reset="latest",
        consumer_timeout_ms=15000,
        enable_auto_commit=False,
        auto_commit_interval_ms=50
    )
    # 监听对应的topic
    consumer.subscribe(topic)
    try:
        while True:
            res = consumer.poll(timeout_ms=100, max_records=50)
            for item in res:
                print("res is:", res)
                kafka_dict = res[item][0].value
                print("kafka_dict is:", kafka_dict)
                offset = res[item][0].offset
                print("offset is:", offset)
            # 手动提交offset
            consumer.commit_async()
    except Exception as e:
        print(repr(e))
    finally:
        consumer.close()
```