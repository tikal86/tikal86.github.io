## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/tikal86/tikal86.github.io/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

[see observable svg page](svg.md)

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

```Java
package nl.tikal.reactive;

import io.reactivex.rxjava3.core.Flowable;
import io.reactivex.rxjava3.core.Observable;

/**
 * Hello world!
 *
 */
public class BlogDeel1
{
    public static void main( String[] args )
    {
        // Observable without backpressure
        Observable.just("Hello observable without backpressure")
            .subscribe(System.out::println);

        // Observable with backpressure
        Flowable.just("Hello flowable")
            .subscribe(System.out::println);

        // Operation
        Observable.just("Hello observable without backpressure", "Does not start with hello")
            .filter(text -> text.startsWith("Hello"))
            .subscribe(System.out::println);
    }
}

```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/tikal86/tikal86.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
