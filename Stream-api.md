当需要处理超大JSON文本时，需要Stream API，在fastjson-1.1.32版本中开始提供Stream API。

# 序列化

      JSONWriter writer = new JSONWriter(new FileWriter("/tmp/huge.json"));
      writer.startArray();
      for (int i = 0; i < 1000 * 1000; ++i) {
            writer.writeValue(new VO());
      }
      writer.endArray();
      writer.close();

# 反序列化
      
      JSONReader reader = new JSONReader(new FileReader("/tmp/huge.json"));
      reader.startArray();
      while(reader.hasNext()) {
            VO vo = reader.readObject(VO.class);
            // handle vo ...
      }
      reader.endArray();
      reader.close();
