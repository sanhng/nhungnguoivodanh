当需要处理超大JSON文本时，需要Stream API，在fastjson-1.1.32版本中开始提供Stream API。

# 序列化
## 超大JSON数组序列化
如果你的JSON格式是一个巨大的JSON数组，有很多元素，则先调用startArray，然后挨个写入对象，然后调用endArray。
* 例1
      JSONWriter writer = new JSONWriter(new FileWriter("/tmp/huge.json"));
      writer.startArray();
      for (int i = 0; i < 1000 * 1000; ++i) {
            writer.writeValue(new VO());
      }
      writer.endArray();
      writer.close();

## 超大JSON对象序列化
如果你的JSON格式是一个巨大的JSONObject，有很多Key/Value对，则先调用startObject，然后挨个写入Key和Value，然后调用endObject。
* 例2
      JSONWriter writer = new JSONWriter(new FileWriter("/tmp/huge.json"));
      writer.startObject();
      for (int i = 0; i < 1000 * 1000; ++i) {
            writer.writeKey("x" + i);
            writer.writeValue(new VO());
      }
      writer.endObject();
      writer.close();

# 反序列化
## 例3      

      JSONReader reader = new JSONReader(new FileReader("/tmp/huge.json"));
      reader.startArray();
      while(reader.hasNext()) {
            VO vo = reader.readObject(VO.class);
            // handle vo ...
      }
      reader.endArray();
      reader.close();

## 例4

      JSONReader reader = new JSONReader(new FileReader("/tmp/huge.json"));
      reader.startObject();
      while(reader.hasNext()) {
            String key = reader.readString();
            VO vo = reader.readObject(VO.class);
            // handle vo ...
      }
      reader.endObject();
      reader.close();