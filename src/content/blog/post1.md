---
title: "Demo Post 111111"
description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
pubDate: "Sep 10 2022"
heroImage: "/post_img.webp"
tags: ["tokio"]
---

# 1.搭建Get请求
```java
 public static String GET(String url) throws Exception{

        URL  url1 = new URL(url);
        HttpURLConnection connection = (HttpURLConnection) url1.openConnection();
        connection.setRequestMethod("GET");
        connection.setRequestProperty("Content-Type","application/json");
        connection.connect();
        InputStream is = connection.getInputStream();
        BufferedReader reader  = new BufferedReader(new InputStreamReader(is, StandardCharsets.UTF_8));
        StringBuilder sb  = new StringBuilder();
        String a = null;
        while ((a = reader.readLine()) != null) {
            sb.append(a);
        }
        return String.valueOf(sb);
    }
```

# 2.在比赛中Json封装成List<Map<String,String>> 性价比更高


```java
    public static List<Map<String,String>> JsonToListMap(String url) throws Exception
    {

        String get = GET(url);
        List<Map<String,String>> datalist = new ArrayList<>();
        JSONArray jsonArray = new JSONArray(get);
        for (int i = 0; i <jsonArray.length() ; i++)
        {
            JSONObject object = new JSONObject(jsonArray.optString(i));
            Map<String,String> map = new HashMap<>();
            Iterator<String> keys = object.keys();
            while (keys.hasNext())
            {
                String key = keys.next();
                map.put(key,object.optString(key));
            }
            datalist.add(map);
        }

        return datalist;
    }
```

