# @PathVarialbe
ex) http://127.0.0.1/index/1

```
@PostMapping("delete/{idx}")
@ResponseBody
public JsonResultVo postDeleteFactory(@PathVariable("idx") int factoryIdx) {
	return factoryService.deleteFacotryData(factoryIdx);
}
```

# ThymeleafでList<Object>をpostする
https://medium-company.com/springboot-thymeleaf-list/