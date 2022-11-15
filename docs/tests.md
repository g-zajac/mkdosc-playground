# Test page
Test page for testing, formating, tools, plugins etc.\
Ver 1.0.8 

## Revision date

https://timvink.github.io/mkdocs-git-revision-date-localized-plugin/

<small><br><i>Updated {{ page.meta.revision_date }}</i></small>
{% endif %}

This page was last updated: *{{ git_revision_date_localized }}*

Created: {{ page.meta.git_created_date_localized }}

Page last revised on: {{ git_revision_date }}

## Math formulas

$$
@math $ \frac{\sqrt{2x}}{y} $
$$

$$
\operatorname{ker} f=\{g\in G:f(g)=e_{H}\}{\mbox{.}}
$$


## Flow charts
Text based flow chart, more info [here](https://mermaid-js.github.io/mermaid/#/). En example below.

``` mermaid
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
```

## Notes test

!!! info

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

!!! success
        hurrraaaa!

!!! failure

        buuuueeee!


## Icons
:fontawesome-regular-face-laugh-wink:
:fontawesome-abstract:


## Tabs
Could be used for code snipets, code / expectd response

=== "C"

    ``` c
    #include <stdio.h>

    int main(void) {
      printf("Hello world!\n");
      return 0;
    }
    ```

=== "C++"

    ``` c++
    #include <iostream>

    int main(void) {
      std::cout << "Hello world!" << std::endl;
      return 0;
    }
    ```

## hints

```bash
apt update # (1)
```

1. I'm a code annotation!


``` yaml
theme:
  features:
    - content.code.annotate # (1)
```

1.  :man_raising_hand: I'm a code annotation! I can contain `code`, __formatted
    text__, images, ... basically anything that can be written in Markdown.
