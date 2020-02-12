# Jackson
### Mapping
```Java
    /**
     * 引数のurlよりJSONデータを取得して返します。
     * @param url JSONデータ取得のurl
     * @return JSONデータ。存在しなければ{@link Optional#empty()}を返します。
     * @see JsonNode
     * @author HyungCheol Kim
     */
    private static Optional<JsonNode> metaTagData(String url) {
        ObjectMapper objectMapper = new ObjectMapper();
        try {
            JsonNode node = objectMapper.readValue(new URL(StringUtil.htmlUnescape(url)), JsonNode.class);
            if (node.get("code").asInt() != 1) {
                throw new CodeContextException().message("Json data is illegal -> "+node.toString());
            }
            return Optional.ofNullable(node);
        } catch (IOException e) {
            StandardLog.application().error(e);
        } catch (Exception e) {
            StandardLog.application().error(e);
        }
        return Optional.empty();
    }
```

### Use
```Java
/**
 * {
 *  "code": "1",
 *  "item": [
 *      {
 *          "title": "テストタイトル",
 *          "description": "テストディスクリプション",
 *          "keywords": "テストキーワード",
 *          "og:title": "テストogタイトル",
 *          "og:image": "テストogイメージ",
 *          "og:description": "テストogディスクリプション"
 *      }
 *  ],
 *  "total": "1"
 * }
 *
 */
@Builder
public class StaffDetailTag {
    @NonNull
    private final Optional<JsonNode> json;

    public String title() {
        return json.get().get("item").get(0).get("title").asText();
    }
    public String description() {
        return json.get().get("item").get(0).get("description").asText();
    }
    public String keywords() {
        return json.get().get("item").get(0).get("keywords").asText();
    }
    public String ogTitle() {
        return json.get().get("item").get(0).get("og:title").asText();
    }
    public String ogImage() {
        return json.get().get("item").get(0).get("og:image").asText();
    }
    public String ogDescription() {
        return json.get().get("item").get(0).get("og:description").asText();
    }
}
```

# Json serialize and deserialize
- https://stackoverflow.com/questions/12468764/jackson-enum-serializing-and-deserializer
- https://www.baeldung.com/jackson-serialize-enums