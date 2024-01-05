## Security Annotation
### @PathVariable
> URI의 일부를 메서드의 매개변수로 바인딩하는 데 사용된다.

- @RequestMapping 또는 @GetMapping, @PostMapping 등과 같은 곳에 쓰이는 변수를 메서드의 매개변수로 전달한다.

```java
import org.springframework.web.bind.annotation.PathVariable;
// @Controller 내부 . . .

    @GetMapping("/articles/{id}") // URI 에서 사용되는 id 값을
    public String getArticle(@PathVariable Long id, Model model) { // 메서드의 매개변수로 사용 가능
        Article article = blogService.findById(id);
        model.addAttribute("article",new ArticleViewResponse(article));

        return "article";
    }

    // . . .
```